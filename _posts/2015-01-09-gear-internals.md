---
layout: post
title: Building GEAR
comments: True
redirect_from: "/2015/01/09/gear-internals/"
permalink: building-gear-internals
---

So back to GearSystems, you might wonder what do we do in GEAR? This question has made us get motivated with hell lot of ideas and features. As a team, we did some gathering and discussed upon what exactly are we solving when the GEAR takes up its shape. There were many ideas flowing in, and obviously we had to let go of few of them, else the timeline to make the GEAR turn would be long and we might get lagging behind with this project forever. 

For if you were a Software Engineer, you would understand that for a project running on self requirements procurement, huge number of ideas might pose a drawback if they aren't filtered and only few of them are taken in based on the *priority* to build the product/service faster.

So, we made filtering of ideas and jotted down all the awesome ones on one sheet and rest of the rejected ones are noted down to be implemented as enhancements. These enhancements shall be added and our systems shall be released with changing version numbers based on the number of additions. We decided that we follow a x.y.z i.e 1.0.0 kind of versioning. So, when a minor enhancement/bug fix/patch is added, the `z` is increased, and when a moderately major enhancement is added, the `y` shall be increased and when a huge changes or major enhancement is added we would change the `x` by one. So, this looked promising for the versioning for us. Github would help us in releasing the versions of our software, after all its a VCS i.e Version Controlling System.

To start building the GEAR system, as a team we had to decide what all things can be bifurcated/segregated into common groups and divide each of them among us. So, major UI/UX part has been taken up by Sudheesh since he has experience in that field. Rahul Jain has been chosen along with Sudheesh to help in structuring and designing.

Me and Rajat started working on modelling the data. We figured out what all models we have to create and what all attributes shall these models contain. We also started working on cluster based analysis of data and apis from google related to maps. We shall soon blog about these proceedings in a detailed way possibly with implementations depending on our free time since the turning of GEAR is requiring more effort from us.


Rahul Yadav has taken up work related to Public Relations and also capturing and processing awesome photographs which we use in our portals and blogs.

Arjun along with Rahul Yadav has been working on structuring surveys which help us in understanding real problems and frame our requirements in an efficient manner. We are building surveys which would serve providing insight upon technical and general problems at hand.

Arjun collaborated with me to bring up blogs. I have configured the present blogs and Arjun has cloned the blogs from the available themes. I have created subdomains on our site and added CNAME records. Sudheesh has committed CNAME files to each of the team members. Overall it was awesome effort by the team in rotating the GEAR.

Stay tuned for the awesome stuff going on in GEAR.