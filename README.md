passtools-api
=============

Official documentation and resources for the PassTools REST API.




## Overview

The PassTools API enables you to easily create/update Apple Passbook passes (simply called _passes_ in our system).
If you are not yet familiar with Passbook, please start [here](https://developer.apple.com/passbook/)

You can code directly to the APIs or use the existing client SDKs we have in the following languages:
* [Java](https://github.com/tello/passtools-java)
* [Python](https://github.com/tello/passtools-python)
* [Ruby](https://github.com/tello/passtools-ruby)


## Early API Access Program

The initial rollout of the PassTools API is limited to a few early users in order to make sure we can provide a high level of customer support as we scale up our support systems.
If you are interested in the program, please email us at help@passtools.com and we will do our best to get you access as soon as possible.

Once you are given access, you will have the ability to:
* Create/edit pass templates.
* View API Logs from the web front end in the Activity pages.


## Fundamental Concepts

The primary concept is that passes are created from pass templates. 

Passes can then be:
* Created with your custom data.
* Completely changed and re-added to an existing user's Passbook.
* Updated with certain field changes, so the user's pass would be updated automatically via push notification.
* Delivered through your own systems (email, SMS, URL) to your customers.

We will then provide analytics on the number of installs/uninstalls through the PassTools UI.



## API Objects

Our API objects are accessed through a REST architecture over https.

####Pass Templates

A _pass template_, or _template_, is made up of a header and its hash map field model.
* The _header_ contains information around the template itself, such as ID, name, description, type (boarding pass, coupon, event, etc.).
* A _field_ is a a multi-value object identified by a key name. It represents an element of the pass such as _label_, _value_, _change message_ on update, etc.
* The _template model_ is a hashmap for the fields representation of the pass. The hash map key is the field _key name_ and its value is the fied multiple attributes.

Once you have created a template in the PassTools UI, you can get the field model through our GET /template/{templateID} API.
You are then free to use that model in order to set its value and create passes based on it.

####Passes

Creating a pass is as simple as passing the field model into the POST /pass/{templateId} API with the model as a {key,JSON} form field array. 
The field model is the pass template with values set by your application needs.

Once a personalized pass is created, you can update it, as well as download it as a file from your API caller through the GET /pass/{passID}/download, or through our SDKs.
That pass can then be delivered to your customers, either attached as a file to an email, or through an URL where you will host it, or SMS.

We will soon offer deliverability features in order to provide more advanced 1:1 analytics from your passes to a consumer and in order for you to avoid web hosting pass URLs.


####Locations

We enable to set locations at the pass level in order to create dynamic personalized passes, such as boarding passes or coupons.
For that matter, we provide 2 api endpoints POST pass/{passId}/locations where you can add up to 10 locations for a given pass, as well as the ability to delete a location/pass.

Please note that if the parent template of the pass had locations assigned, the pass will inherit those locations unless you are passing more locations through the API such that count(of location through API) + count( template locations) > 10.
In practice, if you are really trying to dynamically add locations to your passes, it is best to create a template with no locations.



####Pass Fields

Pass fields, or fields, are elements of the pass. Field attributes are exposed through the template creation flow of PassTools.

A field is a {key,JSON} entry where the JSON is made of the following attributes:
* _key:_ the key name is clearly exposed in the UI and the get template API. You can rename the key name as desired from the UI.
* _field type:_ as defined by the Apple's spec, a field can be a TopLevel field, Header, Barcode, Back field, etc.
* _label:_ the label shown on a PassBook pass (for instance "Discount" for a coupon pass).
* _value:_ the actual value for a field (for instance Discount: $30 for label:value).
* _required:_ a true/false boolean needed to keep the integrity of the pass per your template creation definition.
* _changeMessage:_ the push notification message sent for a field level change (for instance "boarding gate change).


The {key,JSON} structure is generic and therefore we expect to enrich the JSON with more attributes as we enrich the functionality of API platform.



Please note that that fields that relate to dates shall be in the following ISO 8601 format: "2013-02-08T09:00:00Z" up to the second.


## Security


* Our APIs only work under 2048 bit HTTPS encrypted connections to ensure your data is private from client to server connections.
* Access is authenticated through a unique secret key which we provide to you during the onboarding process. It is your responsibility to keep this key well guarded as it represents your identity.
* You can either use your own Apple's certificate to sign passes, or we will assign a unique certificate to your account.




## API Doc

The detailed API documentation can be found [here](https://github.com/tello/passtools-api/wiki/Methods_1.1).
  


## Feedback

Please send us any feedback to help@passtools.com. 
We listen carefully to your needs and are working on adding important requested functionality (e.g. web certificate uploads, push notifications, redemption, internationalization, etc.).


