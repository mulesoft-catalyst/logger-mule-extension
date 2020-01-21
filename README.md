## Creation

This extension was built using SDK version 1.1 and archetype version 1.0.1.
It's a Logger module that enforces best practices and outputs log fields in JSON format.

https://docs.mulesoft.com/mule-sdk/1.1/xml-sdk#create-and-test-an-xml-sdk-project

There is an issue and you have to add the following to your pom file
to get, the created archetype, to compile:

```
<pluginRepositories>
        <pluginRepository>
            <id>mulesoft-releases</id>
            <name>mulesoft release repository</name>
            <layout>default</layout>
            <url>https://repository.mulesoft.org/releases/</url>
            <snapshots>
                <enabled>false</enabled>
            </snapshots>
        </pluginRepository>
    </pluginRepositories>
```

### Custom Types

Follow this documentation: https://docs.mulesoft.com/mule-sdk/1.1/xml-sdk#example-using-json-custom-types.

Enumerations (DropBox in UI) are strings in the json schema, not objects.


## Build

mvn clean install -DskipTests=true

## Usage

To use this smart connector add the following to your pom file:
```
<dependency>
    <groupId>org.mule.extension</groupId>
	<artifactId>logger-mule-extension</artifactId>
	<version>1.0.0-SNAPSHOT</version>
	<classifier>mule-plugin</classifier>
</dependency>
```
### Sample output

```
INFO  2020-01-21 15:06:41,116 [[MuleRuntime].cpuLight.23: [xml-sdk-companion].smart-connector-code.CPU_LITE @10c3bfdd] [event: c4618950-3c78-11ea-8cbd-38f9d3924940] logger-mule-extension: {"level": "INFO","applicationName": "xml-sdk-companion","applicationVersion": "1.0.0","executionPoint": "flow-name","correlationId": "c4618950-3c78-11ea-8cbd-38f9d3924940","message": {"key": "value"}}
```
