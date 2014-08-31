---
layout: post
title: "Ruby on Rails project - Punch Clock App"
date: 2014-07-16 22:45:21 +0000
comments: true
categories: 
- Ruby
- Rails
- Web Development
- Rouby on Rails Projects
---

{% img /images/punch-clock.jpg %}

So I'm done with week 2 of the Tealeaf Ruby on Rails course and I've learned to do basic CRUD ( create, read, update, delete) actions using Rail's resourses , models, form helpers, and views.

I thought this would be a good time start on a side project I had saved in my back pocket. This would be a good chance to practice what I've learned as well as start my own project. The idea is pretty simple, it's called "Punch Clock", for now at least. It allows you to create different jobs or tasks, and then track the time you spent working on them. Here  the Github repository <!--more-->

https://github.com/doug7410/punch-clock

####The image above is what it looks like so far.


You can also click on the Job Title's  to see that job's detail's page There you will see a list of all the punches you've made. Each punch out has the "time on the clock" next to it. So if you punch in at 8:00AM and punch out at 10:35AM, that punch will show your time like this "0002:35:00" . You just worked for 2 hours and 35 minutes! Go take a coffee break!

The page will also show the total time worked on that job. Here's a screenshot of the ** job detail page **.

{% img /images/punch-clock2.jpg %}

** So far my list of features for this app are: **

  - You can create jobs
  - each job has a title and  description
  - each job has punches
  - each punch "out" uses the previous punch "in" to calculate the time on the clock
  - each job has a running total of all the time worked

That's it for now. Here is a list of what I want to add on

  - add user authentication
  - use javascript to have running clocks
  - add notes to each punch so you can keep track of what was done during that time period
  - have the ability to edit or delete punched
  - be able to manually add punches
  - ability to edit jobs and user profiles
  - add hourly rate to jobs to keep track of earnings
  - add reports to break down time worked by day, month, date-range, etc..

That's all I have for now, but there are lots of possibilities with this.  I also want to have a nice graphic design, but that's not as important as the MVP right now.

If you have any suggestions or questions please leave in the comments. Thanks!