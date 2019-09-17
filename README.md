# Zola Deploy Action

A GitHub action to automatically build and deploy your [zola] site to the master
branch as GitHub Pages.

## Table of Contents

 - [Usage](#usage)
 - [Secrets](#secrets)
 - [Custom Domain](#custom-domain)

## Usage

In `.github/workflows` you can put any `.yml` file and put the following contents inside.

```
on:
  push:
    branches:
      - master
name: Build and deploy on push
jobs:
  build:
    name: zbrox/zola-deploy-action
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: zbrox/zola-deploy-action
      uses: zbrox/zola-deploy-action@master
      env:
        TOKEN: ${{ secrets.TOKEN }}
```

## Secrets

 * `TOKEN`: Personal Access key with the scope `public_repo`, we need this
    to push the site files back to the repo.
    
    ( Actions already provides a `GITHUB_TOKEN` which is an installation token and does not trigger a GitHub Pages builds hence we need a personal access token )

## Environment Variables
* `PAGES_BRANCH`: The git branch of your repo to which the built static files will be pushed. Default is `gh-pages` branch

## Custom Domain

If you're using a custom domain for your GitHub Pages site put the CNAME 
in `static/CNAME` so that zola puts it in the root of the public folder
which is where GitHub expects it to be.

[zola]: https://github.com/getzola/zola
