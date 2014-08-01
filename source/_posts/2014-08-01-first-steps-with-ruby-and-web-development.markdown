---
layout: post
title: "First steps with Ruby and Web Development"
date: 2014-08-01 14:14:11 +0000
comments: true
categories: 
- Ruby
- Tealeaf Academy
- Web Development Career
---

<h3><a href="http://dsp-websolutions.com/portfolio/wp-content/uploads/2014/06/ruby-on-rails-tutorials-3.jpg"><img class="alignnone  wp-image-153" src="http://dsp-websolutions.com/portfolio/wp-content/uploads/2014/06/ruby-on-rails-tutorials-3-300x149.jpg" alt="ruby-on-rails-tutorials-3" width="332" height="165" /></a></h3>
<h3>All I want to do is be a professional web developer, make some money, love what I do, and live happily ever after.</h3>
Not to much to ask right? So where do I start? My journey actually began a while ago and I have some basic knowledge. I know HTML, CSS, some PHP and a little javascrpt. But that alone is not enough to get a job in today's market. Now adays, you need more that that. There are basically two types of web developers.
<ol>
  <li>Front End</li>
  <li>Back End</li>
</ol>
The differences are ilustrated very well in this youtube video. <a href="http://www.youtube.com/watch?v=zXqs6X0lzKI" target="_blank">http://www.youtube.com/watch?v=zXqs6X0lzKI</a>

A <strong>front end</strong> developer deals with what you see in your web browser. The HTML, CSS and Javascript. They do things like design and build sites and user interface.

A <strong>back end</strong> developer deals with the server side scripting, databases, and behind the sceens magic that powers the web. Especially on sites where the user creates the content (like Facebook for example).
<h3>I became interested in back end a long time ago when I learned you can create a site dynamically from a database.</h3>
For example, if you have a site that sells video games, you can have a database with all the games and use it to dynamically create a page for every game in the database, while actually only having to write code for  a single page. Imagine if you have to code up a separate page for every game in your database. And then imagine you have 5000 games! Yikes!<!--more-->

So to me, there is a certain kind of magicall-ness to back end web development. I know it's not as cool as levitating a super model, but it's magical to me. So I know I want to do <strong>back end</strong>, but how do I learn that? At the time of this epiphany(around 2006), the answer to that was to learn <strong>PHP</strong>. I know that was a long time ago, so you must be thinking I'm an expert PHP guy right? Sorry to say, that's not the case.

I used to make sites in Dreamweaver, and Dreamweaver has some built in tools to write PHP for you. So for a long while that's what I did. Which in the end, got me no where because I really didn't know what the heck I was doing. I didn't decide to actually try to learn how to use PHP the right way until about a year ago. I started by watching videos on Lynda.com . They were good, but I was on my own, since Lynda.com didn't really have any instructor feedback or assistance. I got stuck A LOT and kind of gave up on that. Then I discoverd an online school called O'Reilly School of Technology. They happed to have a cirtificate course called PHP/SQL Programming . PERFECT! Right? Well after about a year of doing this course ( with a few little breaks here and there) I didn't feel it's going to make me the <em><strong>modern rockstar developer </strong></em>I am striving to be. There are a few issues I have with them, but I wont go into that here.

Fast forward to a couple of months ago (5/2014). I've come to the conclusion I need a school, with real teachers, and an active commuity of students , AND a cariculum designed to give me the skill set of a <strong>modern web developer</strong>. I found (through a lot of searching) <strong><a href="http://www.gotealeaf.com" target="_blank">Tealeaf Academy shcool for Ruby on Rails Developers</a> !</strong> They offer a four month/ three course program that takes you from zero to Ruby super hero. Now I'm not saying I believe  I'm going to finish the program and then get a job the next day. I know it will take a lot of work after the program is over. You don't get years of experience in four months obviously, but I do think it will give me the foundation to get those years of experience.  So this is where I'm at. I've been doing the course for the last month and I couldn't be happier.

Here is a list of what I've learned so far.
<h3>My time spent learning PHP was not wasted!</h3>
Ruby and PHP are not that different in some ways. They are both programming languages. They use the same concepts. Ruby is just a lot more pleasent to write (in my opinion). My first days with Tealeaf were spent on the pre-course. It's meant to be an introducion to programming and ruby. Since I allready know the bascics of programming, this was pretty easy for me. Ruby has it's own syntax of course, but it's very easy to pick up and very easy to read.

<strong>Here's a line of ruby code</strong>

<code lang="ruby"> cards.each { |card| puts card }</code>

Easy right? Here's the same thing in PHP

<code lang="php">
for($i = 0; $i<count($cards); $i++){
echo $cards[$i];
}
</code>

It's doing the same thing, but the Ruby code is so much easier to read and write, not to mention faster.
</pre>
<h3>Command line</h3>
I finally learned to use the command line! It's really not that hard. The commands I find myself using most are

<ul>
  <li>cd - change directory</li>
  <li>ls - list files in the current directory</li>
  <li>mkdir - make a directory</li>
  <li>touch - create a file</li>
  <li>git - use git to make commits and push to git hub</li>
</ul>

<h3>Git and Github</h3>
If you want to be a modern web developer you HAVE to learn to use Git and Github. Github is used for storing your code and allows you to see all the versions you saved. It also allows teams to work on collaborate on a project and people to download your code to play with it. Very important and very big deal in the web development world.
<h3>Time management for web developers</h3>
I know this has nothing to do with Ruby, but it's worth mentioning. As it turns out there are two kinds of people in the business world. Makers and Managers,  and they need to manage their time differently to achieve maximum efficiency. Managers can do the 9-5 thing and cut up their day into nice little one or two hour chunks. Makers on the other hand need a nice long chunk of time to get something done. They don't do well with interruptions. The more they can focus on their craft, the happier they will be. I know this is true from personal experience. I love having a nice Saturday all to myself to work on a project. Here's an article all about this phenomenon <a href="http://www.paulgraham.com/makersschedule.html">http://www.paulgraham.com/makersschedule.html</a>
<h3>How to build an application from start to finish</h3>
There is a certain workflow to efficiently writing a program . It's very difficult to just start witing code. You need to figure out the logic and then turn that logic into working code. Here is the magic formula.

<ul>
        <li>Come up with requirements/specifications, which will determine the scope.</li>
  <li>Application logic; sequence of steps. Write the logic in psudo code</li>
  <li>Translation of those steps into real code</li>
  <li>Run code to verify logic.</li>
</ul>

<h3>Object Oriented Programming with Ruby (OOP)</h3>
This is a subject that I've been wanting to learn, and struggling with for a long time (in PHP), and I'm happy to say I finally get it. Thanks to Tealeaf and Ruby. The idea is with OOP is you create classes for a program and create objects from the classes. Classes are like blueprints for a house,and objects are like the houses made from the blueprints. There are some important key words in Ruby with OOP.
<ul>
  <li>class - the blue print for objects</li>
  <li>.new - keyword to create new objects</li>
  <li>initialize - this is a special method that is run every time an object is created</li>
  <li>attr_accessor - this creates getter and setter methods for instance variables</li>
  <li>module - modules define behaviors that can be mixed into classes</li>
  <li>include - the keyword for mixing modules into classes</li>
</ul>

There's a lot more to it than that, but those are some of the basics in Ruby OOP Here is an example of a simple class and object

<code lang="ruby">
class Dog{
  attr_accessor :name

  def intialize(n)
    @name = n
  end
}

fido = Dog.new("Fido")
</code>

<h3>This is where I was at after 2 weeks of Tealeaf Academy</h3>
I now have basic knowleghe of Ruby, OOP in Ruby, and I learned some valuable web developent skills such as command line and git. I completes a few projects as well.

<strong>Procedural Blackjack Game</strong> - <a href="https://github.com/doug7410/tealeaf_course_1/blob/master/blackjack.rb">https://github.com/doug7410/tealeaf_course_1/blob/master/blackjack.rb</a>

<strong>Tic-Tac-Toe</strong> - <a href="https://github.com/doug7410/tealeaf_course_1/blob/master/tic_tac_toe.rb">https://github.com/doug7410/tealeaf_course_1/blob/master/tic_tac_toe.rb</a>

<strong>Object Oriented Blackjack Game</strong> - <a href="https://github.com/doug7410/tealeaf_course_1/blob/master/OO_blackjack.rb">https://github.com/doug7410/tealeaf_course_1/blob/master/OO_blackjack.rb</a>

I'm pretty happy with myself. This post is getting pretty long winded, so I'll save week 3 for the next post. Thanks for reading!