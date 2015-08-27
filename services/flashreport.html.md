---
title: Flashreport
---

Generating reports as PDFs from your systems has never been so easy and cost effective.
No need to provision hardware or acquire costly and complex report generation solutions. Simply:

* Use our API to send us your data in JSON or XML
* We generate the report and store it safely on Amazon S3
* You download it and store it where you want


## <a id='managing'></a>Creating and Managing Services Instances ##

Refer to [Managing Service Instances with the CLI](/devguide/services/managing-services.html) for help binding the Flashreport service to your application.

Our [sample Java app](https://github.com/flashreport-io/flashreport-cf-spring) contains a step-by-step guide to binding a Flashreport service instance to an application.

## <a id='using'></a>Using Service Instances with your Application ##

Once you have bound the service to your application and pushed your app again or restaged, the [VCAP_SERVICES Environment Variable](/devguide/deploy-apps/environment-variable.html) contains your API key.

The following example shows the format of credentials in `VCAP_SERVICES` environment variable:

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

Refer to [Binding Applications to Service Instances](/devguide/services/application-binding.html#use) for additional information.

## <a id='sample-app'></a>Sample Applications ##

See our [sample Java app](https://github.com/flashreport-io/flashreport-cf-spring) on GitHub.

## <a id='dashboard'></a>Dashboard ##

The Flashreport dashboard lets you consult your generated reports and manage your templates. Access your dashboard by clicking **Manage** next to the Flashreport service in the Services section of your space.


## <a id='addl-docs'></a>Additional Documentation

Consult our detailed documentation on [http://flashreport.io/docs.html](http://flashreport.io/docs.html).

## <a id='support'></a>Support ##

[Contacting Service Providers for Support](/marketplace/contacting-service-providers-for-support.html)

Consult our support page [http://flashreport.io/support.html](http://flashreport.io/support.html).

