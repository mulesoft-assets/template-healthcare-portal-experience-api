# Template Healthcare Portal to FHIR EHR Experience API

+ [License Agreement](#licenseagreement)
+ [Use Case](#usecase)
+ [Considerations](#considerations)
	* [Cloudhub security considerations](#cloudhubsecurityconsiderations)
	* [APIs security considerations](#apissecurityconsiderations)
+ [Run it!](#runit)
	* [Running on premise](#runonopremise)
	* [Running on Studio](#runonstudio)
	* [Running on Mule ESB stand alone](#runonmuleesbstandalone)
	* [Running on CloudHub](#runoncloudhub)
	* [Deploying your Anypoint Template on CloudHub](#deployingyouranypointtemplateoncloudhub)
	* [Properties to be configured (With examples)](#propertiestobeconfigured)

# License Agreement <a name="licenseagreement"/>
Note that using this template is subject to the conditions of this [License Agreement](AnypointTemplateLicense.pdf).
Please review the terms of the license before downloading and using this template. In short, you are allowed to use the template for free with Mule ESB Enterprise Edition, CloudHub, or as a trial in Anypoint Studio.

# Use Case <a name="usecase"/>

As a Portal User I want a service to request and update Clinical data from an EHR system and Salesforce Health Cloud.

# Considerations <a name="considerations"/>

To make this Anypoint Template run, there are certain preconditions that must be considered. **Failing to do so could lead to unexpected behavior of the template.**

## Cloudhub security considerations <a name="cloudhubsecurityconsiderations"/>

+ When VPC is configured in a Cloudhub account, two additional **ports** are available **for internal calls: 8091 and 8092**
+ ${http.port} and ${https.port} are still reserved for external endpoints and should not be used for setting internal port values
+ Internal endpoints **can be configured using** proposed placeholders: **${http.internal.port}** and **${https.internal.port}**
+ There is a URL naming convention for **calls between applications within the same VPC: mule-worker-internal-<appname\>.cloudhub.io**
+ **Cloudhub will not replace provided SSL certificates for internal calls**, therefore they should be valid for the mentioned URL naming convention

## APIs security considerations <a name="apissecurityconsiderations"/>
This Experience API is meant to be deployed to CloudHub and managed using the API Platform Manager.

### Exposing external endpoints with HTTPS and basic authentication
+ It is triggered by SFDC Health Cloud using HTTPS

### Exposing internal endpoints with RAML and HTTPS
+ It is interconnected internally with EHR FHIR System API, Appointments Process API and Onboarding Process API which are deployed within a CloudHub VPC.

# Run it! <a name="runit"/>
Simple steps to get Healthcare Portal to FHIR EHR Experience API running.
See below.

## Running on premise <a name="runonopremise"/>
In this section we detail the way you should run your Anypoint Template on your computer.


### Where to Download Mule Studio and Mule ESB
First thing to know if you are a newcomer to Mule is where to get the tools.

+ You can download Anypoint Studio from this [Location](http://www.mulesoft.com/platform/studio)
+ You can download Mule ESB from this [Location](http://www.mulesoft.com/platform/soa/mule-esb-open-source-esb)

### Importing an Anypoint Template into Studio
Mule Studio offers several ways to import a project into the workspace, for instance:

+ Anypoint Studio Project from File System
+ Packaged mule application (.jar)

You can find a detailed description on how to do so in this [Documentation Page](https://docs.mulesoft.com/studio/7.2/import-export-packages).

### Running on Studio <a name="runonstudio"/>
Once you have imported you Anypoint Template into Anypoint Studio you need to follow these steps to run it:

+ Generate keystore (You can find a detailed description on how to do so in this [Documentation Page](https://docs.mulesoft.com/mule-runtime/4.1/tls-configuration))
+ Locate the properties file `mule-<env>.properties`, in src/main/resources
+ Complete all the properties required as per the examples in the section [Properties to be configured](#propertiestobeconfigured)
+ Once that is done, right click on you Anypoint Template project folder
+ Hover you mouse over `"Run as"`
+ Click on  `"Mule Application"`

### Running on Mule ESB stand alone <a name="runonmuleesbstandalone"/>
Complete all properties in one of the property files, for example in `mule.prod.properties` and run your app with the corresponding environment variable to use it. To follow the example, this will be `mule.env=prod`.

## Running on CloudHub <a name="runoncloudhub"/>
While creating your application on CloudHub (or you can do it later as a next step), you need to go to `"Manage Application"` > `"Properties"` to set all environment variables detailed in **Properties to be configured**.
Follow other steps defined [here](#runonpremise) and once your app is all set and started, there is no need to do anything else.

### Deploying your Anypoint Template on CloudHub <a name="deployingyouranypointtemplateoncloudhub"/>
Mule Studio provides you with really easy way to deploy your Template directly to CloudHub, for the specific steps to do so please check this [link](https://docs.mulesoft.com/runtime-manager/deploying-to-cloudhub)

## Properties to be configured (With examples) <a name="propertiestobeconfigured"/>
In order to use this Mule Anypoint Template you need to configure properties (Credentials, configurations, etc.) either in properties file or in CloudHub as Environment Variables. Detailed list with examples:
### Application properties

**HTTPS configuration**
+ https.port `8082`
+ keystore.location `keystore.jks`
+ keystore.password `pass123!`
+ key.password `pass123!`
+ key.alias `1`

**API calls configuration**

+ api.ehr.host `ehr_system_api_hostname`
+ api.ehr.basepath `/api`
+ api.ehr.port `80`

+ api.appointment.host `appointment_process_api_hostname`
+ api.appointment.basepath `/api`
+ api.appointment.port `80`

+ api.identity.host `identity_process_api_hostname`
+ api.identity.port `80`
+ api.identity.basepath `/api`

+ api.onboarding.host `onboarding_process_api_hostname`
+ api.onboarding.port `80`
+ api.onboarding.basepath `/api`

**API Autodiscovery**

+ api.id `api_id`
+ anypoint.platform.client_id `anypoint_platform_client_id`
+ anypoint.platform.client_secret `anypoint_platform_client_secret`
