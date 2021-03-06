# grunt-jsbeautifier [![Gittip](http://img.shields.io/gittip/vkadam.png)](https://www.gittip.com/vkadam/) [![Build Status](https://travis-ci.org/vkadam/grunt-jsbeautifier.png)](https://travis-ci.org/vkadam/grunt-jsbeautifier) [![NPM](https://nodei.co/npm/grunt-jsbeautifier.png?downloads=true&stars=true)](https://npmjs.org/package/grunt-jsbeautifier)

[jsbeautifier.org](http://jsbeautifier.org/) for grunt

## Getting Started
This plugin recommends using Grunt `~0.4.1`. Grunt `~0.3.0` is only suported till version 0.1.4

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

### Grunt `~0.4.1`
```
npm install grunt-jsbeautifier --save-dev
```

One the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```
grunt.loadNpmTasks('grunt-jsbeautifier');
```

### Grunt `~0.3.0`
Install this grunt plugin next to your project's [grunt.js gruntfile][getting_started] with:

```
npm install grunt-jsbeautifier@0.1.4
```

Then add this line to your project's `grunt.js` gruntfile:

```
grunt.loadNpmTasks('grunt-jsbeautifier');
```

[grunt]: http://gruntjs.com/
[getting_started]: https://github.com/gruntjs/grunt/blob/master/docs/getting_started.md

## Examples

### Single Task
  - files (required): Your source files to beautify
  - options (optional): Overwrite default jsbeautifier options

```javascript
"jsbeautifier" : {
    files : ["src/**/*.js"],
    options : {
    }
}
```

### Multi Task
  - src (required): Your source files to beautify
  - options (optional): Overwrite default jsbeautifier options

```javascript
"jsbeautifier" : {
    "default": {
        src : ["src/**/*.js"]
    },
    "git-pre-commit": {
        src : ["src/**/*.js"],
        options : {
            mode:"VERIFY_ONLY"
        }
    }
}
```

## Config

#### files
Type: `Files`
Default value: `[]`

List of files to be beautified. This option is applicable only for **Single Task**

#### src
Type: `Files`
Default value: `[]`

List of files to be beautified. This option is applicable only for **Multi Task**

#### options.mode (optional)
Type: `String`
Default value: `VERIFY_AND_WRITE`

If mode is "VERIFY_ONLY", then task will fail if at least one file can be beautified. This is useful for pre-commit check.

#### options.dest (optional)
Type: `String`
Default value: `''`

All beautified file will be stored under "dest".

#### options.jsbeautifyrc (optional)
Type: `String` or `true`
Default value: `null`

_Alias:_ options.config (for version < 0.2.7)

If set to `true`, config will be sent to [jsbeautify](https://github.com/einars/js-beautify#options) from `.jsbeautifyrc` files relative to the flies being beautified.

If a filename is specified, options and globals defined therein will be used. The `jsbeautifyrc` file must be valid JSON and looks like the one supported by js-beautify itself.

### Default options from [js-beautify](https://github.com/einars/js-beautify#options) can be used
```javascript
  "jsbeautifier": {
      files: ["src/**/*.js"],
      options: {
          config: "path/to/configFile",
          html: {
              braceStyle: "collapse",
              indentChar: " ",
              indentScripts: "keep",
              indentSize: 4,
              maxPreserveNewlines: 10,
              preserveNewlines: true,
              unformatted: ["a", "sub", "sup", "b", "i", "u"],
              wrapLineLength: 0
          },
          css: {
              indentChar: " ",
              indentSize: 4
          },
          js: {
              braceStyle: "collapse",
              breakChainedMethods: false,
              e4x: false,
              evalCode: false,
              indentChar: " ",
              indentLevel: 0,
              indentSize: 4,
              indentWithTabs: false,
              jslintHappy: false,
              keepArrayIndentation: false,
              keepFunctionIndentation: false,
              maxPreserveNewlines: 10,
              preserveNewlines: true,
              spaceBeforeConditional: true,
              spaceInParen: false,
              unescapeStrings: false,
              wrapLineLength: 0
          }
      }
  },
```
Only specifiy options to overwrite.

**NOTE:** All options can be specified similar to [js-beautify](https://github.com/einars/js-beautify#options) using underscore.


### FAQ/Tips
#### 1. Exclude files
All files from foo folder except bar.js
```javascript
jsbeautifier: {
    files: ['foo/*.js', '!foo/bar.js']
}
```
#### 2. Use specific version of js-beautify
If you want use specific version of js-beautify instead of latest, please refer to [npm shrinkwrap](https://npmjs.org/doc/shrinkwrap.html)

#### 3. Beautify files other than js, json, css & html
If you need to beautify files other than js, json, css & html, it can be done by passing **fileTypes**.

For example, beautifying **'.js.erb'** files **along with '.js'**, beautifying **'.less'** files **along with '.css'**, beautifying **'.html.erb'** files **along with '.html'**.
```
jsbeautifier: {
    files: ['foo/css/*.css', 'bar/css/*.less', 'foo/js/*.js', 'bar/js/*.js.erb', 'foo/html/*.html', 'bar/html/*.html.erb'],
    options: {
        js: {
            fileTypes: ['.js.erb']
        },
        css: {
            fileTypes: ['.less']
        },
        html: {
            fileTypes: ['.html.erb']
        }
    }
}
```

## Release History
* 0.2.6: Bumped version after for changing dist to dest
* 0.2.5: Support dist folder and show all failed files in VERIFY_MODE [22](https://github.com/vkadam/grunt-jsbeautifier/issues/22), [24](https://github.com/vkadam/grunt-jsbeautifier/issues/24), [25](https://github.com/vkadam/grunt-jsbeautifier/issues/25)
* 0.2.4: Support custom file types other than js, json, css & html. Use latest versions for dependencies [23](https://github.com/vkadam/grunt-jsbeautifier/issues/23), [26](https://github.com/vkadam/grunt-jsbeautifier/issues/26)
* 0.2.3: Always use latest version of js-beautify. [21](https://github.com/vkadam/grunt-jsbeautifier/issues/21)
* 0.2.2: Configuration is now lint happy. Options can be specified in cameCase, [17](https://github.com/vkadam/grunt-jsbeautifier/issues/17)
* 0.2.1: Added Support for flat config file
* 0.2.0: Added support for css, html and json files
* 0.1.10: Added verify only mode [15](https://github.com/vkadam/grunt-jsbeautifier/issues/15). This will fail if any file needs beautification.
* 0.1.9: Upgraded [js-beautify](https://npmjs.org/package/js-beautify) to 1.4.0. Fixed issues [13](https://github.com/vkadam/grunt-jsbeautifier/issues/13)
* 0.1.8: Upgraded [js-beautify](https://npmjs.org/package/js-beautify) to ~1.3.1. Fixed issues [10](https://github.com/vkadam/grunt-jsbeautifier/issues/10), [12](https://github.com/vkadam/grunt-jsbeautifier/issues/12)
* 0.1.7: Upgraded grunt to ~0.4.1, [js-beautify](https://npmjs.org/package/js-beautify) to ~1.2.0. Fixed issues [6](https://github.com/vkadam/grunt-jsbeautifier/issues/6), [7](https://github.com/vkadam/grunt-jsbeautifier/issues/7), [8](https://github.com/vkadam/grunt-jsbeautifier/issues/8), [9](https://github.com/vkadam/grunt-jsbeautifier/issues/9)
* 0.1.6: Make sure new line at the end of file. Fixed issue [5](https://github.com/vkadam/grunt-jsbeautifier/issues/5)
* 0.1.5: Upgraded to grunt ~0.4.0. Fixed issues [2](https://github.com/vkadam/grunt-jsbeautifier/issues/2), [3](https://github.com/vkadam/grunt-jsbeautifier/issues/3), [4](https://github.com/vkadam/grunt-jsbeautifier/issues/4)
* 0.1.4: Upgraded [js-beautify](https://npmjs.org/package/js-beautify) to latest version (0.3.2)
* 0.1.3: Added fix for block comment formatting.
* 0.1.2: Supported grunt 0.4~.
* 0.1.1: Readme file changes
* 0.1.0: Initial version.

## License
Copyright (c) 2012 Vishal Kadam
Licensed under the MIT license.
