# Template Healthcare Portal to FHIR EHR Experience API


# License Agreement

This template is subject to the conditions of the [MuleSoft License Agreement](https://s3.amazonaws.com/templates-examples/AnypointTemplateLicense.pdf). Review the terms of the license before downloading and using this template. You can use this template for free with the Mule Enterprise Edition, CloudHub, or as a trial in Anypoint Studio.

# Use Case

As a Portal User I want a service to request and update Clinical data from an EHR system and Salesforce Health Cloud.

# Considerations

To make this Anypoint Template run, there are certain preconditions that must be considered. Failing to do so could lead to unexpected behavior of the template.

## CloudHub Security Considerations

- When VPC is configured in a Cloudhub account, two additional ports are available for internal calls: 8091 and 8092.
- ${http.port} and ${https.port} are still reserved for external endpoints and should not be used for setting internal port values.
- Internal endpoints can be configured using proposed placeholders: ${http.internal.port} and ${https.internal.port}.
- URL naming convention: calls between applications within the same VPC: mule-worker-internal-<appname\>.cloudhub.io
- CloudHub does not replace provided SSL certificates for internal calls, therefore they should be valid for the applicable URL naming convention.

## API Security Considerations
Deploy the Experience API to CloudHub and managed using API Manager.

### Expose External Endpoints with HTTPS and Basic Authentication
- Trigger using SFDC Health Cloud over HTTPS.

### Expose Internal Endpoints with RAML and HTTPS
- Interconnect internally with EHR FHIR System API, Appointments Process API and Onboarding Process API which are deployed within a CloudHub VPC.

# Run it!
Simple steps to get Healthcare Portal to FHIR EHR Experience API running.

## Run On Premises
In this section we detail the way you should run your Anypoint Template on your computer.


### Where to Download Anypoint Studio and the Mule Runtime

If you are new to Mule, download this software:

- [Download Anypoint Studio](https://www.mulesoft.com/platform/studio)
- [Download Mule runtime](https://www.mulesoft.com/lp/dl/mule-esb-enterprise)

### Import Template in Studio

In Studio, click the Exchange X icon in the upper left of the taskbar, log in with your
Anypoint Platform credentials, search for the template, and click **Open**.

### Run in Studio

After opening your template in Anypoint Studio, follow these steps to run it:

1. Locate the properties file `mule.dev.properties`, in src/main/resources.
2. Complete all the properties in the "Properties to Configure" section.
3. Right click the template project folder.
4. Hover your mouse over `Run as`.
5. Click `Mule Application (configure)`.
6. Inside the dialog, select Environment and set the variable `mule.env` to the value `dev`.
7. Click `Run`.

### Run with Mule Stand Alone
Complete all properties in one of the property files, for example in `mule.prod.properties` and run your app with the corresponding environment variable to use it. To follow the example, use `mule.env=prod`.

## Run in CloudHub
After adding your application to Runtime Manager, go to **Manage Application** > **Properties** to set the environment variables listed in the "Properties to Configure" section.

### Deploy in CloudHub

In Studio, right click your project name in Package Explorer and select **Anypoint Platform** > **Deploy on CloudHub**.



## Properties to Configure
In order to use this Mule Anypoint Template you need to configure properties (Credentials, configurations, etc.) either in properties file or in CloudHub as Environment Variables. 

### Application Properties

**HTTPS Configuration**
- https.port `8082`
- keystore.location `keystore.jks`
- keystore.password `pass123!`
- key.password `pass123!`
- key.alias `1`

**API Calls Configuration**

- api.ehr.host `ehr_system_api_hostname`
- api.ehr.basepath `/api`
- api.ehr.port `80`

- api.appointment.host `appointment_process_api_hostname`
- api.appointment.basepath `/api`
- api.appointment.port `80`

- api.identity.host `identity_process_api_hostname`
- api.identity.port `80`
- api.identity.basepath `/api`

- api.onboarding.host `onboarding_process_api_hostname`
- api.onboarding.port `80`
- api.onboarding.basepath `/api`

**API Autodiscovery**

- api.id `api_id`
- anypoint.platform.client_id `anypoint_platform_client_id`
- anypoint.platform.client_secret `anypoint_platform_client_secret`
