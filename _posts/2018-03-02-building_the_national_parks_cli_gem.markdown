---
layout: post
title:      "Building the National Parks CLI Gem"
date:       2018-03-02 23:18:48 -0500
permalink:  building_the_national_parks_cli_gem
---


Moving from test-driven labs to a freeform project is like taking the training wheels off a bike: a bit nerve-racking, but exhilirating once you've got the hang of it.

Living in Colorado, I've become a big fan of our national parks, and although I don't visit them as often as I would like, they made for a great start for this project. I decided to scrape 2 levels down, using both the National Park Service's "Find a Park" map page and the parks list page for each state and territory.

After working through the "Student Scraper" lab, this seemed pretty straightforward. And once I got to the code, I guess it was. The key there is *once I got to the code.*

I had been working through the previous labs on either an iMac or an ancient MacBook which usually does the trick and allows me to study anywhere. However, it turns out projects don't play too nicely with the in-browser IDE and custom repositories, and trying to update Ruby on an outdated laptop is truly a nightmare.  So, a solid weekend of mild meltdowns later, I learned how to set up a local development environment on the iMac, chalked it up as a bonus life lesson, and finally got started.

I had in mind the following flow starting out:
1. Display a list of all 57 states and territories.
2. *User selects a state or territory by number.*
3. Display a list of that state or territory's parks and monuments.
4. *User selects a park or monument by number.*
5. Display the park name, location, and description.
6. Allow the user to move back to previous list views.

Working through Avi's CLI gem walkthrough was extremely helpful in terms of layout and getting the States list running. After that, I realized I was on my own to take the CLI a step further to display the Parks list and then further details.

For the Parks list to function properly by taking in the user input and scraping that particular state's url, I found that a combination of argument-based methods and instance variables worked well to ensure the correct url was passed through every methods called. This approach also rescued me from an error in which the user could return to the States list after viewing more information on a particular park, but couldn't get back to the Parks list for that state.

There is an immense sensation of accomplishment upon seeing a CLI app work without bugs that I had not anticipated. Couple that with learning how to build, submit, install, and then run a gem seemlessly (eventually), and I'm encouraged to keep moving forward in Ruby and development overall!

See the final project code [here](https://github.com/heislercreative/national-parks-cli) and test out the National Parks CLI gem by installing: `gem install national-parks` and running: `national-parks`.
