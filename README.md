passtools-api
=============

Official documentation and resources for the Passtools.com REST API.



## Overview

The PassTools API enables you to easily create/update Apple's PassBook passes. 
You can code directly to the APIs or use the existing client SDKs we have in the following languages:
* [Java](https://github.com/tello/passtools-java)
* [Ruby](https://github.com/tello/passtools-ruby)
* [Python](https://github.com/tello/passtools-python)


## Fundamental Concepts

The primary concept to understand is that passes are created from templates. 

Passes can then be
* Updated so they they can be updated on an existing iPhone PassBook and later automatically 
through a push notification system (coming soon).
* Delivered through your own systems (emails, as URLs or SMS) to your consumers.

We will then report analytics on the number of installs/uninstalls through the passtools.com UI.



### API Objects

Our API objects are accessed through a REST architecture over https.

####Templates

A template is made up of a header and its hashmap field model.
* The header contains information around the template itself, such as ID, name, description, type (boarding pass, coupon, event..).
* A field is a a multi-value object identified by a key name. It represents an element of the pass such as "label", "value" , "change message" on update, etc...
* The "template model" is a hashmap for the fields representation of the pass. Its key is the field key name and its value is the fied multiple attributes.

####Passes


### Security


## API Doc

The detailed API documentation can be found [here](https://github.com/tello/passtools-api/wiki/Methods).


