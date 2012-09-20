Luracast Restler 3.0 Sp1
========================

Restler is a simple and effective multi-protocol REST API Server written in PHP. 
Just deal with your business logic in php, restler will take care of the REST!

### Restler 3 - *Better APIs by Design*

* [Developer Home](http://luracast.com/products/restler/)
* Updates on [Facebook](https://www.facebook.com/Luracast) and [Twitter](http://twitter.com/Luracast)

Features
--------

* No Learning Curve
* Light weight
* Flexible
* Highly Customizable
* Many Examples that can be tried on your localhost to get started
* Supports HTTP request methods  GET, POST, PUT, DELETE, and PATCH
* Supports both RESTful and Pragmatic REST API Design
* Clients can use X-HTTP-Method-Override header
* Two way format(media type) conversion
    * Pluggable Formatters
    * Comes with JSON, XML, Yaml, Amf, and Plist(both XML and Binary) formats
* Pluggable Authentication schemes
    * `[planned]` OAuth 2
* Pluggable Filters to effectively manage API usage
    * `[planned]` API Rate Limiting Filter
* Routing
    * Manual Routing
        * Using `@url GET my/custom/url/{param}` PHPDoc comments
    * Auto Routing
        * URL to Method mapping
        * URL part to Method parameter mapping
        * Query parameters to Method parameter mapping
        * Request body to Method parameter mapping
        * `[planned]` Header to Method parameter mapping
* Cache support
    * Client Side Caching support
    * Proxy Caching support
    * Server Side Caching
        * `[planned]` ETag, If-None-Match support
        * `[planned]` Last-Modified, If-Modified-Since support
* API Design
    * Always supports URLEncoded format for simplified input (POST vars)
    * Automatic parameter validation and type conversion
    * API versioning support by URL and/or vendor specific MIME
    * API documentation and discovery using [Restler API Explorer](https://github.com/Luracast/Restler-API-Explorer)
    * API throttling
* Management
    * `[planned]` Unit Testing using [PHPUnit](https://github.com/sebastianbergmann/phpunit/)
    * Behaviour Driven API testing using [Behat](http://behat.org/) and [Guzzle](https://github.com/guzzle/guzzle)
    * Commandline Project Management using [Respect/Foundation](https://github.com/Respect/Foundation)
    * Dependency Management using [Composer](http://getcomposer.org/)
    * Source code distributed under LGPL

Installation
------------
Installation is a two step process. Do the following in the folder where you want Restler to be setup

1. [Download](https://github.com/Luracast/Restler/zipball/v3) and unpack Restler 3, or Checkout using Terminal/Commandline

```
git clone git://github.com/Luracast/Restler.git -b v3 ./
```

2. Download the dependencies using make. Using Terminal/Commandline

```
make composer-install
```

Now the vendor folder will have all dependencies.


Changes from Restler 2.0
------------------------

**Restler 3.0** is completly rewriten from Restler 2.0 with best practices in mind for

* PHP Coding
* RESTfulness and/or Pragmatic REST
* API Design

**Restler 3.0**

* uses namespaces, Late Static Bindings, and Closures and thus it is **PHP 5.3+** only
  (if you need **PHP 5.0+** support use [Restler 2](https://github.com/Luracast/Restler/tree/v2))
* provides backword compatibility for Restler 1 and 2.
    Use `$r->setCompatibilityMode($version);`
* supports hybrid api which provides extended data to authenticated users
  Use `@access hybrid` PHPDoc comment
* uses smart auto routing by default where API method parameters that
  have default values are no longer mapped to the URL, instead they are
  mapped to query strings to reduce ambiquity in the url.
* supports `suppress_response_codes` as query string, when set to true;
  all http responses will be returned with HTTP OK with the errors in the
  body to accomodate mobile and less privilaged clients.
* has improved `CommentParser` which adds support for embeded data in multiple formats
    * inline doc comments `{@name value}`
    * querystring params \`\`\` param1=value&param2=value2\`\`\`
    * json \`\`\` {"parm1": value, "param2": value2}\`\`\` which can be placed in multi-lines
* has `Defaults` class with static properties that can be changed to suit the needs
* ...(more to follow)

Changes from Restler 1.0
------------------------

Restler 2.0 is a major rewrite to use convention over configuration and it is optimized 
for performance. Here are some of the major changes and improvements

* PHPDoc comments to map a method to URI are now optional.
* All public methods that does not begin with an underscore are mapped
  automatically to the method name (`gateway\classname\methodname\param1\...`)
* If we do not specify the second parameter for `$restler->addAPIClass` it will be mapped to the
  class name instead of mapping it to the root
* Restler 2 is written for PHP 5.3 and above but it make use of compat.php and work on
  any version of PHP starting from PHP 5.0