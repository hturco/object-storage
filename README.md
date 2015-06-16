# object-storage [![NPM version](https://badge.fury.io/js/openstack-storage.png)](http://badge.fury.io/js/openstack-storage)
A node.js client library for interacting with Object Storage (Swift)

_Copyright 2012, FeedHenry Ltd. Licensed under the
MIT license, please see the LICENSE file.  All rights reserved._

## Installation
    npm install object-storage

## Example usage 1
    var async = require('async');
    var storage = require('storage');
    
    ## get an authentication function. config formats are described in lib/authenticate.js
    ## use one of these:
    var authFn = async.apply(storage.authenticate.getTokensNative, config); // for native auth (swauth or tempauth)
    var authFn = async.apply(storage.authenticate.getTokensKeystone, config); // option for keystone auth

    var storageSwift = new storage.ObjectStorage (authFn, function(err, res, tokens) {
      console.log('Storage constructor - err: ', err, ', tokens: ', tokens);
      var containers = storageSwift.getContainers(function(err, containers) {
        console.log('getCOntainers - err: ', err, ', containers: ', containers);
        // containers is an array of objects [{name: "Name1"...}, ...]
      });
    });

## Example usage 2
    // Create a container called "EngTest"
    storageSwift.createContainer("EngTest", function (err, statusCode) {});
    
    // upload a local file test.png to a container called "EngTest" naming the remote file: file1.png 
    storageSwift.putFile("EngTest", {remoteName:'file1.png', localFile:'./test.png'}, function(err, statusCode) {});
    
    // delete a remote file: file1.png from a container called "EngTest"
    storageSwift.deleteFile("EngTest", 'file1.png', function (err, statusCode) {})
    
    // delete a container
    storageSwift.deleteContainer("EngTest", function (err, statusCode) {});

See the `examples` folder for more sample API usage.



