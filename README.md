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

## Custom Icon

The default icon could be replaced with a customized logo by replacing the icon.svg file under the icon folder at root project level

## Build and Deployment

Replace YOUR_ORG_ID value in the POM file for the actual id of the anypoint platform organization where you will be 
publishing the module

#### Compile
mvn clean package -DskipTests=true
#### Install in local maven repository
mvn clean install -DskipTests=true

#### Upload to Exchange 

* Again, make sure your ORG ID number is being used as the artifact's _groupId_ in your pom file
* also, define a property in your pom file, like this:
  ```
   <anypoint.org.id>YOUR_ORG_ID</anypoint.org.id>
  ```
  This property is used in the Distribution Management section of the pom file.
* verify you have defined the repository server credentials, the Exchange credentials in this case, in your maven settings.xml file
  ```
  <server>
          <id>exchange-maven-facade</id>
          <username>YOUR_USERNAME</username>
          <password>YOUR_PASSWORD</password>
  </server>
  ```

Finally, execute the following command:

mvn clean deploy -DskipTests=true


## Usage

To use this smart connector add the following to your pom file:
```
<dependency>
    <groupId>YOUR_ORG_ID</groupId>
	<artifactId>logger-mule-extension</artifactId>
	<version>1.0.0</version>
	<classifier>mule-plugin</classifier>
</dependency>
```

Remember you replaced YOUR_ORG_ID for the actual id of the anypoint platform organization where you want to 
publish the module

### Sample output

```
INFO  2020-05-24 19:45:39,059 [[MuleRuntime].cpuLight.22: [playground].playgroundFlow.CPU_LITE @5c6a236b] [event: 484d43f0-9e10-11ea-bc96-38f9d3924940] logger-mule-extension: {"level": "INFO","timestamp": "2020-05-24T19:45:38.989-03:00","environment": "local","applicationName": "playground","applicationVersion": "1.0.0","flowName": "flow-name","correlationId": "484d43f0-9e10-11ea-bc96-38f9d3924940","message": "This is a sample message","content": {"accountId": "2345994","status": "closed","entitlements": ["BA","KA","PP"]}}
```
