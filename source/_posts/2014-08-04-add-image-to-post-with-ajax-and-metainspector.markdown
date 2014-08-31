---
layout: post
title: "How I added images to my postit app with AJAX and MetaInspector"
date: 2014-08-04 15:07:35 +0000
comments: true
author: Doug Steinberg
categories:
- ruby
- rails
- javascript
- ajax
- web scrapers
- MVC
- Rails Apps
---

In [Tealeaf Academy's](gotealeaf.com) second course [Rapid Prototyping with Ruby on Rails](http://www.gotealeaf.com/curriculum#!rails) we built an app called Postit. It's bassically a clone of the popular site Reddit.com. Of of the featues of this app is to add a URL to the site you are posting about. I decided to add a feature for grabbing an image on that URL. To do this I used some AJAX and a web scraping gem. Here is what the page looks like in action. 

{% img /images/image_scrapper.jpg %}

Here is the link to the actual working app http://shielded-retreat-9536.herokuapp.com/ <!--more-->

Here is the code on GitHub https://github.com/doug7410/postit-app

You'll have to register and create a post in order to try out the image feature.

## Here the rundown on how I did it.

### 1. First add a column to the database for the image

The first thing I had to do was add a `post_image` column to the `posts` table. I went into the console and created a migration.

```
$ rails generate migration add_post_image_to_posts
```
This created the migration file. Below is the file with the code to add the new column.

```ruby 20140711160221_add_post_image_to_posts.rb
class AddPostImageToPosts < ActiveRecord::Migration
  def change
    add_column :posts, :post_image, :string
  end
end
```

### 2. the basic workflow for getting the images from a URL
In this application a post has 5 attributes (not including timestamps). They are:

  - title
  - url
  - description
  - slug
  - post_image
  - user_id

I'm using a web scraper called [metainspector](https://github.com/jaimeiniesta/metainspector) to fetch an array of images from the `url` given to the post. To access the images returned by metainspector I have to take following steps:

1. create a link that sends an HTTP request to a `post_image` action in the post controller
2. that action renders a javascript template
3. that template uses a method which is accessed on the post objecy
3. inside that method, **metainspector** uses the `url` to return an array of images that are on the url's web page
4. a list of images is shown and the user chooses an image for the post

That's the basic outline of the workflow for getting the images. Here is how I did it. 

### 3. The workflow in the UI

I'm using AJAX and a very slick JavaScript interface in the UI to select the image. The workflow in the UI works like this:

  1. when creating or editing a post, the user enters a url in the URL form field
  2. the user clicks on the "Choose Post Image" button
  3. underneath the URL field, a hidden div slides down with all the images generated from the URL
  4. the user clicks on an image to choose it and assign it to the post

Rails has a very easy way to AJAXify a link by adding `remote: true` to a `link_to` helper method. Here is the section of the form with the URL field and the link:

```erb
<div class="control-group">
  <%= f.label :url %>
  <%= f.text_field :url %>
  <%= link_to 'Choose Post Image', post_image_path, remote: true, 
  method: 'post', class: 'btn btn-primary', id: 'choose_img_btn' %>
</div>
```

There are two things about this link use some special rails magic

- `remote" true` 
- `method: 'post'`

`remote: true` turns this into an AJAX link. It's equivalent to writing a JavaScript event handler that process an AJAX call when the link is clicked. 

`method: 'post'` turns the link in to a POST request as opposed to a GET request. 

Both of these are necessary for the next step, the controller action. 

When the user adds a URL to the field and then clicks the "Choose Post Image" button it uses this rout:

```ruby
post '/post_image', to: 'posts#post_image'
```

The link goes to the `post_image_path` , so a click on this link sends a POST request to the `post` controller's `post_image`  action , and because the link has the `remote: true` parameter, the format is JavaScript. 

### 4. what's happening in the `post_image` action in the `post` controller

Here is the action in the controller:

```ruby
def post_image
  @post = Post.new

  respond_to do |format|
    format.js do
      @url = params[:url]
    end
  end
end
```

Here there are 3 things happening. 

- a new @post object is created. This is necessary because the post model has a method that fetches the images. So you need a post object to call that method
- a @url variable is created from the URL field in the form. If you look at the "Choose Post Image" link you probably notice there is no URL parameter anywhere. I used JavaScript to dynamically add the url as a parameter to the link. 
- lastly, the action renders the default template `post_image.js.erb` . Since the request coming into the action is JavaScript formatted, the `respond_to` block sends the request off to the `post_image.js.erb` template.

**I should probably take a step back and show you the JavaScript that added the URL parameter to the link.**
 
```Javascript /app/assets/javascripts/post_images.js
// this makes the "choose image button add the url parameter to the end of the link"

$(document).ready(function(){

  var link = $("#choose_img_btn").attr("href");
  var url = $("#post_url").val();
  
  $("#choose_img_btn").attr("href", link + "?url=" + url );

  $("#post_url").change( function(){
    url = $("#post_url").val();
    var new_link = (link + "?url=" + url);
    $("#choose_img_btn").attr("href", new_link );
  })
});
```

**NOTE:** _to get the code above to work properly I had to add the jquery-turbolinks gem to my gemfile_

`gem 'jquery-turbolinks'`

Basically what this does is append `?url=`  and whatever text is in the URL feild to the end of the link. 

The link by default points to the `/post_image` path. So if you type `www.cnn.com` into the URL field, the link will automatically be turned into `/post_image?www.cnn.com`

### 5. inside the JavaScript template  `post_image.js.erb`

After the response goes through the controller action it ends up in the JavaScript template. This is where all of the cool AJAX stuff happens. Here is what the template looks like.

```Javascript /app/views/posts/post_image.js.erb
var images_html = '<ul class="choose_img_thumbs">';

<% if @post.url_images(@url) != "error"  %>
  <% @post.url_images(@url).each do |image| %
    images_html += '<li>';
    images_html += '<%= image_tag image , id: "url_image" %>';
    images_html += '</li>';
  <% end %>
  images_html += '</ul>'
<% else %>
  images_html += 'You did not enter a valid URL. Please try again.'
<% end %>

$("#images_container").html(images_html);

$("#image_choices").slideDown(function(){

  $("#image_choices img").each( function(){
    $(this).click( function(){
      $("#post_post_image").val($(this).attr('src'));
      $("#image_choices").slideUp();
      $("#post_image").slideDown().html('<img src="' + $(this).attr('src') + '" />');
    });
  });
});
```
**To give you an idea of my though process I'll try to explain what this file does.** 

- It creates an unordered list of images and then places them into a div with the ID of `#images_container` . 
- Once the image list is inside the `#images_container` , that div slides down. Keep in mind this is all happening on the create post or edit post page. 
- After the `#images_container` slides down, the user clicks on an image to choose it and assign it to the post. 
- once the chosen image has been clicked the `images_container` slides up and another hidden div, `#post_image` gets the chosen image inserted into it and slides down.
- there is also a hidden form field `#post_post_images`. The image URL is dynamically added to it's value attriubte.

The important part of this code is `@post.url_images(@url)` . Here is the `url_images` method in the Post model

```ruby /app/models/post.rb
def url_images(url)
  ext = url.split('.').last
  if ['jpg','jpeg','png','gif','bmp'].include?(ext)
    [url]
  else
   begin
     page = MetaInspector.new(url) 
     page.images
   rescue
     "error"
   end
  end
end
```

There are basically 3 cases that can happen in this method

- the URL passed in is an image URL
- the URL is a web page with images on it
- or there is a problem with the URL, in which case the string "error" is returned. 

The first thing that happens is the URL is split apart on the dots (.) . If it's  an image URL like `www.mysite.com/myimage.jpg` the first condition in the if statement will execute and an array with the URL string will be returned.

If that's not the case the URL will be passed into MetaInspector and assigned to the `page` variable. MetaInspector scrapes information from a given URL and gives you several methods for accessing that data. In this case I just want the images. `page.images` returns an array of all the images retrieved by MetaInspector

If MetaInspector has a problem with the URL passed in it will throw an exception and the whole app will fail. To get around this I used a `begin and rescue block`. This way if there are any exception thrown by MetaInspector the method will execute the rescue block and just return the string "error". 

So that's the first thing going on the JavaScript template. The first line is 

```Javascript
<% if @post.url_images(@url) != "error"  %>
```

so as long as there is no error, this section will execute.

```Javascript
<% @post.url_images(@url).each do |image| %
  images_html += '<li>';
  images_html += '<%= image_tag image , id: "url_image" %>';
  images_html += '</li>';
<% end %>
images_html += '</ul>'
```

This creates tan unordered list of images and assigns the list to the `images_html` variable. 

That list is put into the `#images_container` with this code

```Javascript
$("#images_container").html(images_html);
```

Then this part 
```Javascript
$("#image_choices").slideDown(function(){
```
slides down the `#image_choices` and when an image is clicked 3 things happen

- this line `$("#post_post_image").val($(this).attr('src'));` adds the URL of the clicked image to a hidden form input  `"#post_post_image"`
- the `#image_choices` div slides up
- the image is added to the `#post_image` div and it slides down

```Javascript
$("#image_choices").slideDown(function(){

  $("#image_choices img").each( function(){
    $(this).click( function(){
      $("#post_post_image").val($(this).attr('src'));
      $("#image_choices").slideUp();
      $("#post_image").slideDown().html('<img src="' + $(this).attr('src') + '" />');
    });
  });
});
```

### 6. finishing up the feature's workflow

At this pont all that is left is the post has to be saved and the image URL will be added to the `post_image` column. This is because of the hidden form field I talked about. Here is the hidden field in the form.

```ruby
<%=  f.hidden_field :post_image %>
```

Also, just for clarification. Here is the entire post form.

```erb /app/views/posts/_form.html.erb
<div class="well">

<%= render 'shared/errors', object: @post %>
<%= my_form_for @post do |f| %>
  <%=  f.hidden_field :post_image %>
<div class="control-group">
  <%= f.label :title %>
  <%= f.text_field :title %>
</div>
<div class="control-group">
  <%= f.label :url %>
  <%= f.text_field :url %>
  <%= link_to 'Choose Post Image', post_image_path, remote: true, method: 'post', class: 'btn btn-primary', id: 'choose_img_btn' %>
</div>
<div id="image_choices" >
  <h4>Choose an image to go with this post.</h4>
  <div id="images_container"></div>
</div>
<div id="post_image">
  <%= image_tag @post.post_image  %>
</div
> <div class="control-group"> 
  <%= f.label :description  %>
  <%= f.text_area :description, rows: 5 %>
</div>
<div class="control-group">
  <h5>Categories:</h5>
  <%= f.collection_check_boxes :category_ids, Category.all, :id, :name do |cb| %>
    <%= cb.label(class: 'checkbox inline') { cb.check_box(class: 'checkbox') + cb.text } %>
  <% end %>  
</div>
  <%= f.submit(@post.new_record? ? 'Create Post' : 'Update Post', class: 'btn btn-primary') %>
<% end %>
</div>
```

I hope that made some sense and now you have some idea of how I did it. It took a combination of JavaScript, jQuery, AJAX, a scraper gem, and standard rails MVC. I'm sure there are things that can be improved on and tweaked so please feel free to leave feedback. 

Thanks for reading!
