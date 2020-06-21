==
Building Service-Based Atlas Cluster Management
==

Developer Productivity
~~

`MongoDB Atlas <https://www.mongodb.com/cloud/atlas>`__ is changing the database industry standard as per database provisioning, maintenance, and scaling, as it just works. However, even superheroes like Atlas know that with Great Power Comes Great Responsibility.

For this reason, Atlas provides Enterprise-grade security features for your clusters and a set of `user management roles <https://docs.atlas.mongodb.com/reference/user-roles/>`__ that can be assigned to log in users or `programmatic API keys <https://docs.atlas.mongodb.com/configure-api-access/>`__.

However, since the management roles were built for a bride use case of our customers there are some customers who need more fine-grained permission permissions for specific teams or user types. Although, at the moment the management roles are predefined, with the help of a simple Realm service/s and the programmatic API we can allow user access for very specific management/provisioning features without exposing them to a wider sudo all ability.

To better understand this scenario I want to focus on a specific use case of Database user creation for the application teams. In this scenario perhaps each developer/team may need its own user and specific database permissions. With the user roles, Atlas currently offers you will need to grant the team a `Cluster Manager Role` which will allow them to change cluster properties as well as pause and resume a cluster which might be too much for our users.

<div class='callout'>

If you didn't set up your free cluster on MongoDB Atlas, now is a great time to do so. You have all the instructions in this [blog post](https://www.mongodb.com/blog/post/quick-start-getting-your-free-mongodb-atlas-cluster).

</div>


Proposed solution
~~

Our teams will submit their request to a pre-built service which will authenticate them and request an input for the user description. Further, the service will validate the input and post it to the Atlas API without exposing any additional information or API keys.

The user will receive a confirmation that the user was created and ready to use.

Work Flow
~~

To make the service more accessible for users I am using a form-based service called `Typeform <https://www.typeform.com/>`__, you can choose many other available form builders (e.g `Google Forms <https://www.google.com/forms/about/>`__). This form will gather the information and password/secret for the service authentication from the user and pass it to the Realm webhook which will perform the action.


.. image:: /img/DrawingFlow.png
   :height: 100px
   :width: 200px
   :scale: 50%
   :alt: Flow diagram
   :align: right
   
 The user fills the form and security information.
.. image:: /img/InputForm.png
   :height: 100px
   :width: 200px
   :scale: 50%
   :alt: Input Example
   :align: right
   
 Webhook backend
 ~~
.. figure:: /img/webhookDecl.png
   :scale: 50%
   :alt: Webhook declaration

   The main part of the Realm application is to hold the Atlas API keys and information as private secure secrets
 

