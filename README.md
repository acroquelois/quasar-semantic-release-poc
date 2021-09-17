# Quasar semantic versionning automation

This repository is a scaffold of quasar app with automatic semantic version on git tag changing

## Features
CI catch git tag update and make:
* update package.json version
* update CHANGELOG.md

## Implement on existing project

### 1) Update quasar.conf.js

```js
build: {
  env: {
    QUASAR_APP_VERSION: require('./package.json').version
  }
}
```

Then you can use ```process.env.QUASAR_APP_VERSION``` in your code

### 2) Add standard-version node package

> npm install --save-dev standard-version

This package is used to update the CHANGELOG.md and package.json:

**Update ```package.json``` script:**

```json
"scripts": {
    "release": "standard-version",
    "release:patch": "standard-version --release-as patch",
    "release:minor": "standard-version --release-as minor",
    "release:major": "standard-version --release-as major"
  }
  ```

**Create config file ```.versionrc.js```:**


```json
{
  "types": [
    {"type": "feat", "section": "Features"},
    {"type": "fix", "section": "Bug Fixes"},
    {"type": "chore", "hidden": true},
    {"type": "docs", "hidden": true},
    {"type": "style", "hidden": true},
    {"type": "refactor", "hidden": true},
    {"type": "perf", "hidden": true},
    {"type": "test", "hidden": true}
  ]
}

```
repo & doc: https://github.com/conventional-changelog/standard-version

### 3) Add commit linter

We need commit linter to ensure that our commit respect to commit convention established

**Install husky & commitlint:**
> npm install --save-dev husky

> npm install --save-dev @commitlint/cli

> npm install --save-dev @commitlint/config-conventional


commit lint doc: https://github.com/conventional-changelog/commitlint

**Chose your commit convention in ```.commitlintrc.json```:**

```json
{
  "extends": ["@commitlint/config-conventional"]
}
```

**Setup git hook:**

To make the linter available you need to setup the Git hook:
> husky install

> husky add .husky/commit-msg "yarn commitlint --edit $1"

To active the hook for user who just clone the repo run the Git hook setup in the ```npm prepare``` command who his automatically run before ```npm install```:

```json
"scripts": {
    "prepare": "husky install",
    "dev": "quasar dev",
    "release": "standard-version",
    "lint": "eslint --ext .js,.vue ./",
    "test": "echo \"No test specified\" && exit 0"
  }
```
