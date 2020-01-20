## Creation

This extension was built using SDK version 1.1 and archetype version 1.0.1

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

