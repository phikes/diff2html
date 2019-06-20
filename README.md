# diff2html

[![Codacy Quality Badge](https://api.codacy.com/project/badge/Grade/06412dc3f5a14f568778d0db8a1f7dc8)](https://www.codacy.com/app/rtfpessoa/diff2html?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=rtfpessoa/diff2html&amp;utm_campaign=Badge_Grade)
[![Codacy Coverage Badge](https://api.codacy.com/project/badge/Coverage/06412dc3f5a14f568778d0db8a1f7dc8)](https://www.codacy.com/app/rtfpessoa/diff2html?utm_source=github.com&utm_medium=referral&utm_content=rtfpessoa/diff2html&utm_campaign=Badge_Coverage)
[![Circle CI](https://circleci.com/gh/rtfpessoa/diff2html.svg?style=svg)](https://circleci.com/gh/rtfpessoa/diff2html)
[![Dependency Status](https://dependencyci.com/github/rtfpessoa/diff2html/badge)](https://dependencyci.com/github/rtfpessoa/diff2html)

[![npm](https://img.shields.io/npm/v/diff2html.svg)](https://www.npmjs.com/package/diff2html)
[![Dependency Status](https://david-dm.org/rtfpessoa/diff2html.svg)](https://david-dm.org/rtfpessoa/diff2html)
[![devDependency Status](https://david-dm.org/rtfpessoa/diff2html/dev-status.svg)](https://david-dm.org/rtfpessoa/diff2html#info=devDependencies)

[![node](https://img.shields.io/node/v/diff2html.svg)]()
[![npm](https://img.shields.io/npm/l/diff2html.svg)]()
[![npm](https://img.shields.io/npm/dm/diff2html.svg)](https://www.npmjs.com/package/diff2html)
[![Gitter](https://badges.gitter.im/rtfpessoa/diff2html.svg)](https://gitter.im/rtfpessoa/diff2html?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

diff2html generates pretty HTML diffs from git or unified diff output.

[![NPM](https://nodei.co/npm/diff2html.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/diff2html/)

## Features

* Supports git and unified diffs

* Line by line and Side by side diff

* New and old line numbers

* Inserted and removed lines

* GitHub like style

* Code syntax highlight

* Line similarity matching

* Easy code selection

## Online Example

> Go to [diff2html](https://diff2html.xyz/)

## Distributions

* [WebJar](http://www.webjars.org/)

* [Node Module](https://www.npmjs.org/package/diff2html)

* [Bower Package](http://bower.io/search/?q=diff2html)

* [Node CLI](https://www.npmjs.org/package/diff2html-cli)

* Manually download and import `dist/diff2html.min.js` into your page

## How to use

To load correctly in the Browser you always need to include the stylesheet in the final HTML.

Import the stylesheet

```html
<!-- CSS -->
<link rel="stylesheet" type="text/css" href="dist/diff2html.css">
```

You can also refer to it from a CDN like [CDNJS](https://cdnjs.com/libraries/diff2html).

### Browser Library

Import the stylesheet and the library code

```html
<!-- CSS -->
<link rel="stylesheet" type="text/css" href="dist/diff2html.css">

<!-- Javascripts -->
<script type="text/javascript" src="dist/diff2html.js"></script>
```

It will now be available as a global variable named `Diff2Html`.

```js
var diffHtml = Diff2Html.getPrettyHtml(
  '<Unified Diff String>',
  {inputFormat: 'diff', showFiles: true, matching: 'lines', outputFormat: 'side-by-side'}
);
document.getElementById("destination-elem-id").innerHTML = diffHtml;
```

### Node Module

```js
let diff2html = require("diff2html").Diff2Html
```

### Angular

* Typescript

```typescript
// import diff2html
import {Diff2Html} from 'diff2html'
import {Component, OnInit} from '@angular/core';


export class AppDiffComponent implements OnInit {
  outputHtml: string;
  constructor() {
    this.init();
  }

  ngOnInit() {
  }

  init() {
    let strInput = "--- a/server/vendor/golang.org/x/sys/unix/zsyscall_linux_mipsle.go\n+++ b/server/vendor/golang.org/x/sys/unix/zsyscall_linux_mipsle.go\n@@ -1035,6 +1035,17 @@ func Prctl(option int, arg2 uintptr, arg3 uintptr, arg4 uintptr, arg5 uintptr) (\n \n // THIS FILE IS GENERATED BY THE COMMAND AT THE TOP; DO NOT EDIT\n \n+func Pselect(nfd int, r *FdSet, w *FdSet, e *FdSet, timeout *Timespec, sigmask *Sigset_t) (n int, err error) {\n+\tr0, _, e1 := Syscall6(SYS_PSELECT6, uintptr(nfd), uintptr(unsafe.Pointer(r)), uintptr(unsafe.Pointer(w)), uintptr(unsafe.Pointer(e)), uintptr(unsafe.Pointer(timeout)), uintptr(unsafe.Pointer(sigmask)))\n+\tn = int(r0)\n+\tif e1 != 0 {\n+\t\terr = errnoErr(e1)\n+\t}\n+\treturn\n+}\n+\n+// THIS FILE IS GENERATED BY THE COMMAND AT THE TOP; DO NOT EDIT\n+\n func read(fd int, p []byte) (n int, err error) {\n \tvar _p0 unsafe.Pointer\n \tif len(p) > 0 {\n";
    let outputHtml = Diff2Html.getPrettyHtml(strInput, {inputFormat: 'diff', showFiles: true, matching: 'lines'});
    this.outputHtml = outputHtml;
  }
}
```

* HTML

```html
<!DOCTYPE html>
<html>
  <head>
    <title>diff2html</title>
  </head>
  <body>
    <div [innerHtml]="outputHtml"></div>
  </body>
</html>
```

* `.angular-cli.json` - Add styles

```json
"styles": [
  "diff2html.min.css"
]
```

### Vue.js

```vue
<template>
    <div v-html="prettyHtml" />
</template>

<script>
import { Diff2Html } from "diff2html";
import "diff2html/dist/diff2html.min.css";

export default {
  data() {
    return {
      diffs: "--- a/server/vendor/golang.org/x/sys/unix/zsyscall_linux_mipsle.go\n+++ b/server/vendor/golang.org/x/sys/unix/zsyscall_linux_mipsle.go\n@@ -1035,6 +1035,17 @@ func Prctl(option int, arg2 uintptr, arg3 uintptr, arg4 uintptr, arg5 uintptr) (\n \n // THIS FILE IS GENERATED BY THE COMMAND AT THE TOP; DO NOT EDIT\n \n+func Pselect(nfd int, r *FdSet, w *FdSet, e *FdSet, timeout *Timespec, sigmask *Sigset_t) (n int, err error) {\n+\tr0, _, e1 := Syscall6(SYS_PSELECT6, uintptr(nfd), uintptr(unsafe.Pointer(r)), uintptr(unsafe.Pointer(w)), uintptr(unsafe.Pointer(e)), uintptr(unsafe.Pointer(timeout)), uintptr(unsafe.Pointer(sigmask)))\n+\tn = int(r0)\n+\tif e1 != 0 {\n+\t\terr = errnoErr(e1)\n+\t}\n+\treturn\n+}\n+\n+// THIS FILE IS GENERATED BY THE COMMAND AT THE TOP; DO NOT EDIT\n+\n func read(fd int, p []byte) (n int, err error) {\n \tvar _p0 unsafe.Pointer\n \tif len(p) > 0 {\n"
    };
  },
  computed: {
    prettyHtml() {
      return Diff2Html.getPrettyHtml(this.diffs, {
          inputFormat: "diff",
          showFiles: true,
          matching: "lines",
          outputFormat: "side-by-side"
        });
    }
  }
};
</script>
```

## API

> Intermediate Json From Git Word Diff Output

    getJsonFromDiff(input: string, configuration?: Options): Result[]

> Pretty HTML diff

    getPrettyHtml(input: any, configuration?: Options): string

> Check out the `typescript/diff2html.d.ts` for a complete API definition in TypeScript.

> Check out the `docs/demo.html` for a demo example.

## Configuration
The HTML output accepts a Javascript object with configuration. Possible options:

  - `inputFormat`: the format of the input data: `'diff'` or `'json'`, default is `'diff'`
  - `outputFormat`: the format of the output data: `'line-by-line'` or `'side-by-side'`, default is `'line-by-line'`
  - `showFiles`: show a file list before the diff: `true` or `false`, default is `false`
  - `matching`: matching level: `'lines'` for matching lines, `'words'` for matching lines and words or `'none'`, default is `none`
  - `matchWordsThreshold`: similarity threshold for word matching, default is 0.25
  - `matchingMaxComparisons`: perform at most this much comparisons for line matching a block of changes, default is `2500`
  - `maxLineSizeInBlockForComparison`: maximum number os characters of the bigger line in a block to apply comparison, default is `200`
  - `maxLineLengthHighlight`: only perform diff changes highlight if lines are smaller than this, default is `10000`
  - `templates`: object with previously compiled templates to replace parts of the html
  - `rawTemplates`: object with raw not compiled templates to replace parts of the html
  - `renderNothingWhenEmpty`: render nothing if the diff shows no change in its comparison: `true` or `false`, default is `false`
  > For more information regarding the possible templates look into [src/templates](https://github.com/rtfpessoa/diff2html/tree/master/src/templates)

** Diff2HtmlUI Helper Options **
  - `synchronisedScroll`: scroll both panes in side-by-side mode: `true` or `false`, default is `false`

> For more information regarding the possible templates look into [src/templates](https://github.com/rtfpessoa/diff2html/tree/master/src/templates)


## Diff2HtmlUI Helper

> Simple wrapper to ease simple tasks in the browser such as: code highlight and js effects

* Invoke Diff2html
* Inject output in DOM element
* Enable collapsible file summary list
* Enable syntax highlight of the code in the diffs

### How to use

#### Mandatory HTML resource imports

```html
<!-- CSS -->
<link rel="stylesheet" type="text/css" href="dist/diff2html.css">

<!-- Javascripts -->
<script type="text/javascript" src="dist/diff2html.js"></script>
<script type="text/javascript" src="dist/diff2html-ui.js"></script>
```

#### Init

```js
var diff2htmlUi = new Diff2HtmlUI({diff: diffString});
// or
var diff2htmlUi = new Diff2HtmlUI({json: diffJson});
```

#### Draw

```js
diff2htmlUi.draw('html-target-elem', {inputFormat: 'json', showFiles: true, matching: 'lines'});
```

#### Syntax Highlight

> Add the dependencies.
Choose one color scheme, and add the main highlight code. Note that the stylesheet for the color scheme must come **before** the main diff2html stylesheet.
If your favourite language is not included in the default package also add its javascript highlight file.

```html
<!-- Stylesheet -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.13.1/styles/github.min.css">
<link rel="stylesheet" type="text/css" href="dist/diff2html.css">

<!-- Javascripts -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.2.3/jquery.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.13.1/highlight.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/9.13.1/languages/scala.min.js"></script>
<script type="text/javascript" src="dist/diff2html-ui.js"></script>
```

> Invoke the Diff2HtmlUI helper

```js
$(document).ready(function() {
    var diff2htmlUi = new Diff2HtmlUI({diff: lineDiffExample});
    diff2htmlUi.draw('#line-by-line', {inputFormat: 'json', showFiles: true, matching: 'lines'});
    diff2htmlUi.highlightCode('#line-by-line');
});
```

#### Collapsable File Summary List

> Add the dependencies.

```html
<!-- Javascripts -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.2.3/jquery.js"></script>
<script type="text/javascript" src="dist/diff2html-ui.js"></script>
```

> Invoke the Diff2HtmlUI helper

```js
$(document).ready(function() {
    var diff2htmlUi = new Diff2HtmlUI({diff: lineDiffExample});
    diff2htmlUi.draw('#line-by-line', {inputFormat: 'json', showFiles: true, matching: 'lines'});
    diff2htmlUi.fileListCloseable('#line-by-line', false);
});
```

# Troubleshooting

### 1. Out of memory or Slow execution

#### Causes:
* Big files
* Big lines

#### Fix:
* Disable the line matching algorithm, by setting the option `{"matching": "none"}` when invoking diff2html

## Contributions

This is a developer friendly project, all the contributions are welcome.
To contribute just send a pull request with your changes following the guidelines described in `CONTRIBUTING.md`.
I will try to review them as soon as possible.

## License

Copyright 2014-2016 Rodrigo Fernandes. Released under the terms of the MIT license.

## Thanks

This project is inspired in [pretty-diff](https://github.com/scottgonzalez/pretty-diff) by [Scott González](https://github.com/scottgonzalez).

---
