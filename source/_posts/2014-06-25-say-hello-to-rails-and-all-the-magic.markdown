---
layout: post
title: "Say hello to rails and all of it's magic!"
date: 2014-06-25 12:20:36 +0000
comments: true
categories: 
- Ruby
- Rails
- Tealeaf Academy
- MVC
- Web Development Career
---

{% img /images/roads-22.jpg %}

I'm through the first week of course 2 with Tealeaf Academy (Rapid prototyping with Ruby on Rails) It's been very demanding to say the least, but still very fun and engaging.  There was a lot of information to absorb and I learned a lot.

Before week 1 officially started, I was asked to read this [Getting Started with Rails guide](http://guides.rubyonrails.org/getting_started.html). I did actually get through it and build the example project, but by the end I wasn't very confident about Rails, which is ok, because that's what the course is for.
<!--more-->

The first lecture in the course cleared a lot of things up for me. Ruby on Rails (or RoR) is basically split up into 5 main parts and follows a MVC  (Model View Controller) pattern:

### The five parts are:

  1. The Router
  2. The Controller
  3. The Model
  4. The Database
  5. The View

## Here is my quick explanation of  how rails works:

  1. A HTTP request comes into the **Router**
  2. the router directs that request to the **Controller**
  3. depending on what is in the request, the **Controller** will do 1 of 3 things
    - redirect to the router **Router** 
    - render a **View** template 
    - or reach into the **Model**. The **Model** can then retrieve data from the **Database** , send that back to the  **Controller**, and then render a **View**
      

####Here is a nice diagram of rails:

{% img /images/request_response_mvc.jpg %}

### This part of the course focused mostly on the Model layer

Here is what a simple model looks like in Rails

```ruby 
class Post < ActiveRecord::Base
end
```

Every model in Rails corresponds to a table in the database. The above model would belong to a table named 'posts'. Rails has several conventions for naming models, classes, tables, and lots of other things. This is what allows the "Rails Magic" to happen. For a model three naming conventions must be followed.

  1. the name of the model file must be singular, lowercase, and snake case. So the Post model would be in a file called 'post.rb'. A 'PostCategory' model would be in 'post_category.rb'
  2. the name of the model class should be singular and CamelCase. ex: 'Post', or 'PostCategory'
  3. the name of the table must be  plaural form, and snake case. ex: 'posts, or 'post_categories'

Figuring out the name Rails expects can sometimes be tricky, so there is a built in method you can use in rails console to figure those tricky ones out. Check out the code below in rails console.

```
> "Goose".tableize
=> "gooses"
```

The model name here is Goose. Calling the `tableize` method on the string "Goose" tells you rails expects the table to be called 'gooses'. The model file for this would be goose.rb .

To create tables in Rails there is a great built in feature called **_migrations_**. To create a migration you first run this command in termianl in your project directory

```
$ rails generate migration create_gooses
```

In this example gooses is the table name. If you wanted to make a posts table you would just replace gooses with posts.  This will create a file in the `db/migrate` directory that looks like this:


```ruby
class CreateGooses < ActiveRecord::Migration
  def change
    create_table :gooses do |t|
    end
  end
end
```

Now lets give gooses a name, height, and timestamps columns.

```ruby
class CreateGooses < ActiveRecord::Migration
  def change
    create_table :gooses do |t|
      t.string :name
      t.integer :height
      t.timestamps
    end
  end  
end
```

  1. t.string :name (creates a column called name with a type of string)
  2. t.integer :height (creates a column called height with a type of integer)
  3. t.timestamps creates two column (created_at and updated_at) Rails automatially fills these in when records are created or updated. Pretty neat right!

After you finish creating your migration file you run this command in your terminal

```
$ rake db:migrate
```

If you have bundler installed you might need to run

```
$ bundle exec rake db:migrate
```

This will create the table in your database, and you never have to write a single line of SQL, now that's awesome!

####gooses table

<table class="table">
  <tr>
    <th>id</th>
    <th>name</th>  
    <th>height</th>
    <th>created_at</th>
    <th>updated_at</th>
  </tr>  
  <tr>
    <th>&nbsp;</th>
    <th>&nbsp;</th>
    <th>&nbsp;</th>
    <th>&nbsp;</th>
    <th>&nbsp;</th>
  </tr>
</table>

As you can see above, the rails automaically added _id_ , _created_at_, and _updated_at_ columns.

<p>Now that we have a table set up all we have to go is create a model to go with it. Remember, the model is there to get data out of that table. Here is what the _Goose_ model will look like .

```ruby Goose Model
class Goose < ActiveRecord::Base
end
```

I know there's not much to that, but it's all you'll need to interact with the gooses table. There are 2 things to remember when creating this model.

  - the file name must be singular and in snake_case 
  - the class name must be singular and in CamelCase

This model will give the entire application access to several getter and setter as well as other methods for objects created from the Goose class. And several methods that can be used on the Goose class. Some examples are:

  1. goose.name
  2. goose.name = 
  3. Goose.first
  4. Goose.find(2)
  5. Goose.new(name: 'fred', height: '10')


In this post I talked a little about the MVC pattern in rails, the flow of Rails, creating tables with migrations, and models. In the next post I'll talk about model associations. 
