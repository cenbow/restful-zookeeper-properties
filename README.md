[![Build Status](https://travis-ci.org/pnerg/restful-zookeeper-properties.svg?branch=master)](https://travis-ci.org/pnerg/restful-zookeeper-properties) [![codecov.io](https://codecov.io/github/pnerg/restful-zookeeper-properties/coverage.svg?branch=master)](https://codecov.io/github/pnerg/restful-zookeeper-properties?branch=master)

# RESTful ZooKeeper Properties
Provides a RESTful JSON interface to a property based zookeeper data model.    
This project adds a HTTP based RESTful interface on top of the project [ZooKeeper Properties](https://github.com/pnerg/zookeeper-properties)

![Overview](https://github.com/pnerg/restful-zookeeper-properties/blob/master/src/main/javadoc/doc-files/overview.png)

The purpose is to allow for easy access to view/change properties using non-programmatic tools such as [wget](https://www.gnu.org/software/wget/) and [curl](http://man.cx/curl)

The above figure depicts a setup where there are a number of _micro services_, in an essence stand-alone processes performing some task. A typical problem in a _micro services_ architecture is to configure each individual service. Not only are the services potentially distributed over a number of hosts, there's most likley going to be multiple instances of each service. 
The common pattern is to use a centralized database for storage, of which [ZooKeeper](https://zookeeper.apache.org/) is very popular.  

The project [ZooKeeper Properties](https://github.com/pnerg/zookeeper-properties) provides the API the application/service needs to read property/configuration data.  
For details on data model and usage of the persistence layer refer to the above referred project. 

This project focuses on adding a simple way to manage the properties/configuration.  
That is without needing to perform programmatic tasks.  
Quite often the administrator needing to setup/maintain the system is not a programmer, rather a script hacker.  
This person only wants to be able to set/read/delete property data using scripting tools or possible a web browser.  
Therefore this project provides a simple RESTful interface allowing for easy manipulation of the property data using tools such as [curl](http://man.cx/curl).

## The API
There's four basic uses cases which are described in the sections to come.  

### List all property sets
Performing a _GET_ on the URL:
```
[uri]/properties
```  
Will yield a json formated list with all the names of the existing property sets.
E.g.  
```json
["system"]
```
### List all properties for a single property set
Performing a _GET_ on the URL:
```
[uri]/properties/set-name
```  
Will yield a json formated list with all the name/value pairs of the properties for the set with the name _set-name_.  
E.g.  
```json
{"port": "6969","host": "127.0.0.1"}
```
or with pretty-print  
```json
{
"port": "6969",
"host": "127.0.0.1"
}
```
### Set properties for a single property set
Performing a _PUT_ on the URL:
```
[uri]/properties/set-name
```  
With the data such as :
```json
{"port": "6969","host": "127.0.0.1"}
```
Will set the properties for the set with the name _set-name_.  
Note any existing set with the same name will be overwritten.  
It's also important that the _Content-Type_ is set to _application/json_
### Delete a property set
Performing a _DELETE_ on the URL:
```
[uri]/properties/set-name
```  
Will delete the set with the name _set-name_.  

## LICENSE

Copyright 2016 Peter Nerg.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

<http://www.apache.org/licenses/LICENSE-2.0>

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
