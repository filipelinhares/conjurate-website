---
layout: docs
title:  "Docs"
permalink: 'docs'
---

## Instalation

### Global

```bash
npm install -g conjurate
```

### Local

```bash
npm install --save-dev conjurate
```

`package.json ↓`

```json
{
  "scripts": {
    "gen": "conjurate"
  }
}
```

### npx

```bash
npx conjurate
```

## Config

```json
{
  "templatesSource": "./conjurate",
  "templates": {
    "template-name": "./default-output"
  }
}
```

### `templatesSource`

This is the folder where you keep your templates. By default it is `./conjurate` but you can set any other path.

#### Using npm packages

You can use npm packages as templates.

```json
{
  "templatesSource": "npm:package-name",
}
```

>  ℹ️ In <a href="/docs/#template-package">Template package</a> you can learn more about how to create your own.

### `templates`

This is where you set the templates created inside your `templatesSource` by passing their name and a default folder where the generated structure will be placed.

```json
{
 "templates": {
    "template-name": "./default-output"
  }
}
```


## CLI

### Structure Generating command:
```bash
conjurate <template-name> <placeholder-content>
```

#### `<template-name>`
The template name as in config file

#### `<placeholder-content>`
It will be replaced by the [`%placeholders%`](/docs/#placeholders) when running the generator command.

### Flags

#### Overwrite default-output in config file.
- `--output`
- alias `-o`

#### List your templates.
- `--templates`
- alias: `-t`

#### Show help message
- `--help`
- alias: `-h`

#### Output generation log messages
- `--logs`
- alias: `-l`
- default: `true`
- _disable:_ `--no-logs`

## Templates

Each folder inside your `templatesSource` is a template.

### Placeholders
You can use a placeholders when developing your templates to help with customization. It will be replaced by the <span>&lt;placeholder-content&gt;</span> passed in the CLI. It can be used in files name, files content and folders name.

| Placeholders | Result of "test string"|
| --- | -- |
|`%camel-case%` | `testString` |
|`%lower-case%` | `test_string` |
|`%no-case%` | `test string` |
|`%dot-case%` | `test.string` |
|`%dash-case%` | `test-case` |
|`%pascal-case%` | `TestCase` |
|`%path-case%` | `test/case` |
|`%snake-case%` | `test_string` |
|`%swap-case%` | `TEST CASE` |
|`%title-case%` | `Test case` |
|`%upper-case%` | `TEST_STRING` |
|`%first-word%` | `test` |
|`%last-word%` | `case` |

> ℹ️ If you want to use spaces when using the CLI, use quotes
>
>```bash
>conjurate component "test string"
>```

### Template package

Conjurate allow you to use npm packages as templates. You can find existing [templates](/templates) to use or create your own.


#### Create a template package
You can use the [create-conjurate-template](https://github.com/filipelinhares/create-conjurate-template) which is a Github's template repository.

1. Clone your new repository.
2. Configure your ./index.js as you do in templates config inside `.conjurate.json`
```js
module.exports = {
  component: './src/components'
}
```

3. Create your template folders inside ./templates, eg:
```
`-- templates
    `-- example
        `-- %dash-case%.js
```

4. Now inside your project, just configure your new template package:
```json
{
  "templatesSource": "npm:package-name",
}
```

>  ℹ️ To list your template in <a href="/templates">templates page</a> just add <code>conjurate-template</code> as a keyword in your npm package.


[travis-img]: https://travis-ci.org/filipelinhares/conjurate.svg?branch=master
[travis-url]: https://travis-ci.org/filipelinhares/conjurate
[changelog-image]: https://img.shields.io/badge/changelog-md-blue.svg?style=flat
[changelog-url]: CHANGELOG.md
[license-image]: https://img.shields.io/npm/l/conjurate.svg?style=flat
[license-url]: LICENSE.md
[npm-image]: https://img.shields.io/npm/v/conjurate.svg?style=flat
[npm-url]: https://www.npmjs.com/package/conjurate



