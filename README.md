# Moving on to TypeScript
This project has been converted to TypeScript, please see [breeze-odata4](https://github.com/tschettler/breeze-odata4) for the TypeScript version of this adapter that I'm currently working on.

# BreezeJS OData v4 Adapter

This is an experimental adapter to allow [BreezeJS](http://www.getbreezenow.com/) to communicate with a server that is using version 4 of the OData protocol.

## Background

The current adapter for OData is designed to work with up to version 3 of the OData protocol. I am currently working of an application that requires me to communicate with a server using OData v4.
At the same time I want to use Breeze, but with no official OData v4 adapter, I'm attempting to write my own.

I am using the [Olingo OData client](http://olingo.apache.org/doc/javascript/index.html), which is the v4 successor to the [datajs](http://datajs.codeplex.com/) library that is currently used by Breeze (and only supports up to v3).

## Caveat

This is *not* ready for production use by a long, long way. I have basically taken the [built in OData adapter](https://github.com/Breeze/breeze.js/blob/master/src/b00_breeze.dataService.odata.js)
and started modifying it to try to bring it in line with the v4 spec. I am by no means an expert and also I have paid no attention to clean code. This is just a hack right now. If it turns
out to be usable I will clean it up some.

## Usage

If you are brave and want to give it a go, I have written it in such a way that you do not need to re-build Breeze to use it.

Include the JavaScript files in the following order:

1. odatajs-4.0.0.js*
2. breeze.js
3. breezeOdataV4Adapter.js

Then in your app, configure Breeze to use this adapter:

```JavaScript
breeze.config.initializeAdapterInstance('dataService', 'ODataV4', true);
```

The adapter also assumes that promises are available either because AngularJS has been included or the window.Q object exists.

\* I have also updated this library with an IIFE at the end since the require global was being overwritten.

## Progress

So far, in my limited testing, I have the following features working:
- Metadata
- Queries (`breeze.EntityQuery()`) with filtering (`where()`) and eager loading (`expand()`)
- Batch inserts/updates/deletes (`entityManager.saveChanges()`)

But I have not tested these widely - my app is in its very early stages so there are probably many cases that will not work as expected.

## Contribution

Ideally the Breeze guys will come out with an official adapter, but failing that, I hope to bring this one to a production-ready state. I have no
experience building anything like this, so I welcome input from anybody who is interested in using Breeze with OData v4 and may have some advice to offer, or even bug reports
on using what I have put together here.

Useful links if you want to contribute:

- The current [Breeze OData adapter source](https://github.com/Breeze/breeze.js/blob/master/src/b00_breeze.dataService.odata.js)
- [OData v4 spec](http://www.odata.org/documentation/odata-version-4-0/)
- [Olingo OData Client for JavaScript](http://olingo.apache.org/doc/javascript/index.html)
