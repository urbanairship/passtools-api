passtools-api
=============

Official documentation and resources for the Passtools.com REST API.




## Overview

The PassTools API enables you to easily create/update Apple's PassBook passes, called passes in our system.

You can code directly to the APIs or use the existing client SDKs we have in the following languages:
* [Java](https://github.com/tello/passtools-java)
* [Ruby](https://github.com/tello/passtools-ruby)
* [Python](https://github.com/tello/passtools-python)



### Early API Access Program

The initial rollout is limited to a few early users in order to make sure we can provide the right level of customer service support as we scale up our support systems.
If interested in the program, please email us at help@passtools.com in order to open up the API related UI views and API access.

Once enrolled, the UI will give you the ability to 
* Create/edit pass templates
* View API Logs 


## Fundamental Concepts

The primary concept is that passes are created from pass templates. 

Passes can then be
* Updated so they they can be updated on an existing iPhone PassBook and later automatically 
through a push notification system (coming soon).
* Delivered through your own systems (emails, as URLs or SMS) to your consumers.

We will then report analytics on the number of installs/uninstalls through the passtools.com UI.



### API Objects

Our API objects are accessed through a REST architecture over https.

####Pass Templates

A pass template, or template, is made up of a header and its hash map field model.
* The header contains information around the template itself, such as ID, name, description, type (boarding pass, coupon, event..).
* A field is a a multi-value object identified by a key name. It represents an element of the pass such as "label", "value" , "change message" on update, etc...
* The "template model" is a hashmap for the fields representation of the pass. The hash map key is the field key name and its value is the fied multiple attributes.

On you have created a template in the passtools.com UI, you can get the field model through our GET /template/{templateID} api.
You are then free to use that model in order to set its value and create passes based on it.

####Passes

Creating a pass is as simple as passing the field model into the POST /pass/{templateId} api with the model as a {key,JSON} form field array. 
The field model is the pass template with values set by your application needs.

Once a personalized pass is created, you can download it as a file from your api caller through the GET /pass/{passID}/download, or through our SDKs.
That pass can then be delivered to you consumer base, either attached as a file to an email, or through an URL where you will host it, or SMS.

We will soon offer deliverability features in order to provide tigher 1:1 analytics from your passes to a consumer and in order for you to avoid web hosting pass URLS.


####Pass Fields

Pass fields, or fields, are elements of the pass. Field attributes are exposed through the template creation flow of passtools.com.

A field is a {key,JSON} entry where the JSON is made of the following attributes
* key: the key name is clearly exposed in the UI and the get template API. You can rename the key name as desired from the UI.
* field type: as defined by the Apple's spec, a field can be a TopLevel field, Header, Barcode, Back field, etc...
* label: the label shown on a PassBook pass (for instance "Discount" for a coupon pass)
* value: the actual value for a field (for instance Discount: $30 for label:value).
* required: a true/false boolean needed to keep the integrity of the pass per your template creation definition.
* changeMessage: the push notification message sent for a field level change (for instance "boarding gate change )


The {key,JSON} structure is generic and therefore we expect to enrich the JSON with more attributes as we enrich the functionality of API platform.


### Security


* Our APIs only work under 2048 bit HTPPS encrypted connections to ensure your data is private from client to server connections.
* Access is authenticated through a unique secret key which we provide to you during the onboarding process. It is your responsibility to keep this key well guarded as it represents your identity.
* We assign a unique Apple Certificate to your passes to ensure the Certificate is only used by you.




## API Doc

The detailed API documentation can be found [here](https://github.com/tello/passtools-api/wiki/Methods).


# Feedback

Please send us any feedback at help@passtools.com. 
We listen carefully to your needs and are working on adding important requested functionality (certificate uploads, push notifications, redemption, internalization, etc..).


