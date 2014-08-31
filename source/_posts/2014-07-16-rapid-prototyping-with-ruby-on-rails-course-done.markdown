---
layout: post
title: "Tealeaf - Rapid prototyping with Ruby on Rails cousre done!"
date: 2014-07-16 16:10:36 +0000
comments: true
categories: 
- Ruby
- Rails
- Tealeaf Academy
- Rouby on Rails Projects
- Web Development Career
---

{% img /images/postit.jpg %}

It's been a few weeks since I last posted about my journey to becoming a Ruby on Rails developer through <a href="http://gotealeaf.com">Tealeaf Academy</a> . At this point I'm done with their second course "Rapid Prototyping with Ruby on Rails" . This blog post is actually my final assignment for the course. I have learned to build a basic rails app from start to finish and I've even been able to apply some custom features that weren't discussed in the course. <!--more-->

Here is the final project http://shielded-retreat-9536.herokuapp.com
Here is my code on GitHub - https://github.com/doug7410/postit-app

#### I've learned way to much to go into detail about everything so here is a summery of all the things I learned while building this rails application.</h4>

  - Model View Controller
  - Rails Migrations
  - Active Record
  - Active Record Associations
    - 1 to Many Associations
    - Many to Many associations
    - Polymorphic associations
  - RESTful routes
  - Custom Routes
  - ERB templates
  - User Authentication with "has_secure_password"
  - Helper Methods
  - Modules
  - Creating a Gem
  - Rails flavored AJAX

I'm probably leaving some things out, so I might have to go back and edit that list. In my [last post](http://dsp-websolutions.com/portfolio/2014/06/25/journey-to-ror-developer-part-3) I talked about MVC and Rails Migrations. Now I'll talk a little about **Active Record** and **Associations** .

###What is Active Record?

Active record is an ORM (Object Relational Mapping system).  Active Record allows Rails to interact with a database and and also stores information about the relationships between tables in the database. All with out ever writing SQL.This is really incredible if you ever had to write SQL to interact with a database! Active Record completely eliminates that whole layer of thinking.

Here's a simple example of the power and convenience of Active Record. Here is a simple table and it's model.

**dogs table**(tables are always named in plural form)

<table class="table">
  <tr>
    <th>ID</th>
    <th>Name</th>
    <th>Weight</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>1</td>
    <td>Rocky</td>
    <td>15</td>
    <td>5</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Gump</td>
    <td>45</td>
    <td>11</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Jenny</td>
    <td>35</td>
    <td>9</td>
  </tr>
</table>

**Dog model** dog.rb (model names are always singular)

```ruby
class Dog < ActiveRecord::Base
end
```

Notice the Dog class is completely empty aside from the fact that it inherits from ActiveRecord::Base. The Dog class now has access to all the Active Record methods. If we wanted to select a row form the dogs table you can do so like this in rails console. 

```
irb> dog = Dog.first
=> <Dog id: 1, name: "Rocky", weight: "15", age: "5">
```

This would return the first record in the 'dogs' table. Active record has many other methods for returning rows form a table. Let's say we wan't the dog with an ID of 2

```
irb> dog = Dog.find(2)
=> <Dog id: 2, name: "Gump", weight: "45", age: "11">
```

 Active Record also creates getter and setter methods for every column in the database table. So you can do things like this. 

```
irb> dog.name
=> "Gump"
irb> dog.age
=> "11"
irb> dog.age = 12
=> 12
irb> dog
=> [id: 2, name: "Gump", weight: "45", age: "12"]
```

Active record makes working with data a breeze. If we had to write SQL just to do the few examples I have above it would take way more code and would be way less pretty. 

###The other great thing about Active Record is Associations

Associations are used to create relationships between tables. There are 2 ways tables can be related

- 1 to Many
- Many to Many


####Here is another table that can relate to the dogs table:

**owners**

<table class="table">
  <tr>
    <th>ID</th>
    <th>Name</th>
  </tr>
  <tr>
    <td>1</td>
    <td>Frank</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Rachel</td>
  </tr>
</table>

In this example we're going to say a dog has one owner, and an owner can have many dogs. This a a typical one to many relationship. The Dog and Owner models will look like this. 

**Dog model**

```ruby
class Dog < ActiveRecord::Base
  belongs_to :owner
end
```

**Owner model**

```ruby
class Owner < ActiveRecord::Base
  has_many :dogs
end
```

Doing this will require one column to be added to the dogs table. A foreign key of `owner_id`

**dogs table**

<table class="table">
  <tr>
    <th>ID</th>
    <th>Name</th>
    <th>Weight</th>
    <th>Age</th>
    <th>owner_id</th>
  </tr>
  <tr>
    <td>1</td>
    <td>Rocky</td>
    <td>15</td>
    <td>5</td>
    <td>1</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Gump</td>
    <td>45</td>
    <td>11</td>
    <td>1</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Jenny</td>
    <td>35</td>
    <td>9</td>
    <td>2</td>
  </tr>
</table>

Rails will automatically know to use `owner_id` because we stated in the Dog model that a dog `belongs_to :owner` . The foreign key column always goes in the table on the `belongs_to` side of a relation. 

Now we can do things like this. 

```
irb> dog = Dog.find(2)
=> <Dog id: 2, name: "Gump", weight: "45", age: "12">
irb> dog.owner.name
=> "Frank"
irb> owner = Owner.last
=> <Owner id: 2, name: "Rachel">
irb> owner.dogs.first.name
=> "Jenny"
```


So that's a little taste of what active record can do and how classes can be associated. 

Here is a great reference for all Active Record - http://guides.rubyonrails.org/active_record_basics.html

Rails uses a lot of conventions to make all of this magic work, but if you can remember them you can be very productive!
