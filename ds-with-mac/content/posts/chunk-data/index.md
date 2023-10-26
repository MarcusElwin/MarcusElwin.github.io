---
title: Chunking of Data the BQ Way
seo_title: Chunk Data
summary: 
description: 
slug: chunk-data
author: Marcus Elwin

draft: false
date: 2023-10-25T21:53:32+02:00
lastmod: 2023-10-26T07:43:32+02:00
expiryDate: 
publishDate: 

feature_image: 
feature_image_alt: 

categories:
    - Data Engineering
tags:
    - BigQuery
    - BQ
    - Data
    - SQL
series:

toc: true
related: true
social_share: true
newsletter: false
disable_comments: false
---

Recently I had to work with a large client dataset of `100+` million rows and do quite some data cleaning and plumbing. :wrench: In order to prepare this dataset for running a parallel batch job. What it boiled down to in the end, was to create `chunks` of `1000` users in the batch job. 

In this post I'll share one nice way of doing so in `BigQuery` to reduce chunking and data export time from *hours* down to *minutes*!

## Chunking 
When processing data that contains a large number of records, processing each record *one-by-one* can be quite slow. Often data is also fetched from external sources such as an API. Whilst processing data in memory tends to be fast, there are natural memory limitations based on your compute instance. By *chunking* the data the processing of the job can be speed up **multifold**. A *chunk* is simple a grouped set of records according to some key and size e.g. chunks of `1000` users in each file. In order to fit everything in memory.

## Chunking the "naive" pythonic way
Let's say that you have a table called `transactions` with the schema below and `100` million transactions and `50` thousand unique users:
{{< highlight json "linenos=inline, style=monokai" >}}
[
    {
    "name": "transactionid",
    "mode": "REQUIRED",
    "type": "STRING",
    "description" "Unique ID of transaction",
    "fields": []    
    },
    {
    "name": "userid",
    "mode": "REQUIRED",
    "type": "STRING",
    "description" "Unique ID of user",
    "fields": []    
    },
    {
    "name": "accountid",
    "mode": "REQUIRED",
    "type": "STRING",
    "description" "Unique ID of users account",
    "fields": []    
    },
    {
    "name": "date",
    "mode": "NULLABLE",
    "type": "DATE",
    "description" "Date of transaction",
    "fields": []    
    },
    {
    "name": "amount",
    "mode": "NULLABLE",
    "type": "FLOAT64",
    "description" "Amount of transaction debit or credit based on sign",
    "fields": []    
    }
    {
    "name": "description",
    "mode": "NULLABLE",
    "type": "STRING",
    "description" "Transaction description",
    "fields": []    
    }
]
{{< / highlight >}}

The pythonic way shown below would be to:
* Create chunks based on all unique user IDs (`user_id_list`)
* Only query users for a given chunk
* Export data to a file e.g. `.csv`

{{< highlight python "linenos=inline, style=monokai" >}}
def chunk_list(x: list, chunk_size) -> list:
    return [x[i : i + chunk_size] for i in range(0, len(x), chunk_size)]

i=0
for user_id_list in chunk_list(df_userids.userid.tolist(), 1000):
    start_time = time.time()

    query = f"""SELECT *, _FILE_NAME 
               FROM `project.dataset.transactions`
               WHERE userid IN UNNEST({user_id_list})
            """
    result = datalake.query(query)
    df_batch = pd.read_csv(result)
{{< / highlight >}}

Although the code looks easy to understand, testing this on `100` million transactions takes roughly `~7+` hours. This is **way to slow** and we can do much better :brain:.

## Chunking using BigQuery
As BigQuery is "practically" spark under the hood we can use `partitioning` and especially two inbuilt functions [NTILE](https://cloud.google.com/bigquery/docs/reference/standard-sql/numbering_functions#ntile) and [RANGE_BUCKET](https://cloud.google.com/bigquery/docs/reference/standard-sql/mathematical_functions#range_bucket).

What the `NTILE` function is doing:
{{< notice info >}} 
`NTILE` *divides the rows into **constant_integer_expression** buckets based on row ordering and returns the 1-based bucket number that is assigned to each row. The number of rows in the buckets can differ by at most 1. The remainder values (the remainder of number of rows divided by buckets) are distributed one for each bucket, starting with bucket 1. If constant_integer_expression evaluates to NULL, 0 or negative, an error is provided.*
{{< /notice >}}

And what `RANGE_BUCKET` function is doing:
{{< notice info >}} 
`RANGE_BUCKET` *scans through a sorted array and returns the 0-based position of the point's upper bound. This can be useful if you need to group your data to build partitions, histograms, business-defined rules, and more..*
{{< /notice >}}

In short `NTILE` creates the `chunk` groups we want used in a `window function` whilst `RANGE_BUCKET` takes care of creating the partitions. 

In our previous example combining these two together would look like:
{{< highlight sql "linenos=inline, style=monokai" >}}
--we have 50k users and want 1000 users in each bucket i.e. 50k/1000-> 50
DECLARE num_buckets INT64;
SET num_buckets = 50;

CREATE TABLE `project.dataset.trx_user_batches`
PARTITION BY RANGE_BUCKET(id, GENERATE_ARRAY(1, num_buckets + 1, 1)) AS 
-- get transactions
WITH transactions AS (
SELECT *
FROM 
    `project.dataset.transactions`
),
--create n buckets / chunk to contain n users in our case 50
user_rank AS (
SELECT 
  *,  
  NTILE(num_buckets) OVER(ORDER BY userid) AS id
FROM report
),
--notice that we need to create num_buckets + 1 here
user_bucket AS (
SELECT
  *,
  RANGE_BUCKET(id, GENERATE_ARRAY(1, num_buckets + 1, 1)) AS bucket
FROM 
  user_rank
),
SELECT
  trx.userid,
  trx.accountid,
  trx.transactionid,
  trx.date,
  trx.amount,
  trx.description
  rb.id
FROM 
  transactions AS trx
INNER JOIN
  user_bucket AS ub
ON
  AND trx.userid = ub.userid
{{< / highlight >}}
 With this query we get `50` partitions with `~1000` users in each file or around `2` million transactions per file. This is a much smaller dataset that we can fit in memory (i.e. `Pandas`) compared to the `100` million rows we started with. For instance if you want to export the partitions as files for another job or workflow you could use:

{{< highlight sql "linenos=inline, style=monokai" >}}
EXPORT DATA
  OPTIONS (
    uri = 'gs://trx_user_batches/user_batch_*.csv',
    format = 'CSV',
    overwrite = true,
    header = true,
    field_delimiter = ';')
AS (
SELECT
  *
FROM 
  `project.dataset.trx_user_batches` 
ORDER BY
  userid ASC,
  accountid ASC,
  date ASC
);
{{< / highlight >}}

The nice thing with having the partitions and using `EXPORT DATA` statement, is that this is much faster the then the pytonic approach in terms of chunking. Exporting 50 partitions files takes roughly `~30-40` minutes instead if `7+` hours :rocket:.

{{< notice tip >}} 
By default `BigQuery` exports data `>= 1GB` to several files. This is true even if you have partitions in your dataset. If you want to force your export to only save output to 1 file given that the size of each file is `< 1 GB` you can add a `LIMIT` statement to e.g. `MAX_INTEGER` to force all data to the same worker.

{{< /notice >}}

An update to the query if you want to make sure that you save each partition to 1 file:
{{< highlight sql "linenos=inline, style=monokai" >}}
DECLARE num_files INT64;
SET num_files = 50;
FOR item in (SELECT idx FROM UNNEST(GENERATE_ARRAY(1, num_files + 1, 1)) AS idx WHERE idx < num_files)
DO
EXPORT DATA
  OPTIONS (
    uri = CONCAT('gs://trx_user_batches/user_batch_*', item.idx, '.csv'),
    format = 'CSV',
    overwrite = true,
    header = true,
    field_delimiter = ';')
AS (
SELECT
  *
FROM 
  `project.dataset.trx_user_batches` 
WHERE
    id = item.idx
ORDER BY
  userid ASC,
  accountid ASC,
  date ASC
LIMIT
    9223372036854775807
);
END FOR;
{{< / highlight >}}