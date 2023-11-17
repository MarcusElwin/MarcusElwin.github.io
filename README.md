# ds-with-mac
![hugo workflow](https://github.com/MarcusElwin/MarcusElwin.github.io/actions/workflows/hugo.yml/badge.svg)
![typos workflow](https://github.com/MarcusElwin/MarcusElwin.github.io/actions/workflows/typos.yml/badge.svg)

DS portfolio websites + blog made easily in Hugo

# Setup 🛠️
1. Install hugo `brew install hugo`
2. Init & update submodules
   ```sh
   git submodule init && git submodule update
   ```

## Typo checks
This repo uses [typos](https://github.com/crate-ci/typos/tree/master) for typo checks to run locally:
```sh
# check typos in content folder
typos ./ds-with-mac/content/ 
```

```sh
# correct typos in folder
typos ./ds-with-mac/content/ -w
```

### Creating posts
```sh
# create new post
hugo new posts/<name>/index.md
```

```sh
# server website locally
hugo server
```