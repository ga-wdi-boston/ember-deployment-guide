[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# Ember Deployment Guide

Use this guide to deploy Ember apps based on our [Ember Template](https://github.com/ga-wdi-boston/ember-template)
to GitHub Pages.

## Prerequisites

-   [Ember Template](https://github.com/ga-wdi-boston/ember-template)
-   [Ember](https://github.com/ga-wdi-boston/ember)

## Objectives

By the end of this, developers should be able to:

-   Deploy an Ember app to GitHub Pages

## Deployment

1.  Make sure that everything is named consistently (i.e. `ember-template` ->
 `ember-deployment-example`).
1.  If you haven't already, run `npm install` and `bower install`.
1.  Update `config/environment.js` as follows:

  ```js
  if (environment === 'production') {
    ENV.baseURL = '/ember-deployment-example/';
    ENV.locationType = 'hash';
  }
  ```

1.  Make sure all work is committed and working on your `master` branch.
1.  Create a `gh-pages` branch locally and check it out. Merge `master` into
`gh-pages`.
1.  Remove `/dist` from `.gitignore`, add and commit.
1.  Run `ember build --environment=production`.
1.  `git add /dist` and commit.
1.  Use "subtree push" to create a new gh-pages branch on GitHub composed only
of the dist directory using:

  ```js
  git subtree push --prefix dist origin gh-pages
  ```
(Taken from [https://gist.github.com/cobyism/4730490](https://gist.github.com/cobyism/4730490))


## [License](LICENSE)

Source code distributed under the MIT license. Text and other assets copyright
General Assembly, Inc., all rights reserved.
