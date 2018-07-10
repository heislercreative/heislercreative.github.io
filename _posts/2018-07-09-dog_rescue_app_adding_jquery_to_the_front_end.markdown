---
layout: post
title:      "Dog Rescue App: Adding jQuery to the Front End"
date:       2018-07-10 03:53:53 +0000
permalink:  dog_rescue_app_adding_jquery_to_the_front_end
---


To build upon my previous Rails app for use by a dog rescue shelter, I was challenged to add jQuery and AJAX front-end functionality and create internal API routes for easy access to data. The switch from Ruby to JavaScript was not entirely new to me, but it was now time to put all the newly learned material into action!

In order to prepare for the use of JSON objects through the internal API, I first generated the AMS serializers for the Dog, Breed, and Event models. All were given additional attributes to serialize, as well as necessary relationships:
```
{
     id: 1,
     name: "Ranger",
     gender: "Male",
     age: 10.5,
     trained: false,
     fee: 200,
     description: "Still a puppy at heart, despite his size.",
     breed: {
          id: 1,
          name: "Golden Retriever"
     },
     user: {
          id: 1,
          name: "Admin"
     }
}
```
I then set up the various controllers to respond as JSON (or ERB views) upon request and got to work on writing the JavaScript portions of the app. For ease of use, and to be able to quickly test and debug in the browser console, I took the route of first writing the script directly in the view and then abstracting it away to the asset pipeline once finished.

In my original Rails app, the partial used to display event information on the index and user homepage gave very limited information (title, date/time, and description). I decided to truncate the description to save space and then add a "More" button to each entry. A quick GET request to the internal API now creates a new JS model object and renders the rest of the description, as well as a list of attending users.
```
$(".event-more").on("click", function() {
    let eventId = $(this).data("id")
    let organizerId = $(this).data("organizer")
    $.getJSON(`/users/${organizerId}/events/${eventId}`, function(resp) {
      let event = new Event(resp)
      event.renderMore()
    })
  })
```
As seen above, the route for the GET request took a little more effort to reach correctly, as events are a nested resource under the organizing user. It ended up being good practice pulling all the necessary data from the Ruby object through the "More" button's data attributes.

Another beneficial functionality of AJAX is the ability to create/edit an object and immediately see it rendered on the page without being redirect. I also set this feature up for the Event object and included the POST and GET request logic in the form partial so it can be used just as well for new events or changes made to existing ones.

In order to meet one of the requirements of the project, I made use of **fetch()** to render the index view of all breeds in the shelter database. At first glance, the page load appeared less responsive than the previous implementation with straight ERB using the Ruby models. This makes sense, though, as the page is fairly static in nature. However, I would certainly use this method again for displaying dynamic content.

In the end, JavaScript (particularly jQuery and AJAX functionality) is all about dynamic user interaction. Now that the app implements some of these features, it's starting to feel more like a modern, usuable site that users have come to expect.

[View the repo on GitHub](https://github.com/heislercreative/dog-rescue-rails)
