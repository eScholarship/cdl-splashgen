# CDL SplashGen
Generates metadata splash pages for PDFs in [eScholarship](https://escholarship.org/).

## Description
CDL Splashgen is a Java web application that runs as a service to make splash
pages for items in [eScholarship](https://escholarship.org/). It is built
using Maven and packaged as a WAR file.

## Build
To build the project:
```bash
mvn clean package
```
This will create a WAR file under target/ directory.

## Run
To run the application locally:
```bash
mvn jetty:run
```
This will start an embedded Jetty server, deploy the WAR file and start the web application.

Access the application at http://localhost:8080/

## Deploy (generic instructions)
To deploy the WAR file to a standalone servlet container like Tomcat:

1. Stop Tomcat
2. Copy the WAR file from target/ to <Tomcat>/webapps/
3. Start Tomcat

## Deploy on CDL servers

```bash
mvn clean package
eye restart tomcat
# wait about a minute, then confirm it restarted with
eye info tomcat
tomcat ............................ up  (01:01, 0%, 2106Mb, <14558>)
```

## Assumptions
The SplashGen service hard codes the paths to the fonts it wants to use.
Wherever you're running this service, you'll need to ensure that the following
paths exist:

```
/usr/share/fonts/dejavu/DejaVuSans.ttf
/usr/share/fonts/dejavu/DejaVuSans-Bold.ttf
/usr/share/fonts/Code2000.ttf
```

## Usage

The SplashGen service accepts POST requests with JSON data containing:

* Input PDF
* Splash page PDF template
* Output path
* JSON instructions for splash page content

When such a POST request is received, SplashGen will generate a new PDF with the
splash page merged, and write it to the provided output path (if the path exixts
and the service has permissions to write to that locaion, of course).

### Endpoints
* POST /splashgen - Main endpoint to generate splash page
* GET /splashgen - Healthcheck endpoint

### Examples
The utils folder of this project contains a Ruby script,
[splashGen.rb](utils/splashGen.rb), which is used by the eScholarship Controller
to add splash pages to items in eScholarship, upon submission. As such, it is a
good example of how to use the SplashGen service.

If you are running SplashGen locally, perhaps with the ebmedded Jetty server:

```bash
mvn jetty:run
```

You can interact with the SplashGen service with Curl:

Make a POST request with JSON data:

```bash
curl -X POST -H "Content-Type: application/json" -d @data.json http://localhost:8080/splashgen
```

Sample data.json file:
```json
{
  "pdfFile": "/path/to/input.pdf",
  "splashFile": "/path/to/splashTemplate.pdf",
  "combinedFile": "/path/to/output.pdf",
  "instrucs": [
    {
      "paragraph": [
        {"text": "This is splash page content"}
      ]
    }
  ]
}
```

### Healthcheck
```bash
curl -I http://localhost:8080/splashgen
```
Returns 200 OK if the service is up.

## Authors
[California Digital Library](https://cdlib.org/)

## License
[BSD 3-Clause](./LICENSE)
