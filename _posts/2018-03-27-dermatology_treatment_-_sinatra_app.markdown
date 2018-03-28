---
layout: post
title:      "Dermatology Treatment  - Sinatra App"
date:       2018-03-28 01:26:57 +0000
permalink:  dermatology_treatment_-_sinatra_app
---


For my first foray into making a Sinatra app from scratch, I decided to work with an MVC concept I interact with daily: dermatology treatment. I've worked as a surgery coordinator for a skin cancer surgeon for almost 3 years and have seen the value of being able to easily track patients and their outstanding treatment.

Or rather, I should say that I can imagine being able to easily track patients. In reality, handling results and scheduled appointments for 10 providers and tens of thousands of patients is a much more complex process and requires a robust EHR (electronic health record) system to organize the chaos. Even then, though, it's hard to find a way to get a quick view of who has outstanding treatment and needs to be prioritized.

While rudimentary, my approach starting out was to created 3 essential models:
1. Providers (users who can sign up and manage their patients)
2. Patients (who have basic demographics and a history of various conditions)
3. Conditions (chosen from a list and with details like diagnosis and treatment dates, treatment types, etc.)

I made a perhaps overly-ambitious goal of creating a functioning app over the weekend, which in all fairness, I did accomplish. However, I wasn't completely satisfied with how I originally implented the authentication methods of confirming the provider was logged in and that only that providers patients could be edited by that provider. I found a way to make this work in the erb view but decided that it should ultimately be the *controllers'* responsibility to handle authentication.

So, I started refactoring. **And I broke everything.** Thankfully, reviewing a previous lecture by Avi both inspired and guided me through the frustration of taking a working product, partially destroying it, and putting it back together in a way that felt correct and scalable.

I even took it a step further after releasing the amount of repeat code in my controllers and created simplified helper methods to clean things up, such as:
```
def current_user
      @provider ||= Provider.find_by(username: session[:username]) if session[:username]
end
```
```
def current_patient
      @patient ||= current_user.patients.find_by_id(params[:id])
end
```
```
def current_condition
      @condition ||= current_patient.conditions.find_by_id(params[:cid])
end
```
The end result was functioning code I could be happy seeing and understanding, which is the whole point of it all, isn't it?
