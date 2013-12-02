# thehelp-project

This project is designed to get a high quality grunt-based project automation setup in place very quickly.

## Features

Grunt task setup:

* time-grunt
* env (using env.json)
* mocha-cli for 'unit', 'integration' and 'interactive' tasks, running everything underneath 'test/<test type>' excluding the 'client' subdirectory
* command-line options supported for tests: 'grep', 'coverage', 'reporter' and 'bail'
* staticanalysis, encompassing two tasks: jshint and complexity
* doc, wrapping two tasks: groc and fix-groc-stylesheet
* watch core setup and subtasks for tests, static analysis and documentation generation
* `modifiedInLast()` method to filter files processed using the grunt 'partial' command-line option
* clean, deleting public/*, tmp/* by default, and extended to include files under doc if you call `registerDoc()`

## Jump in!

### Install

Include the project in your dependencies:

```
  "thehelp-project": "git+ssh://git@infra:thehelp-project#v1.0.0"
```

### Usage

To get up and running very quickly with all defaults, just put this in your Gruntfile:

```
var GruntConfig = require('thehelp-project').GruntConfig;
var config = new GruntConfig(grunt);
config.standardSetup();
config.standardDefault();
```

## History

### 2.1.0

* new: task 'test-all' for easy code coverage testing

### 2.0.0

* `registerCopy()` now takes options param, not files
* `registerCopyFromDist()` now creates just one target
* new: `registerInstall()` for 'npm/bower install'
* new: 'setup' task for installing dependencies

### 1.4.1

* can use `bowerSpecialCases` to customize the behavior of `registerCopyFromBower()`. two special-cases are included by default: lodash (dist/lodash.compat.js) and requirejs (require.js)

### 1.4.0

* new method: `registerCopyFromBower()` - pulls javascript files installed by bower into your lib/vendor directory
* `registerCopy()` can be called more than once; also called by `registerCopyFromBower()` and `registerCopyFromDist` to ensure `grunt-contrib-copy` task is ready for use
* dependency update: latest versions of lodash, grunt-contrib-jshint, grunt-mocha, time-grunt, and grunt

### 1.3.0

* registerTest: now allows customization of source files to ensure that your 'run-on-change' task behaves properly

### 1.2.3

* Re-ordering parameters in registerStaticAnalysis (now it's files first, then jshintrc path)

### 1.2.2

* Fix to registerOptimize: fix task name collision for multiple libraries based off of the same root javascript file

### 1.2.1

* Fix to registerOptimize: allow multiple libraries based off of the same root javascript file (take name for task from the output file, not the input file)

### 1.2.0

* new method: `registerCopyFromDist()` - pulls files out of `dist/` folders of installed node modules
* `registerCopy()` files parameter now optional

### 1.1.0

* new method: `registerCopy()` - pulls in `grunt-contrib-copy` task, passes `files` parameter to it
* new method: `registerConnect()` - sets up two targets: test (port 3001) and keepalive (port 3000)
* new method: `registerOptimize()` - uses `grunt-requirejs` to optimize and concatenate AMD files, producing unoptimized and, if requested, standalone files based on almond.js
* new method: `registerMocha()` - running phantomjs-based in-browser unit tests. Works well with `registerConnect()`

### 1.0.3

* adding 'dist' target to  `registerClean()`

### 1.0.2

* `registerStaticAnalysis()` uses .jshintrc file inside this project by default, to make it that much easier to set up a new project.

### 1.0.1

* new: `loadLocalNpm()` loads tasks from node modules installed as dependencies of this library, not from the project which is using this library.

### 1.0.0

* Initial release
* time-grunt, env, testing with mocha-cli, jshint, complexity, groc and fix-groc-stylesheet, clean, watch, filter, code coverage support in testing,


## License

(The MIT License)

Copyright (c) 2013 Scott Nonnenberg &lt;scott@nonnenberg.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
