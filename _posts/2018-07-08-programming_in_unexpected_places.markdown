---
layout: post
title:      "Programming in Unexpected Places"
date:       2018-07-09 01:42:48 +0000
permalink:  programming_in_unexpected_places
---

After 4 months of dedicated study, I took a month-long break from programming. Or at least that's what I thought.

I work in healthcare administration for a dermatology clinic, and this year we switched from the EHR (Electronic Health Records) application we've used since 2009 to an alternate company. Since our "go-live" date was mid-May and my overtime hours were starting to ramp up, I figured it would be a good time to pause my studies at Flatiron and perhaps prevent all my hair from instantly greying.

It didn't take long, however, to realize that my coding background was about to come in handy.

The new platform we switched to prides itself on being highly customizable. Since each practice and specialty is different, there's not a one-size-fits-all solution for everyone. However, this also means that clients get access to an overwhelming ***mountain*** of complicated features out of the box.

Still, those features weren't quite producing the end results we were looking for. Our in-house dermatopathologist (who analyzes and diagnoses skin specimens) in particular requires a fair amount of data to create pathology reports, such as:
* Collection Date
* Ordering Provider
* Method of obtaining specimen
* Location (on the body)
* Clinical correlation (what the provider thinks the diagnosis could be)
* Specimen size
* Etc.

The EHR uses what they call "templates" to gather and persist data into hundreds of SQL databases. Templates are essentially layout views with forms and buttons, not unlike creating forms in Ruby or Javascript. Their pathology template had the very basics, but we needed more functionality.

Coding to the rescue! While the templates are created and edited through a proprietary editing program rather than a pure programming language, the process is very similar:
1. Create visible fields with ID names to receive input.
2. Use conditional logic to control application flow (with operators like `!=`, `&&`, `||`).
3. Add "triggers", essentially functions that fire on a click or other input.
4. Persist data to the database and update the template view to reflect changes.
5. If buttons are included to generate documents, parse the data for output through macros.

While using the form fields and triggers to capture data for the generated doment was fairly straightforward, the challenge came in determining where to *persist* and then *retrieve* the data for future use in the template. The EHR software uses hundreds of SQL databases, so I tracked down exactly which worked best and which columns to repurpose for our use.

![](https://preview.ibb.co/fBT0CT/Template1.jpg)

Once I established where to persist data, I set up triggers to fire upon submitting the form. I then set up triggers for retrieving the data upon selecting an entry from the orders table (top of template). Finally, I updated the triggers and document macros to display the data in a more human-readable form.

![](https://preview.ibb.co/jQKU6o/Test_Path.jpg)

The end result? A lot of initial effort, but also the payoff of a smoothly functioning dermatopathology lab. In the end, it's all about leveraging the power of programming to make work easier and smarter.
