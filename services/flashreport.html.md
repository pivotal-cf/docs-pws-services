---
title: Flashreport
---

Generating reports in PDF from your systems has never been so easy and cost effective.
No need to provision hardware or acquire costly and complex report generation solutions. Simply:

* Use our API to send us your data in JSON or XML
* We generate the report and store it safely on Amazon S3
* You download it and store it where you want


## <a id='managing'></a>Creating and Managing Services Instances ##

Flashreport service can be bound to your application in the usual way, please refer to [Managing services from the command line](/devguide/services/managing-services.html).

Our [sample java app] (https://github.com/flashreport-io/flashreport-cf-spring) contains a step by step guide to bind a flashreport service to an application.

## <a id='using'></a>Using Service Instances with your Application ##

Once the service has been bound to your application (and your application pushed again or restaged), the [VCAP_SERVICES Environment Variable](/devguide/deploy-apps/environment-variable.html) contains your API key.

Format of credentials in `VCAP_SERVICES` environment variable.

~~~xml
{
  flashreport: [
  {
    "name": "flashreport-trial-dev",
    "label": "flashreport",
    "plan": "trial",
    "credentials": {
      "apiKey": "94e29989-4444-5555-6666-28e49fe05f33"
    }
  }
  ]
}
~~~

Please refer to [Using Service Instances with your Application](/devguide/services/adding-a-service.html#use) for additional information.

## <a id='sample-app'></a>Sample Applications ##

Please check our [sample java app] (https://github.com/flashreport-io/flashreport-cf-spring) on GitHub.

## <a id='dashboard'></a>Dashboard ##

Flashreport's dashboard lets you consult your generated reports and manage your templates. Access your dashboard by clicking the 'Manage' button next to the Flashreport service in the Services section of your space.


## <a id='addl-docs'></a>Additional Documentation

Please consult our detailed documentation on [http://flashreport.io/docs.html](http://flashreport.io/docs.html).

## <a id='support'></a>Support ##

[Contacting Service Providers for Support](/marketplace/contacting-service-providers-for-support.html)

Please consult our support page [http://flashreport.io/support.html](http://flashreport.io/support.html).

