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
If interested in the program, please email us at help@passtools.com in order to open up the API UI views and access.

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

A pass template is made up of a header and its hash map field model.
* The header contains information around the template itself, such as ID, name, description, type (boarding pass, coupon, event..).
* A field is a a multi-value object identified by a key name. It represents an element of the pass such as "label", "value" , "change message" on update, etc...
* The "template model" is a hashmap for the fields representation of the pass. The hash map key is the field key name and its value is the fied multiple attributes.

On you have created a pass template in the passtools.com UI, you can get the field through our GET /template/{templateID} api.
You are then free to use that model in order to set its value and create passes based on it.

####Passes

Creating a pass is as simple as passing the field model into the POST /pass/{templateId} api with the model as a {key,JSON} form field array. 
The field model is the pass template with values set by your application needs.

Once a personalized pass is created, you can download it as a file from your api caller through the GET /pass/{passID}/download, or through our SDKs.
That pass can then be delivered to you consumer base, either attached as a file to an email, or through an URL where you will host it, or SMS.

We will soon offer deliverability features in order to provide tigher 1:1 analytics from your passes to a consumer and in order for you to avoid web hosting pass URLS.


####Pass Fields




### Security




## API Doc

The detailed API documentation can be found [here](https://github.com/tello/passtools-api/wiki/Methods).


