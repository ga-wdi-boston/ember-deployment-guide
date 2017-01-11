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

## Deployment to Github

1.  If you haven't already, run `npm install` and `bower install`.
1.  Make sure that everything is named consistently (i.e. `ember-template` ->
 `<% NAME OF YOUR CLIENT %>`). (Search via `command+shift+f`)
1.  You need to tell your Ember client to _point_ to your deployed API. Update
`config/environment.js` to follow below:

```js
module.exports = function(environment) {
  var ENV = {
    modulePrefix: '<% NAME OF YOUR CLIENT will be here %>',
    environment: environment,
    rootURL: '/',
    locationType: 'auto',
    apiHost: 'http://localhost:3000/',
    EmberENV: {
      FEATURES: {
        // Here you can enable experimental features on an ember canary build
        // e.g. 'with-controller': true
      }
    },
```

**Yes, use `var`, not `let` for ENV.**

AND FURTHER DOWN IN `config/environment.js`:

```js
if (environment === 'production') {
  ENV.rootURL = '/';
  ENV.locationType = 'hash';
  ENV.apiHost = '<% replace with the URL to your deployed API %>';
}
```
#### Important:

- Note that `rootURL` is *NOT* camelcase. For example, `rootUrl` will not work.


1.  Now you have to ensure you have your `application/adapter` and `ajax` files
import the `apiHost` link.

In `application/adapter` file:

```js
import ActiveModelAdapter from 'active-model-adapter';
import ENV from '<% ember-deployment-example name %>/config/environment';

export default ActiveModelAdapter.extend({
  host: ENV.apiHost,
  ...
  ...
  ...
});
```

IF/WHEN you have a `ajax/service` file:

```js
import AjaxService from 'ember-ajax/services/ajax';
import ENV from '<% ember-deployment-example name %>/config/environment';

export default AjaxService.extend({
  host: ENV.apiHost,
  ...
  ...
  ...
});
```

1.  Make sure all work is committed and working on your **`master`** branch.
1.  Create a `gh-pages` branch locally via `git checkout -b gh-pages`.
1.  **DO NOT PUSH TO GH-PAGES YET**
1.  Remove `/dist` from `.gitignore` by adding a '#' before it.
1.  Add and commit this change.
1.  Run `ember build --environment=production`.
1.  `git status` and add all files changed (_mainly `dist/`_) and some other changes; Then `commit` all changes.
1.  Use "subtree push" to create a new gh-pages branch on GitHub composed only
of the dist directory by using:

```js
git subtree push --prefix dist origin gh-pages
```

1.  Go check to your github page site and ensure all requests are working and appear
the same as on localhost:4200.
1.  Congrats, you've successfully deployed your Ember App!

## [License](LICENSE)

1.  All content is licensed under a CC­BY­NC­SA 4.0 license.
1.  All software code is licensed under GNU GPLv3. For commercial use or
    alternative licensing, please contact legal@ga.co.
