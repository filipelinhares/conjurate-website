---
layout: learn
title:  "Learning"
permalink: 'getting-started'
---

# Getting started

## Introduction

Conjurate is a generator tool that you can easily plug into your project and it helps generating new folders and files structures based on templates.

## Guide
In this guide you will learn how to setup and use Conjurate in a sample project which is a component library.

Let's start with the following structure:

```diff
|-- package.json
`-- src
    `-- components
```


### Generating the config file

First you need to create the `.conjurate.json` file. You can use the CLI passing the `--init` flag and it will be generated automatically.

```bash
npx conjurate --init
Select your "templatesSource" folder. (default: ./conjurate)
✔  success   Created conjurate
✔  success   Created .conjurate.json
```

You need to set your `templatesSource` which represents the folder where you'll keep your templates, the default is set to `./conjurate` but you can set any path.

```diff
+|-- .conjurate.json
+|-- conjurate
|-- package.json
`-- src
    `-- components
```


### Configuring
Now let's edit the `.conjurate.json` file.

`.conjurate.json ↓`

```json
{
  "templatesSource": "./conjurate",
  "templates": {
    "<template-name>": "./<default-output>"
  }
}
```

`./conjurate` is already set as the `templateSource` of the project.

Now let's set the name and default output path for the component template.

```diff
{
  "templatesSource": "./conjurate",
  "templates": {
-    "<template-name>": "./<default-output>"
+    "component": "./src/components"
  }
}
```

> ℹ️ In [config documentation](/docs/#config) you can learn more about the config file structure and template packages

### Creating templates

Templates in Conjurate is where you keep your templates used to generate your structure.

In this example let's create the `component` template:
```diff
+|-- conjurate
+|   `-- component
+|       |-- %dash-case%.css
+|       |-- %dash-case%.js
+|       `-- tests
+|           `-- index.js
├── .conjurate.json
├── package.json
└── src
  └── components
```

In the filename we're using [`%placeholders%`](/docs/#placeholders), it will be replaced by the `<placeholder-content>` argument that you provide when running the generator.

You can also use placeholders in files content, here is an example:

`./conjurate/component/%dash-case%.js ↓`

```javascript
import %camel-case%Style from './%dash-case%.css' 

class %pascal-case% extends Component {
  constructor() {
    super();
  }

  styles() {
    return [%camel-case%Style];
  }

  render() {
    return `${this.say} %dash-case%`;
  }
}

export default %pascal-case%; 
```

`./conjurate/component/tests/index.js ↓`
```js
import %pascal-case% from '../%dash-case%.js';
```

### Generating the structure

With the templates configured now just run the generator command:

```bash
npx conjurate component my-input
✔  success   Created my-input.css
✔  success   Created my-input.js
✔  success   Created tests
✔  success   Created tests/index.js
```

- `component` is the name of the template.
- `my-input` is our placeholder content.

```diff
|-- conjurate
|   `-- component
|       |-- %dash-case%.css
|       |-- %dash-case%.js
|       `-- tests
|           `-- index.js
|-- package.json
`-- src
    `-- components
+        `-- my-input
+            |-- my-input.css
+            |-- my-input.js
+            `-- tests
+                `-- index.js
```

`./conjurate/input/index.js ↓`
```diff
+import myInputStyle from './my-input.css' 
+
+class MyInput extends Component {
+  constructor() {
+    super();
+  }
+
+  styles() {
+    return [myInputStyle];
+  }
+
+  render() {
+    return `${this.say} my-input`;
+  }
+}
+
+export default MyInput;
```

`./conjurate/component/tests/index.js ↓`
```diff
+import MyInput from '../my-input.js';
```
