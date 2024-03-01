This module provides a function and a command-line script that pretty-print
JSON strings with consecutive values aligned at the same column for improved
readability.

##Usage

In code (first do `npm install node-json-align`):

    JSON.stringifyAligned = require('node-json-align');

On the command line (first do `sudo npm install -g node-json-align`):

    node-json-align --help

The command-line script will output to stdout unless the `-i`/`--in-place`
option is given.

##Parameters

    JSON.stringifyAligned(obj, [replacer], [spaces], [alignAllValues])
    // or
    JSON.stringifyAligned(obj, alignAllValues, [spaces])

 - `replacer`: Like in `JSON.stringify`, this is a value transformation
   function, or an array of properties to serialize.
 - `spaces`: Like in `JSON.stringify`, a number of spaces (or string) to indent
   by (the default is 4)
 - `alignAllValues`: By default, a new alignment group will be started each
   time an array or object value is encountered.  If this option is set to
   `true`, then each object will have all of its values aligned together.

##Examples

```js
JSON.stringifyAligned({abc: 1, defgh: 2})
{
    "abc"   : 1,
    "defgh" : 2
}
```

```js
JSON.stringifyAligned({abc: 1, defgh: [2,3,4], ijk: 5})
{
    "abc"   : 1,
    "defgh" : [
        2,
        3,
        4
    ],
    "ijk" : 5   // Note that this value is not aligned with the first two,
                // since there is an array or object value before it.
}
```

```js
JSON.stringifyAligned({abc: 1, defgh: [2,3,4], ijk: 5}, null, 2, true)
{
  "abc"   : 1,
  "defgh" : [
    2,
    3,
    4
  ],
  "ijk"   : 5
}
```
