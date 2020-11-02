## Creation

This extension was built using SDK version 1.1 and archetype version 1.0.1.
It's a Logger module that enforces best practices and outputs log fields in JSON format.

Mule XML SDK initial project steps:
https://docs.mulesoft.com/mule-sdk/1.1/xml-sdk#create-and-test-an-xml-sdk-project

There is an issue with the generated code and you have to add the following to your pom file
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

We use custom types to create enumeration-type fields. Please follow this documentation to understand the process of 
creating such a field for an operation: https://docs.mulesoft.com/mule-sdk/1.1/xml-sdk#example-using-json-custom-types.

Enumerations (DropBox in UI) are strings in the json schema, not objects.

## Custom Icon

The default icon could be replaced with a customized logo by replacing the icon.svg file under the icon folder at root project level

## Build and Deployment

Replace YOUR_ORG_ID value in the POM file for the actual id of the anypoint platform organization where you will be 
publishing the module

The following changes are not mandatory but recommended:

* Customize the package name according to your organization guidelines. The default value is 'org.company.businessunit'.
* You might also consider customizing the default category value. 

#### Compile
```
mvn clean package -DskipTests=true
```

#### Install in local maven repository

```
mvn clean install -DskipTests=true
````

## Usage

To use this smart connector add the following maven dependency snippet to your mule project pom file. Please verify the
version you want to bring to your project:

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

#### Testing Process For New Module's Versions 

Assuming you have created a project in Anypoint Studio, where you have added the module's dependency snippet: 
     
##### Testing Loop

- Every time you want to try module's changes in Studio, increase the POM file version number (i.e from 1.0.0 to 1.0.1) and install again into your local m2 repository. 
- Update the POM file in the mule project where you are using the new module. After saving the POM file, you should see your new version loaded in the Package Explorer.
     
When you are done testing you will need to do the following: 
 - Go back the module version in the POM file to the version that corresponds with the new release (i.e from 1.0.12 to 1.0.2). Your are ready to continue with the upload (Deploy) to Exchange step.
 - Go to Anypoint Studio and reset the modules cache: Anypoint Studio -> Preferences -> Anypoint Studio -> Tooling -> Modules Cache -> Reset
 - This last step is needed so that Studio can pick up again the new module version but containing all the changes introduced by all the temporary module's versions. 
 Studio does not reload a dependency jar’s file for a previously loaded version, It is kept in its cache and that is why we need to reset it.



### Upload to Exchange 

* Again, make sure your ORG ID number is being used as the artifact's _groupId_ in your pom file
* also, define a property in your pom file, like this:
  ```
   <anypoint.org.id>YOUR_ORG_ID</anypoint.org.id>
  ```
  This property is used in the Distribution Management section of the pom file.
* verify you have defined the repository server credentials, the Exchange credentials in this case, in your maven settings.xml file
  ```
  <server>
          <id>anypoint-exchange-v2</id>
          <username>YOUR_USERNAME</username>
          <password>YOUR_PASSWORD</password>
  </server>
  ```

Finally, execute the following command:

```
mvn clean deploy -DskipTests=true
```


### Sample output

```
INFO  2020-05-24 19:45:39,059 [[MuleRuntime].cpuLight.22: [playground].playgroundFlow.CPU_LITE @5c6a236b] [event: 484d43f0-9e10-11ea-bc96-38f9d3924940] logger-mule-extension: {"level": "INFO","timestamp": "2020-05-24T19:45:38.989-03:00","environment": "local","applicationName": "playground","applicationVersion": "1.0.0","flowName": "flow-name","correlationId": "484d43f0-9e10-11ea-bc96-38f9d3924940","message": "This is a sample message","content": {"accountId": "2345994","status": "closed","entitlements": ["BA","KA","PP"]}}
```
