# Foi-Toy

This is an experimental tool for toying around with **Foi** code. It is **not** an official implementation of the **Foi** language.

## Status

Right now, all Foi-Toy does is tokenize a **Foi** file, and output syntax-highlighted HTML/CSS, with the optional `--color` CLI parameter.

All of this is subject to change at any time.

Example:

```java
///
this is an example of tokenizing a few
different literals (numbers/strings)
///

def a: -42.135;

def b: \h42a;  // this is a hex number

def c: "Hello, ""folks""!";
```

That code currently tokenizes as:

```js
[
  {
    type: 'COMMENT',
    value: '///\n' +
      'this is an example of tokenizing a few\n' +
      'different literals (numbers/strings)\n' +
      '///',
    start: 0,
    end: 82
  },
  { type: 'WHITESPACE', value: '\n\n', start: 83, end: 84 },
  { type: 'KEYWORD', value: 'def', start: 85, end: 87 },
  { type: 'WHITESPACE', value: ' ', start: 88, end: 88 },
  { type: 'GENERAL', value: 'a', start: 89, end: 89 },
  { type: 'COLON', value: ':', start: 90, end: 90 },
  { type: 'WHITESPACE', value: ' ', start: 91, end: 91 },
  { type: 'NUMBER', value: '-42.135', start: 92, end: 98 },
  { type: 'SEMICOLON', value: ';', start: 99, end: 99 },
  { type: 'WHITESPACE', value: '\n\n', start: 100, end: 101 },
  { type: 'KEYWORD', value: 'def', start: 102, end: 104 },
  { type: 'WHITESPACE', value: ' ', start: 105, end: 105 },
  { type: 'GENERAL', value: 'b', start: 106, end: 106 },
  { type: 'COLON', value: ':', start: 107, end: 107 },
  { type: 'WHITESPACE', value: ' ', start: 108, end: 108 },
  { type: 'ESCAPE', value: '\\h', start: 109, end: 110 },
  { type: 'NUMBER', value: '42a', start: 111, end: 113 },
  { type: 'SEMICOLON', value: ';', start: 114, end: 114 },
  { type: 'WHITESPACE', value: '  ', start: 115, end: 116 },
  {
    type: 'COMMENT',
    value: '// this is a hex number',
    start: 117,
    end: 139
  },
  { type: 'WHITESPACE', value: '\n\n', start: 140, end: 141 },
  { type: 'KEYWORD', value: 'def', start: 142, end: 144 },
  { type: 'WHITESPACE', value: ' ', start: 145, end: 145 },
  { type: 'GENERAL', value: 'c', start: 146, end: 146 },
  { type: 'COLON', value: ':', start: 147, end: 147 },
  { type: 'WHITESPACE', value: ' ', start: 148, end: 148 },
  { type: 'DOUBLE_QUOTE', value: '"', start: 149, end: 149 },
  { type: 'STRING', value: 'Hello, ', start: 150, end: 156 },
  { type: 'STRING_ESCAPED_CHAR', value: '""', start: 157, end: 158 },
  { type: 'STRING', value: 'folks', start: 159, end: 163 },
  { type: 'STRING_ESCAPED_CHAR', value: '""', start: 164, end: 165 },
  { type: 'STRING', value: '!', start: 166, end: 166 },
  { type: 'DOUBLE_QUOTE', value: '"', start: 167, end: 167 },
  { type: 'SEMICOLON', value: ';', start: 168, end: 168 }
]
```

If you include the `--color` parameter on the CLI command, the output will instead be the syntax-highlighted HTML/CSS, which (for the above code) looks like:

```html
<!-- ... -->

<i class="t0">///
this is an example of tokenizing a few
different literals (numbers/strings)
///</i>

<i class="t6">def</i> <i class="t1">a</i><i class="t6">:</i> <i class="t7">-42.135</i><i class="t6">;</i>

<i class="t6">def</i> <i class="t1">b</i><i class="t6">:</i> <i class="t3">\h</i><i class="t7">42a</i><i class="t6">;</i>  <i class="t0">// this is a hex number</i>

<i class="t6">def</i> <i class="t1">c</i><i class="t6">:</i> <i class="t0">"</i><i class="t2">Hello, </i><i class="t2">""</i><i class="t2">folks</i><i class="t2">""</i><i class="t2">!</i><i class="t0">"</i><i class="t6">;</i>

<!-- ... -->
```

That HTML/CSS looks like this when rendered in a browser:

<p>
<a href="foi-toy-highlighting.png" target="_blank"><img src="foi-toy-highlighting.png" width="500"></a>
</p>

As shown, the syntax highlighting currently only uses the [Monokai Pro](https://monokai.pro/) dark theme (with "Spectrum" filter) colors.

## To Use

Write **Foi** code and save it in a file -- generally with a `.foi` filename extension, but you can use whatever you like.

Then invoke `node cli.js --file={FILE-PATH}` with a path to the file you want to check. Foi-Toy will print out a list of tokens that were processed from the file.

The `--color` parameter optionally switches output to syntax highlighting (via HTML/CSS), which you can redirect to a `.html` file to view rendered in the browser.

## Tests

There are several test files provided in `./test/` that illustrate some of the syntactic edge cases for tokenizing **Foi** code, especially escaped number literals and escaped string literals (including interpolated string literals).

## License

[![License](https://img.shields.io/badge/license-MIT-a1356a)](LICENSE.txt)

All code and documentation are (c) 2022 Kyle Simpson and released under the [MIT License](http://getify.mit-license.org/). A copy of the MIT License [is also included](../LICENSE.txt).
