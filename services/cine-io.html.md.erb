---
title: cine.io
---

<strong><%= modified_date %></strong>

cine.io is an add-on that provides live streaming capabilities to any application.
cine.io allows developers to build live video-streaming capabilities into their apps with ease. Streaming can happen from any device to any web browser, iOS device, or Android device. All live-streams are backed by a global CDN with 5,000 interconnected networks across 5 continents.
cine.io is accessible via a simple RESTful API and has supported client libraries for both Node.js and Ruby (with iOS and Android coming soon).

## <a id='managing'></a>Managing Services ##

cine.io can be added to your project and bound to your space by selecting cine.io from the Pivotal Web Services Marketplace. Select the appropriate plan and configure the instance name, the space to add it to, as well as the application to bind cine.io to.

Once cine.io has been bound to your application you need to restart your application for it to be able to access the new VCAP_SERVICES environment variable. You can restart the application by clicking the "restart" button on the application page.

## <a id='within-application'></a>Using cine.io within Your Application ##

Once cine.io is bound it updates the VCAP_SERVICES environment variable with an entry for 'cine-io' which contains the credentials as well as other information to access cine.

The VCAP_SERVICES entry will look like:

    {"cine-io":[{"name":"cine-example1","label":"cine-io","tags":["Communication","Messaging and Queuing"],"plan":"starter","credentials":{"publicKey":"PUBLIC_KEY","secretKey":"SECRET_KEY"}}]}

To start using cine.io in your application, import the appropriate cine.io SDK and use it with the Public and Secret keys that are available in VCAP_SERVICES

## <a id='request'></a>Common Request Lifecycle ##

1. Create a live stream
2. Publish a live stream
3. Play a live stream

### Create a live stream ###

Every project starts off with 1 live stream. Most likely you’ll want to have more than 1 unique live stream.
Requests normally start off by creating a live stream. This live stream is unique to your project. You’ll get a response back containing a few fields. The most important fields to save in your database is id, and password. You’ll need these fields to play and publish your live stream. You can always fetch the other fields again by issuing a get request to the stream/show endpoint.

Look at the API docs for POST /stream to learn how to create a stream.

### Publish a live stream ###

Now you’ve saved your stream id and stream password. Using the JS SDK, you’ll need to pass you project’s publicKey to the client. If your specific user has permission in your application to publish to this stream, then you’ll need to send along the stream id and stream password to your web client. For example, this endpoint would be useful if you are building a “virtual classroom” and the current logged-in user has a “teacher” role.

Publishing a live-stream requires that the logged-in user have Adobe Flash installed and enabled in her browser. The JS SDK will automatically download the correct SWF file and launch it in the user’s browser when start ``()`` is called on the publisher.

		var streamId = '<STREAM_ID>'
		  , password = '<STREAM_PASSWORD'
		  , domId = 'publisher-example';

		var publisher = CineIO.publish(
		  streamId, password, domId
		);

		publisher.start();

### Play a live stream ###

Using the JS SDK, you’ll need to pass you project’s public key to the client. To play a stream using the JS SDK, you only need to send out the stream id. Only serve the stream id to users who have permission to view a stream. For example, in our aforementioned “virtual classroom” application, this endpoint would be useful when the current logged- in user has a “student” role.

Playing a live stream will launch the branded, open-source version of JWPlayer. If you have your own JWPlayer license, you can send it as one of the options (key: jwPlayerKey) to the init ``()`` function. Mobile devices will use native `<video>` elements rather than JWPlayer; this happens automatically.

		var streamId = '<STREAM_ID>'
		  , domId = 'player-example';

		CineIO.play(streamId, domId);


### Additional API endpoints ###

Additional API endpoints may be found at: http://www.cine.io/docs.

## <a id='using'></a>Using cine.io ##

### Using with Rails ###

We’ve built a small Ruby Sinatra example.
[Source code](https://github.com/cine-io/cineio-sinatra-example-app)

### Integrate with your Ruby app ###

Ruby on Rails applications may to add the following entry into their Gemfile specifying the cine.io client library.

	gem 'cine_io'

Update application dependencies with bundler.

	$ bundle install

Initialize the client.

	require('cine_io')
    credentials = privateKey = secretKey = ''
    if !ENV['VCAP_SERVICES'].blank?
      JSON.parse(ENV['VCAP_SERVICES']).each do |k,v|
        if !k.scan("cine-io").blank?
          credentials = v.first.select {|k1,v1| k1 == "credentials"}["credentials"]
          secretKey = credentials["secretKey"]
          privateKey = credentials["privateKey"]
        end
      end
    end
	client = CineIo::Client.new(secretKey: secretKey)

Additional examples can be found at the repository’s [homepage](https://github.com/cine-io/cineio-ruby).

### Using with Node.js ###

We’ve built a small Node.js Express example.
[Source code](https://github.com/cine-io/cineio-node-example-app)

Integrate with your Node app. The npm package may be installed with the following command.

	npm install --save cine-io

Initialize the client.

	var CineIO = require('cine-io');
	var vcap_services = JSON.parse(process.env.VCAP_SERVICES)
	var secretKey = vcap_services['cine-io'][0].credentials.secretKey
	var client = CineIO.init({secretKey: secretKey});

Additional examples can be found at the repository’s [homepage](https://github.com/cine-io/cineio-node).


## <a id='support'></a>Support ##

cine.io support resources: https://cineio.uservoice.com

## <a id='reources'></a>Additional Resources ##

http://www.cine.io/