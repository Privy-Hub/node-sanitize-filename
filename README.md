# sanitize-filename

[![build
status](https://secure.travis-ci.org/parshap/node-sanitize-filename.svg?branch=master)](http://travis-ci.org/parshap/node-sanitize-filename)

Sanitize a string to be safe for use as a file name in Windows and Unix
systems by stripping all [control
characters](http://en.wikipedia.org/wiki/C0_and_C1_control_codes) and
restricted characters (`\/:*?"<>|`).

## Usage

```js
// Some string that may be unsafe as a filesystem filename
var UNSAFE_FILENAME = "h*ello:/world?\u0000";

// Sanitize the unsafe filename to be safe for use as a filename
var sanitize = require("sanitize-filename"),
	filename = sanitize(UNSAFE_FILENAME);

// Create a file using the safe filename
require("fs").createWriteStream(filename).end();
```

### Unique filenames

Note that two unique inputs can result in the same output. For example,
`sanitize("file?")` and `sanitize("file*")` will both return `"file"`.

### Empty filenames

Note that the return value can be an empty string. For example,
`sanitize("><")` will return `""`. To avoid this, use a default value
(e.g., `sanitize("><") || "default"`) or `options.replacement`.

## API

### sanitize(filename, [options])

Sanitize the input string, `filename`, removing or replacing unsafe
characters. The `options.replacement` can be a string to replace unsafe
characters with.

## Installation

```
npm install sanitize-filename
```
