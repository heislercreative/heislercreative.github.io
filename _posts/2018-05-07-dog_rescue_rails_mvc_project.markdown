---
layout: post
title:      "Dog Rescue : Rails MVC Project"
date:       2018-05-07 04:40:32 +0000
permalink:  dog_rescue_rails_mvc_project
---


To add to the undoubtedly oversaturated number of Ruby programmers' opinions about Rails, let me just say, "Rails is amazing." The ability to create a large-scale MVC app with access to so many helper methods out of the box saves so much time, it's hard to quantify.

For this particular project, we were not allowed to use one of the most potent Rails features, scaffolding. However, it worked to reinforce the concept of limiting code to what's needed and avoiding purposeless myriad files. No one wants a bloated codebase.

My source of inspiration for this project was the current dog adoption process that my wife and I are in. We recently found an 8 year-old West Highland Terrier at a local shelter that rescues dogs from puppy mills. This particular shelter does a great job with building a volunteer community through Facebook, and I wanted to mirror and extend this online functionality via an MVC site.

The app is made up of 5 models:

1. **Users** (shelter admin, staff with basic admin privileges, and volunteers/adopters)
2. **Dogs** (who can be "adopted" by transferring ownership to another user)
3. **Breeds** (created through the new dog form)
4. **Events** (which can be created and attended by any user)
5. **UserEvents** (join table to connect attending users to an event)

The biggest challenge in this project was keeping track of the progression of the various models and ensuring they interacted well together. Dogs and breeds turned out to be the easiest to correlate, while the adding of authentication by level of privilege or permission took things in a more complex direction.

Users in the app have 3 levels, as previously mentioned:

1. **General Users** (volunteers/adopters): These users can use their accounts to adopt a dog, create new events, and attend existing events.
2. **Staff Admin**: Having been granted extra privileges by the Shelter Admin, these users can also add/edit/delete dogs to be adopted, as well as edit/remove Breeds.
3. **Shelter Admin**: By default, the first user signed up has all privileges, including the ability to grant other users admin status or delete them entirely.

In order to put these different users' privileges into action, I set up various methods in the ApplicationController to help with authentication, including **authentication_required**, **admin_authentication_required**, and **shelter_admin_authentication_required**.

Building upon my [Sinatra Project](https://heislercreative.github.io/dermatology_treatment_-_sinatra_app), I also integrated more Bootstrap features to provide a responsive layout with container columns, colored buttons, and warning fields for form validations, errors, and confirmation messages.

To top it all off, Facebook's Omniauth feature was added as an alternative login method to take advantage of the company's security features and ease of use.
