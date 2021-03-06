[![GitHub license](https://img.shields.io/github/license/mashape/apistatus.svg)](https://github.com/mkozjak/node-telnet-client/blob/master/LICENSE)

[![NPM](https://nodei.co/npm/noogger.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/noogger/)
[![NPM](https://nodei.co/npm-dl/noogger.png?height=2)](https://nodei.co/npm/noogger/)

# Noogger (Node-logger)

A simple logging module for node.js

[![npm](https://img.shields.io/npm/dt/noogger.svg?label=npm%20downloads)](https://www.npmjs.com/package/noogger)
[![Build Status](https://travis-ci.org/websockets/ws.svg?branch=master)](https://travis-ci.org/websockets/ws)

`Noogger` is a simple featured logger module that helps you displaying logs to the console with log levels and pretty colors
 as well as writing logs files in a clean an organized way.
No need to implement the logging mechanism for your node applications anymore.


### Installing
Install it locally in your project or globally:
```
npm install noogger
npm install -g noogger
```

Please download from npm to get the latest stable version.

## Features

-  write daily log file, handy for servers, or applications that run continously
-  Forwards(prints) logging data to the console output if needed (optional)
-  En/Disable Console output with respect to log levels 
-  En/Disable File output with respect to log levels 
-  pretty colors in console output
-  Supported log levels (as per cisco and many other manufacturer standards):
	EMERGENCY(0)
	ALERT(1)
	CRITICAL(2)
	ERROR(3)
	WARNING(4)
	NOTICE(5)
	INFO(6)
	DEBUG(7)
-  Customize date-time format for log lines and for log file name

## Usage

#### Basic (with default parameters)

```js
var log = require('noogger');
...
...
log.emergency("This is an EMERGENCY!!! THE WORLD IS COLLAPSING");
log.alert("OMGGGG!");
log.critical("This is getting critical!");
log.error("Erro 0x04512 Failed to initialize the initialization module");
log.warning("something is wrong");
log.notice("Hey! have you noticed This?!");
log.info("Hello World! Booting..");
log.debug("something Happened!");

```
The log file will look like this
```
28-04-2016 20:16:45.5 [WARNING] something is wrong
28-04-2016 20:16:45.5 [ERROR] Failed to initialize the...
28-04-2016 20:16:45.5 [DEBUG] something Happened!
28-04-2016 20:17:06.6 [ERROR] telnet socket closed
```

#### With custom options

```js
var logParams = {
	consoleOutput : true,
	consoleOutputLevel: ['DEBUG','ERROR','WARNING'],
	
	dateTimeFormat: "DD-MM-YYYY HH:mm:ss.S",
	outputPath: "logs/",
	fileNameDateFormat: "DDMMYYYY",
	fileNamePrefix:"myApp-"
};

var log = require('noogger').init(logParams);

```
or
```js
var log = require('noogger');

var logParams = {
	consoleOutput : true,
	consoleOutputLevel:'DEBUG',
	
	dateTimeFormat: "DD-MM-YYYY HH:mm:ss",
	fileNameDateFormat: "YYYY-MM-DD",
	fileNamePrefix:"myApp-",
	outputPath: "myLogs/"
};


log.init(logParams);
```

## Default Parameters: 
```
	consoleOutput : true,
	consoleOutputLevel: 7, 
	
	fileOutput: true,
	fileOutputLevel: 7, 
	
	outputPath: "logs/",
	fileNameDateFormat: "DDMMYYYY",
	dateTimeFormat: "DD-MM-YYYY HH:mm:ss.S",
	
	fileNamePrefix:"",
	fileNameSuffix:"",
	customIntro: null
```

## Parameters: 
-  	`consoleOutput` : `boolean` : Wether the logs should be printed on the console output as well, or not
-  	`consoleOutputLevel` : `int` or `string` or `array`  : Filters what is printed to the console with respect to log levels (specify the console output log level).
   	using int: from 0 to 7 
  	using string: any valid log level (DEBUG, INFO, ERROR,....)
  	using array: to allow to select multiple log levels without the constraint of order  eg: ['DEBUG','ERROR','WARNING']
-  	`fileOutput` : `boolean` : Wether the logs should be written to files or not
-  	`consoleOutputLevel` : `int` or `string` or `array`  : Filters what is written to log files with respect to log levels (works the same as consoleOutputLevel).
-  	`outputPath` : `string` : define the location where the log files  will be written
-  	`dateTimeFormat` : `string` : specifies the Date and time format to be used inside log file for each record.
                             refer to the date format section.
-  	`fileNameDateFormat`: `string` : the date format to be used in the log files name to differentiate them (per day); 
                               you can alter this, so that it will write one file per week or month or whatever you want,
                               refer to the date format section.
-  	`fileNamePrefix`: `string` : Prepends the given string to every log file name.
-  	`fileNameSuffix`: `string` : Appends the given string to every log file name.
-  	`customIntro`: `function` or `boolean` : Just. try it by stting it to true :) or supply your own function to be called when your application starts(at least at the point where you initialize noogger)


## Date and Time formatting

The formating is based on the moment.js library, since it is the one used.
So please refer to [this page][1].

Submit any issue or request to the [github page][2].

[1]: http://momentjs.com/docs/#/displaying/format/
[2]: https://github.com/Xsmael/node-logger/issues
