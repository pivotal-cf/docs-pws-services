---
title: Memcachier
---

The Easiest, Most Advanced Managed Memcache.

## <a id='managing'></a>Managing Services ##

[Managing services from the command line](/devguide/services/managing-services.html)

## <a id='using'></a>Using Service Instances with your Application ##

See [Using Service Instances with your Application](/devguide/services/adding-a-service.html#using) and [VCAP_SERVICES Environment Variable](/devguide/deploy-apps/environment-variable.html).

Format of credentials in `VCAP_SERVICES` environment variable.

~~~xml
{
  memcachier-n/a: [
    {
      name: "memcachier-1234",
      label: "memcachier-n/a",
      tags: [
        "caching"
      ],
      plan: "dev",
      credentials: {
        servers: "mc4.dev.ec2.memcachier.com:11211",
        username: "3668cf",
        password: "bf12d43795"
      }
    }
  ]
}
~~~

## <a id='additional-documention'></a>Additional Documentation ##

https://www.memcachier.com/documentation

## <a id='support'></a>Support ##

[Contacting Service Providers for Support](../contacting-service-providers-for-support.html)

https://memcachier.zendesk.com/


