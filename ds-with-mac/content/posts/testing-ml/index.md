---
title: Testing of ML Systems
seo_title: Testing of ML Systems
summary: Testing of ML systems, what I wish I knew when I deployed my first ML system.
description: 
slug: testing-ml
author: Marcus Elwin

draft: false
date: 2023-08-20T12:58:11+02:00
lastmod: 2023-08-21T08:50:11+02:00
expiryDate: 
publishDate: 

feature_image: 
feature_image_alt: 

categories:
    - MLOps
tags:
    - Machine Learning
    - Testing
series:

toc: true
related: true
social_share: true
newsletter: false
disable_comments: false
---

So you have secured data :tada: for your model and trained it with `model.train`, and maybe you have evaluated its performance on a *hold-out* test set or potentially done an `A/B-test`. However, how do you know that your model will work, when deployed? 

Can you ensure that your model still works after some slight changes in input data? In this article we will cover some considerations for how you can test your ML system to mitigate and take any relevant actions before and after you have deployed your model. 

This post has been inspired by some previous work such as:
* :computer: [How to Test Machine Learning Code and Systems](https://eugeneyan.com/writing/testing-ml/)
* :computer: [Effective testing for machine learning systems](https://www.jeremyjordan.me/testing-ml/)

## What is an ML system?

> ...The algorithm is only a small part of an ML system in production. The system also includes the business requierments...the interface where users and developers interact...the data stack, and the logic for developing, monitoring & updating your models, as well as the infrastructure. 
> — <cite>Chip Hueyn[^1]</cite>

[^1]: The above quote is excerpted from Huyen, C. (2022). Designing machine learning systems.

The image below shows a high-level overview of what an *ML-system* is:

![ML System](/ml-system.png "Overview of ML System adopted from Huyen, C. (2022). Designing machine learning systems.")

Starting with the *input* part of the system, one can see the following components:
* *ML System users*: this can be both external and internal such as end-users or internal teams or other *ML systems*.
* *Business Requirements*: depending on the company this might be from a *product manager*, *business translator* or other internal *stakeholders* as e.g. marketing.
* *ML System developers*: different roles such as *ML Engineer*, *AI Engineer*, *Data Scientist*, *Data Engineer* or *Software Developer*.

As popularized by Google in their 2015 paper [Hidden Technical Debt in Machine Learning Systems](https://proceedings.neurips.cc/paper_files/paper/2015/file/86df7dcfd896fcaf2674f757a2463eba-Paper.pdf) the actual ML algorithm is a quite small component of the entire system. You may have heard that data scientists tend to spend >= 20% of their time on actual modelling, and <= 80% of their time on other activities such as cleaning of data (this of course varies between different companies). 

Whilst *infrastructure*, *data*, *feature engineering*, *evaluation* and *deployment* are all **vital** components, especially when going from experimentation all the way to production. This is probably one of the reasons why *ML Engineering* has been so populare in the recent years. In my experience the E2E system design should be thought of already in the earlier stages of developing a ML system to ensure sucess of a ML project. 

On another note, here we use the term *ML System* but you might have also heard *data product*:

> Some might also call a ML system a **data product**

In my experience talking *purely* about the deployed ML model some of these components are important to include in your *testing* scope:
* Data
* Feature Engineering
* Evaluation 
* ML algorithm 

However, best practice is to test as much as you can.

## Why test a ML system?

By design ML systems and ML algorithms are `non-deterministic` and depending on the algorithm you choice it might be hard to exactly understand the inner workings (i.e. **white-box** vs **black-box** approaches). An ML system is not better then what data we feed to it i.e. *GIGO* (Garbage in Garbage Out), and data we use tend to be *biased*. 

Also with the advent of *Large Language Models* (LLMs) which is making the access to and development of ML powered systems accessible to anyone with API calling skills. Testing and making sure that such a system works (on common problem for LLMs is e.g. *hallucinations*), is imperative.

## Testing a ML system vs testing a traditional software system

The image below shows some key difference between a *traditional* software system (*software 1.0*) and a ML powered system (*software 2.0*):
1) In a traditional SW system *data* together with *logic* is used as input to produce a *desired behaviour*. 
2) IN a ML system *data* together with *desired behaviour* is used to as input to produce some *logic*.

![SW vs ML System](/sw-vs-ml-system.png "Differences between a traditional SW system and ML system. Note the differences in input and output for the different approaches. Adopted from J. Jordan (2020) Effective testing for machine learning systems.")

The relationship between input and output for (1) and (2) are sort of flipped. For (1) we need tests to ensure that our written logic manages to produce the actual expected behaviour i.e. a button will always get a certain color on a website regardless of the input. Whilst for (2) we try to encode certain behaviour in the *training dataset* used to train the model e.g. customers that would churn in a campaign or not, in order to build a system that "learns" what logic it should apply to find customers with a risk of churning. 

For a system of type (1) above testing usually boils down to:
* *Unit-testing*: individual units of source code is tested.
* *Regression-testing*: tests to make sure the previous fixes to bugs are working.
* *Integration-testing*: longer tests where the software module is tested E2E with adjecent systems.
* *Smoke-testing*: testing if a software is stable or not.
* *Feature-testing*: functional testing of different features in a software.

> It is not uncommon that a ML system also have additional SW components for e.g. rules, where some of these tests would also be of importance.

Tests for (2) will be covered in the following sections.

## Pre-training test(s)
These type of tests are used as different *sanity* checks to identify bugs early on in the development process of a ML system. As these tests can be ran withouth having a train model, we can use this to *short-circuit* training. Main goal here is to identify **errors** or **bugs** to avoid waisting a training job (cash :moneybag: & time :alarm_clock:). 

Some of these tests that I've been using:

1) Check shape of model output 
2) Check shape of model input 
3) Check output ranges 
4) Make <cite>assertions[^2]<cite> on your dataset 
5) Check for <cite>label leakage[^3]</cite> between your datasets

What I have been planning to add as test in the future:
1) Check that one training step of your model reduces the loss

The test above is also a good *sanity check* step if you are dealing with *deep learning* models as part of your training process.

[^2]: Assertions such as checking for *NULL*, *NaN* values, scaling of your dataset, unique values etc.
[^3]: *Label Leakage* is when we leak infomation from the training dataset to test or validation sets.

Below follows some examples of the mentioned tests:

{{< highlight python "linenos=inline, style=monokai" >}}
import tensorflow as tf

NUM_FEATURES = 10
NUM_LABELS = 3

def test_model_output_shape(self):
    """1) Testing that the model output is what we expect"""

    prediction = self.model(self.dummy_data)

    (_, _, output_shape) = prediction.shape

    self.assertEqual(output_shape, NUM_LABELS)

def test_model_input_shape(self):
    """2) Testing shapes of model input to match NUM_FEATURES""""
        # get dataset
        dataset: tf.Dataset = create_dataset(...)

        for features, labels in dataset:
            actual_shape = features.shape
            expected_shape = (1, NUM_FEATURES)
            self.assertEqual(actual_shape, expected_shape)

def test_each_sequence_is_a_unique_user(self):
    """4) Assertion test for testing that each 
    training sequence is a unique user"""
    # expected amount of users
    expected_num_users = 100

    # create dataset
    dataset: tf.Dataset = create_dataset(...)
    actual_num_users = len(list(set(dataset.user_id)))

    self.assertEqual(expected_num_users, actual_num_users

def test_no_user_leakage_all_sets_data_split(self):
    """5) Test to check label leakage between train, test and val sets"""
    train, test, val = data_split(self.dummy_transactions)

    # get intersection of each set
    intersection_train_test = set(
        train["user_id"]
    ).intersection(set(test["user_id"]))
    intersection_train_val = set(
        train["user_id"]
    ).intersection(set(val["user_id"]))
    intersection_test_val = set(
        test["user_id"]
    ).intersection(set(val["user_id"]))

    # verify that the intersection is equal to the empty set
    empty_set = set()
    self.assertEqual(intersection_train_test, empty_set)
    self.assertEqual(intersection_train_val, empty_set)
    self.assertEqual(intersection_test_val, empty_set)
{{< / highlight >}}

## Post-training test(s)
These type of tests do normally fall into two different groups: *invariance tests* & *directional expectation tests*. It is not uncommon that input data might slightly change over time. One example could be *income distribution* in a country that is changing due to a growing middle class. Other examples are e.g. test data such as transactional descriptions / narratives changes. Also note that for these test to make sense we need an actual *trained* model.

### Invariance test(s)
Real-world data might change due to various reason as we eluded to previously. These test aims to test how **stable** and **consistent** the ML model is to **pertubations**. Logic for these types of tests, whilst applied to training a model could also be seen as **data augmentation**.

Some of these tests that I've been using:

1) Assert that model output consistent to small changes in a *feature* of interest.

Where you can replace *feature* with any feature you would like to test e.g. *text descriptions*, *amount*, *date* etc.

To examplify even further, imagine that you have a dataset looking like the below at time *t*:

| Date   | Amount     | Description   |
| --------  | -------- | ------ |
| 2023-03-15 | 1500 EUR | AirBnB Payment |
| 2023-04-15 | 1500 EUR | AirBnB Payment |
| 2023-05-15 | 1500 EUR | AirBnB Payment|

Then at time time *t+1* the dataset looks like the below instead:
| Date   | Amount     | Description   |
| --------  | -------- | ------ |
| 2023-06-05 | 1650 EUR | AirBnB |
| 2023-07-09 | 1700 EUR | AirBnB |
| 2023-08-10 | 1450 EUR | AirBnB |

:question: Do you notice any changes here in the underlying date? This type of behaviour is something we want to test and make sure that our model learns to handle in order to be considered *stable* and *consistent*. 

I have used [faker](https://faker.readthedocs.io/en/master/) and [factor_boy](https://factoryboy.readthedocs.io/en/stable/) to generate dummy data to setup these tests in the past:

{{< highlight python "linenos=inline, style=monokai" >}}
import factory
from dataclasses import dataclass
from factory import Factory, Faker
from factory.fuzzy import (
    FuzzyChoice,
    FuzzyFloat,
)
from typing import Generic, TypeVar
from dateutil.relativedelta import relativedelta

T = TypeVar("T")

@dataclass
class DataType:
    user_id: str
    date: str
    amount: float
    description: str
    label: int

class BaseFactory(Generic[T], Factory):
    # Base class to enable typing o .create() method
    @classmethod
    def create(cls, **kwargs) -> T:
        return super().create(**kwargs)


class DataTypeFakeFactory(BaseFactory[DataType]):
    class Meta:
        model = Transaction

    user_id = Faker("uuid4")
    date = Faker("date_between", start_date="-1y")
    amount = FuzzyFloat(100, 2000)
    description = Faker("sentence")
    label = FuzzyChoice([0, 1])

class AmountInvarianceFakeFactory(DataTypeFakeFactory):
    description = "AirBnB"
    amount = FuzzyFloat(1500, 1700)
    date = factory.Sequence(
        lambda x: datetime.date(2023, 1, 15) + relativedelta(months=x)
    )
    label = 1
{{< / highlight >}}
Nice thing with *factory_boy* is that you can can easily create a `pd.DataFrame` object and feed it through your feature engineering pipeline for the test:

{{< highlight python "linenos=inline, style=monokai" >}}
def test_amount_invariance(self):
    """1) Example of invariance test using AmountInvarianceFakeFactory"""
    # create dummy data
    dummy_data = AmountInvarianceFakeFactory.create_batch(100)
    number_of_records = len(dummy_data)
    df = pd.DataFrame(data=dummy_data)

    # extract features and labels
    features, labels = create_dataset(df, ...)
    predictions = self.model.predict(features)
    nbr_correct = number_correct_predictions(predictions, labels)

    self.assertAlmostEqual(
        nbr_correct,
        number_of_records,
        msg="Different predictions!",
        delta=0.95 * number_of_records
    )
{{< / highlight >}}
Note that we are using the `assertAlmostEqual` here in the test and allow a deviance of `5%` in predictions in this example. If we would not do so, you would see some *flaky* faild builds in your CI/CD pipeline :tools:.

### Directional Expectations test(s)
These type of tests allows us to define a set of **pertubations** to the input which should have a predictable effect on the model output. Logic for these types of tests, whilst applied to training a model could also be seen as **data augmentation**.

Some of these tests that I've been using:

1) Assert that model output is *similar* by increasing a certain *feature* of interest, whilst keeping all other features constant.
2) Assert that model output is *similar* by decreasing a certain *feature* of interest, whilst keeping all other features constant.

Note the use of *similar* above, as we cannot guarante that the model output will be 100% equal in these case instead, on needs to operate on allowable threhsolds e.g. **1-3** standard deviation from the mean or +/- **2,5** p.p. as examples. What you should set as good threhsolds depends on your use case and data.

We build another `DataTypeFakeFactory` for the directional expectatons test:

{{< highlight python "linenos=inline, style=monokai" >}}
class IncreasingAmountFakeFactory(DataTypeFakeFactory):
    """Similar to the invariance test, we can define an increasing amount factory to test here"""
    description = FuzzyChoice(["AirBnB", "AirBnB Payment"])
    label = 1
    amount = factory.Sequence(lambda x: 1500 + 50 * x)
    date = factory.Sequence(
        lambda x: datetime.date(2023, 1, 15) + relativedelta(months=x)
    )
{{< / highlight >}}

We can now build the test using the `IncreasingAmountFakeFactory`:

{{< highlight python "linenos=inline, style=monokai" >}}
def test_increasing_amount_directional_expectations(self):
    """1) Example of directional expectations test using IncreasingAmountFakeFactory"""
    # create dummy data
    dummy_data = IncreasingAmountFakeFactory.create_batch(100)
    number_of_records = len(dummy_data)
    df = pd.DataFrame(data=dummy_data)

    # extract features and labels
    features, labels = create_dataset(df, ...)
    predictions = self.model.predict(features)
    nbr_correct = number_correct_predictions(predictions, labels)

    self.assertAlmostEqual(
        nbr_correct,
        number_of_records,
        msg="Different predictions!",
        delta=0.95 * number_of_records
    )
{{< / highlight >}}

## Data-drift test(s)
In a real-world setting input data and model output will change (it is not *stationary*), the image below shows an example of drift in income distribution:

![Drift](/drift.png "Example of data drift or label shift where income distribution in a certain market has drifted to the left between two different time periods, from low income to more people with high income. This can be due to natural reasons such as improved living standards, but needs to be handle by a ML system built for e.g. predicting income or using income as a feature.")

Drift for a given input dataset and model output can be due to many various reasons:
* Bugs in production or ML code.
* Changes or failures in *upstream* dependencies such as data producer used to create a dataset, modified schema, missing data etc.
* Changes created by the introduction of a ML model, in e.g. targeted marketing with *propensity modelling* you may effect the actions of person to do something they would not normally do (also called *degenerative* feedback loops).
* Production data is different from what was used during training.
* Unknown or not handled *edge-cases* or *outliers* such as the recent COVID-19 pandemic, i.e. it is proably not normal for people to hoarding toilet paper.

Due to the cases above we need ways of identifying when data is *drifting* from a previous state, to take any appropriate actions such as:
* Re-training a model
* Adding static rules for edge-cases
* Collecting more data.

Some of these tests that I've been using:

1) Test that the distribution of a certain *feature* has not changed *too much* over two time periods.

You can replace *feature* with any feature of interest but do note, that we use *test* and *too much* above. This as what it normally boils down to is to evaluate via statistical tests if there has been any *significant* difference in the underlying distribution of the input data or the model predictions. [Albi Detect](https://github.com/SeldonIO/alibi-detect) maintend by the company [Seldon](https://www.seldon.io/) has a quite nice list of drift detection [methods](https://github.com/SeldonIO/alibi-detect#drift-detection).

What I have used before in these scenarios:
1) *T-test*
2) *Kolmogorov-Smirnov test*
3) *Kullback–Leibler divergence*

With a *null hypotehsis* threshold of **0.025 - 0.05** depending on the dataset. Sometimes you may have to use higher thresholds.

Example below on how a KS-test could be used as a test, for testing if the *mean distribution* has changed:
{{< highlight python "linenos=inline, style=monokai" >}}
from scipy import stats

def is_drifting_distribution(self, df, type="mean"):
    # Performs Kolmogorov-Smirnov-test on the amount distribution
    distribution_a, distribution_b = self.data.get_amount_distribution(
        df, test_value=type
    )
    test = stats.ks_2samp(distribution_a, distribution_b)
    return (
        test.pvalue < self._null_hypothesis_threshold, 
        test.pvalue, 
        test.statistic
    )

def test_mean_drift(self):
    # Only perform test if we have enough data
    if self.data.has_enough_data:
        for dataset in self._data_distributions.keys():
            df = self._data_distributions[dataset]
            ks_drift, ks_pvalue, ks_stat = self.is_drifting_distribution(df)
            self.assertFalse(
                ks_drift
            )
    self.assertTrue(True)
{{< / highlight >}}

You can of course replace *mean* with any other statistical metric such as *median*, *variance* etc. If the drift checks should be alerts in another system or parts of your CI pipeline is up to you, the important take away is that you have a process around it and can get alerted either before deployment or after. Much more can be said about *drift-detection* that might be a topic for another post in the future. 

In the meantime if you are more interested I recommend: 
* *Chapter 8* of :book: *Designing machine learning systems* by Chip Hueyn that provides a good overview.

Wow great job :muscle:, if you have made it this far after some 10+ minutes. This post turned out to be longer then what I expected. Hopefully you have found something useful in what has worked for me before, plus some insperation for further resources.

Stay tuned for the coming posts!