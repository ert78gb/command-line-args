[![view on npm](http://img.shields.io/npm/v/command-line-args.svg)](https://www.npmjs.org/package/command-line-args)
[![npm module downloads per month](http://img.shields.io/npm/dm/command-line-args.svg)](https://www.npmjs.org/package/command-line-args)
[![Build Status](https://travis-ci.org/75lb/command-line-args.svg?branch=master)](https://travis-ci.org/75lb/command-line-args)
[![Dependency Status](https://david-dm.org/75lb/command-line-args.svg)](https://david-dm.org/75lb/command-line-args)

**work in progress, draft documentation**

#command-line-args
A command-line parser and usage-guide producer.. Particularly good at organising large sets of options. 

##Install
```sh
$ npm install command-line-args --save
```

##Synopsis
this `app.js`: 
```js
var cliArgs = require("command-line-args");

/* define the command-line options */
var cli = cliArgs([
    { name: "verbose", type: Boolean, alias: "v", description: "Write plenty output" },
    { name: "help", type: Boolean, description: "Print usage instructions" },
    { name: "files", type: Array, defaultOption: true, description: "The input files" }
]);

/* parse the supplied command-line values */
var options = cli.parse();

/* generate a usage guide */
var usage = cli.usage({
    header: "A synopsis application.",
    footer: "For more information, visit http://example.com"
});
    
console.log(options.help ? usage : options);
```
results in this output at the command line:
```sh
$ node app.js
{}
$ node app.js -v
{ verbose: true }
$ node app.js README.md package.json
{ files: [ 'README.md', 'package.json' ] }
$ node app.js README.md package.json -v
{ verbose: true, files: [ 'README.md', 'package.json' ] }
$ node app.js --help

  A synopsis application.

  Usage

  -v, --verbose    Write plenty output
  --help           Print usage instructions
  --files <array>  The input files

  For more information, visit http://example.com

```

#API Reference
<a name="module_command-line-args"></a>
##command-line-args(options)
Command-line parser, usage-guide producer.


- options `Array.<module:command-line-args~OptionDefinition>` - list of option definitions

  
####Example
```js
var cliArgs = require("command-line-args");
var cli = cliArgs([
    { name: "help", type: Boolean, alias: "h" },
    { name: "files", type: Array, defaultOption: true}
]);
var argv = cli.parse();
```
<a name="module_command-line-args#parse"></a>
###cli.parse([argv])

- [argv] `object` - Optional argv array, pass to override `process.argv`.

<a name="module_command-line-args#usage"></a>
###cli.usage(data)

- data `object` - options for template

<a name="module_command-line-args.OptionDefinition"></a>
###type: OptionDefinition

Defines an option

**Scope**: inner typedef of [command-line-args](#module_command-line-args)  
**Type**: `object`  
<a name=""></a>
###name
the option name

**Type**: `string`  
<a name=""></a>
###type
an optional type contructor function

**Type**: `function`  
