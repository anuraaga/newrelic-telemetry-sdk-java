# New Relic Java Telemetry SDK 
The New Relic Java Telemetry SDK for sending telemetry data to New Relic.
The current SDK supports sending dimensional metrics and spans to the Metric and Trace API, respectively.

Why is this cool?

Dimensional Metrics and Spans in New Relic! No agent required. 

The telemetry SDK tries to be helpful, so your job of sending telemetry data to New Relic can be done in the right way, easily. We've covered all of the basics for you so you can focus on writing feature code directly related to your business need or interest.

Why would you want to use the telemetry SDK?

We imagine you (or your customers) are interested in the telemetry data, generated by your tool, framework, or code, in New Relic. You can write an exporter to do so! Check out the [telemetry_examples](telemetry_examples) module to get started.

For the most recently published version, see [Releases](https://github.com/newrelic/newrelic-telemetry-sdk-java/releases)

## Getting Started

In order to send metrics or spans to New Relic, you will need an Insights Insert API Key. 
Please see [New Relic Api Keys](https://docs.newrelic.com/docs/apis/getting-started/intro-apis/understand-new-relic-api-keys#user-api-key)
for more information.

Maven dependencies:

```
    <dependency>
      <groupId>com.newrelic.telemetry</groupId>
      <artifactId>telemetry</artifactId>
      <version>0.3.1</version>
    </dependency>
    <dependency>
      <groupId>com.newrelic.telemetry</groupId>
      <artifactId>telemetry-http-okhttp</artifactId>
      <version>0.3.1</version>
    </dependency>
```

Gradle dependencies: 

```
compile("com.newrelic.telemetry:telemetry:0.3.1")
compile("com.newrelic.telemetry:telemetry-http-okhttp:0.3.1")
```

Take a look at the example code in the [telemetry_examples](telemetry_examples) module. 
We recommend looking at the [TelemetryClientExample](telemetry_examples/src/main/java/com/newrelic/telemetry/exapmles/TelemetryClientExample.java)
first.

Note: If you do not want to include `okhttp` as a transitive depenedency, you will need to provide a custom implementation of the 
`com.newrelic.telemetry.http.HttpPoster` interface, rather than using the `com.newrelic.telemetry:telemetry-http-okhttp` library.

## For Developers: 
### Requirements

* Java 8 or greater
* For IDEA:
    * lombok plugin installed
    * Annotation processing enabled for the project (Sample instructions can be found [here](https://immutables.github.io/apt.html) for popular IDEs)
* Docker & docker-compose must be installed for integration testing

### Building
CI builds are run on Azure Pipelines: 
[![Build Status](https://dev.azure.com/newrelic-builds/java/_apis/build/status/PR%20build%20for%20java%20telemetry?branchName=master)](https://dev.azure.com/newrelic-builds/java/_build/latest?definitionId=8&branchName=master)

The project uses gradle 5 for building, and the gradle wrapper is provided.

To compile, run the tests and build the jars:

`$ ./gradlew build`

### Integration Testing

End-to-end integration tests are included. 
They are implemented with the testcontainers library; [mock-server](https://github.com/jamesdbloom/mockserver) provides the backend.

There are two modes to run the integration tests.
* Run with gradle: `$ ./gradlew integration_test:test`
* Run the integration test classes in IDEA directly. It should "just work".

### Code style
This project uses the [google-java-format](https://github.com/google/google-java-format) code style, and it is 
easily applied via an included [gradle plugin](https://github.com/sherter/google-java-format-gradle-plugin):

`$ ./gradlew googleJavaFormat verifyGoogleJavaFormat`

Please be sure to run the formatter before committing any changes. There is a `pre-commit-hook.sh` which can 
be applied automatically before commits by moving it into `.git/hooks/pre-commit`.

### Module structure:

#### `telemetry_core`
This is the core module for sending dimensional metrics and spans to New Relic. The library is published under maven coordinates:

`com.newrelic.telemetry:telemetry-core`

In order to send metrics and spans to New Relic, you will also need an Insights Insert API Key. 
Please see [New Relic Api Keys](https://docs.newrelic.com/docs/apis/getting-started/intro-apis/understand-new-relic-api-keys#user-api-key)
for more information.

#### `telemetry`
This module contains code for using all New Relic telemetry modules, gathered in one place, as well as what we 
consider "best practice" implementations of how to interact with the lower-level modules.

The `telemetry` library is published under the maven coordinates:

`com.newrelic.telemetry:telemetry`

#### `telemetry-http-okhttp`
This is an implementation of the required http client interface using okhttp as the underlying library.
The `telemetry-http-okhttp` library is published under the maven coordinates:

`com.newrelic.telemetry:telemetry-http-okhttp`

#### `telemetry_examples`
Example code for using the metrics and telemetry APIs.

#### `integration_test`
Integration test module. Uses docker-compose based tests to test the SDK end-to-end.

### Licensing
The New Relic Java Telemetry SDK is licensed under the Apache 2.0 License.

The New Relic Java Telemetry SDK also uses source code from third party libraries. 
Full details on which libraries are used and the terms under which they are licensed can be found in the 
third party notices document.

### Contributing
Full details are available in our [CONTRIBUTING.md](CONTRIBUTING.md) file. 
We'd love to get your contributions to improve the Java Telemetry SDK! Keep in mind when you submit your pull request, you'll need to sign the CLA via the click-through using CLA-Assistant. You only have to sign the CLA one time per project.
To execute our corporate CLA, which is required if your contribution is on behalf of a company, or if you have any questions, please drop us an email at open-source@newrelic.com. 
