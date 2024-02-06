# CDL SplashGen
Generates metadata splash pages for PDFs in [eScholarship](https://escholarship.org/).

## Description
CDL Splashgen is a Java web application that runs as a service to make splash
pages for items in [eScholarship](https://escholarship.org/). It is built
using Maven and packaged as a WAR file.

## Build
To build the project:
```bash
mvn package
```
This will create a WAR file under target/ directory.

## Run
To run the application locally:
```bash
mvn jetty:run
```
This will start an embedded Jetty server, deploy the WAR file and start the web application.

Access the application at http://localhost:8080/

## Deploy
To deploy the WAR file to a standalone servlet container like Tomcat:

1. Stop Tomcat
2. Copy the WAR file from target/ to <Tomcat>/webapps/
3. Start Tomcat

## Documentation
work in progress, more soon

## Authors
[California Digital Library](https://cdlib.org/)

## License
[BSD 3-Clause](./LICENSE)
