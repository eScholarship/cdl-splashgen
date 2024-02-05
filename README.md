# CDL SplashGen

This is a simple Java web application built using Maven and packaged as a WAR file.

## Description
Provide a brief description of what the project does.

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

The application will be available at http://<host>:<port>/${war-name}/

## Documentation
Provide links to any documentation - Javadocs, general documentation etc.

## Authors
Name of author(s)

## License
Open source license if applicable.
