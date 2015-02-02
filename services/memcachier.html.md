---
title: MemCachier
---

[MemCachier](http://www.memcachier.com/) is an implementation of the [Memcache](http://memcached.org/) in-memory key-value store used for caching data. MemCachier is a key technology for scaling and reducing server loads in web applications. The MemCachier add-on manages and scales clusters of memcache servers so that operators can focus on their applications. Tell us how much memory you need and get started for free instantly. You can add capacity later as the need arises.

## <a id='managing'></a>Managing Services ##

Refer to the [Managing Service Instances with the CLI](/devguide/services/managing-services.html) topic for more information.

### <a id='create-service'></a>Creating a MemCachier Service ###

Create a MemCachier service with the following command:

<pre class="terminal">
$ cf create-service memcachier PLAN_NAME INSTANCE_NAME
</pre>

where `PLAN_NAME` is the name of the desired plan and `INSTANCE_NAME` is a name meaningful to you.

### <a id='bind-service'></a>Binding Your MemCachier Service ###

Bind your MemCachier service to your app using the following command:

<pre class="terminal">
$ cf bind-service APP_NAME INSTANCE_NAME
</pre>

Once your MemCachier service is bound to your app, the service credentials will be stored in the `VCAP_SERVICES` environment variable in the following format:

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

For more information, see [Using Service Instances with your Application](/devguide/services/adding-a-service.html#using) and [VCAP_SERVICES Environment Variable](/devguide/deploy-apps/environment-variable.html).

## <a id='ruby'></a>Using MemCachier with Ruby ##

Start by adding the [Dalli](https://github.com/mperham/dalli) gem to your Gemfile. Dalli is a high performance Ruby memcache client.

<pre>
gem 'dalli'
</pre>

Then run `bundle install`:

<pre class="terminal">
$ bundle install
</pre>

Before writing code, you need to create a client object with the correct credentials and settings as the example below shows:

~~~xml
require 'dalli'
cache = Dalli::Client.new((ENV["MEMCACHIER_SERVERS"] || "").split(","),
                    {:username => ENV["MEMCACHIER_USERNAME"],
                     :password => ENV["MEMCACHIER_PASSWORD"],
                     :failover => true,
                     :socket_timeout => 1.5,
                     :socket_failure_delay => 0.2})
~~~

You can now use the cache through simply operations such as `get` and `set`, as the example shows:

~~~xml
cache.set("foo", "bar")
puts cache.get("foo")
~~~

### <a id='ruby-testing'></a>Testing from Ruby ###

## <a id='rails'></a>Using MemCachier with Rails ##

Rails supports three types of caching: automatic whole site, per-view, and fragment. Refer to the [Rails caching guide] for more information on using MemCachier with Rails.

Add the Dalli gem and run `bundle install` as described in the above <a href="#ruby">Ruby</a> section. Once this gem is installed you will want to configure the Rails `cache_store` appropriately. Modify your `config/environments/production.rb` with the following:

~~~xml
config.cache_store = :dalli_store,
                    (ENV["MEMCACHIER_SERVERS"] || "").split(","),
                    {:username => ENV["MEMCACHIER_USERNAME"].
                     :password => ENV["MEMCACHIER_PASSWORD"],
                     :failover => true,
                     :socket_timeout => 1.5,
                     :socket_failure_delay => 0.2
                    }
~~~

<p class="note"><strong>Note</strong>: Rails.cache defaults to a simple in-memory store in your deployment environment, so it does not require a running memcached.</p>

### <a id='rails-testing'></a>Testing from Rails ###

To test locally you can simply use the rails console:

<pre class="terminal">
rails console
>> Rails.cache.write('memcachier', 'clouds')
=> true
>> Rails.cache.read('memcachier')
=> 'clouds'
</pre>

## <a id='python'></a>Using MemCachier with Python ##

MemCachier has been tested with the `pylibmc` memcache client. This client relies on the C libmemcached library, which should be simple to install with your package manager on Linux or Windows. Once libmemcached is installed, install `pylibmc`:

<pre class="terminal">
$ pip install pylibmc
</pre>

Be sure to update your `requirements.txt` file with the new `pylibmc` requirement. Your version might differ from the version in the below example.

<pre>
pylibmc==1.4.0
</pre>

<p class="note"><strong>Note</strong>: If you have difficulty installing the C libmemcached library or `pylibmc`, you can try python-binary-memcached. This is a pure python client that only supports Python 2 at this time.</p>

Next, configure your `settings.py` file as the following example shows:

~~~xml
import pylibmc

servers = os.environ.get('MEMCACHIER_SERVERS', '').split(',')
user = os.environ.get('MEMCACHIER_USERNAME', '')
pass = os.environ.get('MEMCACHIER_PASSWORD', '')

mc = pylibmc.Client(servers, binary=True,
                    username=user, password=pass,
                    behaviors={"tcp_nodelay": True,
                               "ketama": True,
                               "no_block": True,})
~~~

After this, you can start writing cache code in your Python application:

<pre>
mc.set("foo", "bar")
print mc.get("foo")
</pre>

<p class="note"><strong>Note</strong>: A confusing error message you may get from `pylibmc` is <strong>MemcachedError: error 37 from memcached_set: SYSTEM ERROR (Resource temporarily unavailable)</strong>. This indicates that you are trying to store a value larger than 1MB. MemCachier has a hard limit of 1MB for the size of key-value pairs. To work around this, either consider sharding the data or using a different technology. The benefit of an in-memory key-value store diminishes at 1MB and higher.
</p>

##<a id='node'></a>Using MemCachier with Node.js ##

For Node.js we recommend the use of the [memjs](http://github.com/alevy/memjs) client library, which is written and supported by MemCachier. To install memjs, use [node package manager (npm)](http://npmjs.org/) as the following command shows:

<pre class="terminal">
$ npm install memjs
</pre>

The memjs library understands the `MEMCACHIER_SERVERS`, `MEMCACHIER_USERNAME`, and `MEMCACHIER_PASSWORD` environment variables that the MemCachier add-on sets up, as the following example shows:

<pre>
var memjs = require('memjs')
var mc = memjs.Client.create()
mc.get('hello', function(val) {
  alert(val)
})
</pre>

##<a id='java'></a>Using MemCachier with Java ##

We recommend using the [SpyMemcached](http://code.google.com/p/spymemcached/) client for Java. We also recommend using the [Apache Maven](http://maven.apache.org/) build manager for working with Java applications. If you are not using `maven` and are isntead using [Apache Ant](http://ant.apache.org/) or your own build system, then add the `spymemcached` jar file as a dependency of your application.

<p class="note"><strong>Note</strong>: Please make sure to use version <strong>2.8.9</strong> of SpyMemcached. Versions 2.8.10 and later currently have an [issue](http://code.google.com/p/spymemcached/issues/detail?id=272) with SASL authentication that makes these versions unusable with MemCachier.</p>

If you are using `maven`, start by configuring it to have the proper `spymemcached` repository:

~~~xml
<repository>
  <id>spy</id>
  <name>Spy Repository</name>
  <layout>default</layout>
  <url>http://files.couchbase.com/maven2</url>
  <snapshots>
    <enabled>false</enabled>
  </snapshots>
</repository>
~~~

Then add the `spymemcached` library to your dependencies:

~~~xml
<dependency>
  <groupId>spy</groupId>
  <artifactId>spymemcached</artifactId>
  <version>2.8.9</version>
  <scope>provided</scope>
</dependency>
~~~

Once your build system is configured, you can start adding caching to your Java app as shown in the following example:

~~~xml
import java.io.IOException;
import net.spy.memcached.AddrUtil;
import net.spy.memcached.MemcachedClient;
import net.spy.memcached.ConnectionFactoryBuilder;
import net.spy.memcached.auth.PlainCallbackHandler;
import net.spy.memcached.auth.AuthDescriptor;

public class Foo {
  public static void main(String[] args) {
    AuthDescriptor ad = new AuthDescriptor(new String[] { "PLAIN" },
        new PlainCallbackHandler(System.getenv("MEMCACHIER_USERNAME"),
            System.getenv("MEMCACHIER_PASSWORD")));

    try {
      MemcachedClient mc = new MemcachedClient(
          new ConnectionFactoryBuilder()
              .setProtocol(ConnectionFactoryBuilder.Protocol.BINARY)
              .setAuthDescriptor(ad).build(),
          AddrUtil.getAddresses(System.getenv("MEMCACHIER_SERVERS")));
      mc.set("foo", "bar");
      System.out.println(mc.get("foo"));
    } catch (IOException ioe) {
      System.err.println("Couldn't create a connection to MemCachier: \nIOException "
              + ioe.getMessage());
    }
  }
}
~~~

You may want to set the above code up as a new MemCachierClient class as shown in the following example:

~~~xml
package com.memcachier.examples.java;

import java.io.IOException;
import java.net.InetSocketAddress;
import java.util.ArrayList;
import java.util.List;

import javax.security.auth.callback.CallbackHandler;

import net.spy.memcached.ConnectionFactory;
import net.spy.memcached.ConnectionFactoryBuilder;
import net.spy.memcached.MemcachedClient;
import net.spy.memcached.auth.AuthDescriptor;
import net.spy.memcached.auth.PlainCallbackHandler;

public class MemCachierClient extends MemcachedClient {

   public MemCachierClient(String username, String password, String servers) throws IOException {
       this(new SASLConnectionFactoryBuilder().build(username, password), getAddresses(servers));
   }

   public MemCachierClient(ConnectionFactory cf, List<InetSocketAddress> addrs) throws IOException {
       super(cf, addrs);
   }

   private static List<InetSocketAddress> getAddresses(String servers) {
       List<InetSocketAddress> addrList = new ArrayList<InetSocketAddress>();
       for (String server : servers.split(",")) {
           String addr = server.split(":")[0];
           int port = Integer.parseInt(server.split(":")[1]);
           addrList.add(new InetSocketAddress(addr, port));
       }
       return addrList;
   }
}

class SASLConnectionFactoryBuilder extends ConnectionFactoryBuilder {
   public ConnectionFactory build(String username, String password){
       CallbackHandler ch = new PlainCallbackHandler(username, password);
       AuthDescriptor ad = new AuthDescriptor(new String[]{"PLAIN"}, ch);
       this.setProtocol(Protocol.BINARY);
       this.setAuthDescriptor(ad);
       return this.build();
   }
}
~~~

<p class="note"><strong>Note</strong>: It is possible that you might run into Java exceptions about the class loader. See Spymemcached [issue 155](http://code.google.com/p/spymemcached/issues/detail?id=155), which contains a suggested workaround.</p>

## <a id='support'></a>Support ##

[Contacting Service Providers for Support](../contacting-service-providers-for-support.html)

[MemCachier Zendesk](https://memcachier.zendesk.com/)

## <a id='additional-documention'></a>Additional Resources ##

[MemCachier documentation](https://www.memcachier.com/documentation)



