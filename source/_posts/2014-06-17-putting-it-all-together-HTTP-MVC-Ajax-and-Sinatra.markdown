---
layout: post
title: "Putting it all together. Web development with Ruby, HTTP, Ajax , MVC with Sinatra"
date: 2014-06-17 12:20:36 +0000
comments: true
categories: 
- Ruby
- Tealeaf Academy
- Sinatra
- MVC
- AJAX
- Web Development Career
---

{% img http://www.duskyswondersite.com/wp-content/uploads/2014/07/North-Queensferry-Fife-Scotland-by-David-Cation.jpg %}

I just finished up [Tealeaf Academy](http://www.gotealeaf.com) course 1 of 3 . It's has been an outstanding learning experience! I feel like I've come really far as a programmer, and I can take on small projects in Ruby on my own. When I say small projects I mean a simple program that doesn't require a database (databases are in course 2), like a game. I've done blackjack and tic-tac-toe, so I guess the next game could be something like checkers or hangman. If you have any ideas feel free to leave them in the comments. Maybe we could collaborate on a game or other small project. It might be a fun side project.

Anyway....here's a recap of what I've learned since my last post. Here is the [Blackjack Game](http://infinite-waters-7065.herokuapp.com) I made while learning all of these things. <!--more-->

## HTTP

The heart of web development is HTTP. It's a stateless protocol for communicating between distributed systems.  In the case of web development it's usually a server and a client (browser). [This article](http://code.tutsplus.com/tutorials/http-the-protocol-every-web-developer-must-know-part-1--net-31177) goes into detail about HTTP.

## Sinatra

Sinatra is a lightweight MCV framework for ruby. Below is a diagram of the MVC arcitecture.

{% img /images/sinatra.jpg %}

In Sinatra , HTTP request are handled via routs. Routs are stored in controller, then depending on what the rout does, either a template is rendered or the request is redirected to another rout. You can read the Sinatra documentation [here](http://www.sinatrarb.com/intro.html).

## Helper methods in Sinatra

Sinatra gives you the ability to create helper methods. These can be used in the controller and view templates. These are really handy for cleaning up your code and re-factoring.

## AJAX

Ajax uses javascript to reload a section of a page without having to reload everything on the page. Below is an example of a simple ajax function with jQuery.

```javascript A simple AjAX call with jQuery
function player_hits(){
$(document).on("click", "form#hit_form input", function(){ 

$.ajax({
type: "POST",
url: "/game/player/hit"
}).done(function(msg){
$("#game").replaceWith(msg);
});
return false;
});
}
```

Course one has been challenging and I spent a LOT of time on it. I built 3 versions of  the Blackjack game.

  1. [command line - procedural](https://github.com/doug7410/tealeaf_course_1/blob/master/blackjack.rb)
  2. [command line - Object Oriented](https://github.com/doug7410/tealeaf_course_1/blob/master/OO_blackjack.rb)
  3. [web based procedural with Sinatra](http://infinite-waters-7065.herokuapp.com)

I feel like I've come a long way, but I know it's just the beginning. My next post with be about Ruby on Rails!