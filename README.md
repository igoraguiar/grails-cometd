# Grails Cometd Plugin

[CometD](http://cometd.org) is a scalable HTTP-based event routing bus that uses an Ajax Push technology pattern known as [Comet](http://en.wikipedia.org/wiki/Comet_(programming\)).  This plugin allows your Grails application to push asynchronous notifications to HTTP clients using CometD and the [Bayeux](http://cometd.org/documentation/bayeux) protocol.

## Installation
NOTE: Because of a bug this won't work in grails 1.3.2 (fixed in 1.3.3):

	grails install-plugin cometd
	
You can always download the [source](http://github.com/marcusb/grails-cometd) and then from the plugin directory:

	grails package-plugin
	
And then from your application directory:

	grails install-plugin /path/to/grails-cometd-plugin-zip-file

## Usage

### CometD Servlet
***

The plugin configures a CometdServlet, mapped to the path cometd relative to your web application's context path.

### Bayeux Service
***

A bean named bayeux is made available to your application. It is an instance of [BayeuxServer](http://download.cometd.org/bayeux-api-2.0.beta0-javadoc/org/cometd/bayeux/server/BayeuxServer.html). This is used to interact with the Comet server.

### Configuration
***

The plugin is configured in Config.groovy, with options prefixed with "plugins.cometd". The following options are defined:

* **plugins.cometd.continuationFilter.disable**: if set, do not install the to [ContinuationFilter](http://download.eclipse.org/jetty/stable-7/apidocs/org/eclipse/jetty/continuation/ContinuationFilter.html)
* **plugins.cometd.init.params**: a map of init-name -> init-value pairs for an init-param element to be applied to the cometd servlet definition. Make sure you read the javadoc for org.cometd.bayeux.server.ServerTransport for how the init params are applied. Some useful settings include:
	* **timeout**: In the default long polling http transport is the period of time the server waits before answering to a long poll
	* **interval**: In the default long polling http transport is the period of time that the client waits between long polls
	* **maxInterval**: In the default long polling http transport is the period of time that must elapse before the server consider the client being lost

## Contributing
Contributions are welcome, preferably by pull request on GitHub
	
	git clone git://github.com/marcusb/grails-cometd.git

## History

### Version 0.2.1
***
* Install the [ContinuationFilter](http://download.eclipse.org/jetty/stable-7/apidocs/org/eclipse/jetty/continuation/ContinuationFilter.html) by default, it is needed for Tomcat 6

### Version 0.2
***
* Rewritten from scratch for CometD 2.0