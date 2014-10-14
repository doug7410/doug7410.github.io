---
layout: post
title: "Beyonf MVC with rails"
date: 2014-10-14 19:05:06 -0400
comments: true
categories: 
---

---
layout: post
title: "Ruby on Rails - Beyond MVC"
date: 2014-10-12 01:39:18 -0400
comments: true
categories: 
---

# Decorators

We have this method

```ruby
def display_text
     name + tag_text
end
```

The purpose of this method is purely for presentation logic. This method returns the name of a todo plus the tag text which is coming from a private method. We are going to extract this to a decorator.

create  a directory under app called decorators
`/app/decorators`

create new decorator. We want this class to wrap the Todo domain model, so we will initialize with a todo. We can then move the display logic to the decorator 

`todo_decorator.rb`

```ruby
class TodoDecorator
     attr_reader :todo

     def initialize(todo)
          @todo = todo
     end

     def display_text
          todo.name + tag_text
     end

     private
     
     def tag_text
          ..........
     end
end
``` 

Now in the view we can replace this:

```ruby
= link_to todo.display_text, todo
```

With this:

```ruby
= link_to TodoDecorator.new(todo).display_text, todo

```


If we use the decorator a lot we can create a new method in the Todo class like this

```ruby
class Todo < ActiveRecord::Base
     ...........

     def decorator
          TodoDecorator.new(self)
     end

     .................
end
```

And call it in the view like this:

```ruby
= link_to todo.decorator.display_text, todo
```

Often times in complex use we need to access both the methods on the decorator as well as the methods on the original model. We don't want the view to have to remember when to instantiate the decorator and when to go to the original model.  To solve this dilemma go to the controller 

`todos_controller.rb`

```ruby
class TodosController < ApplicationController

     def index
          @todos = current_user.todos
          @todo = Todo.new
     end

     ....
end
```

Instead of passing an array of todos to the view we can pass an array of decorators by changing this:

```ruby
@todos = current_user.todos
```

To this

```ruby
@todos = current_user.todos.map(&:decorator)
```

But then our decorator has to be able to respond to both the methods defined on the decorator and the model itself . To do that we are going to extend the ruby `Forwardable` module, and we're going to define delegaros in the decorator

```ruby
class TodoDecorator
     extend Forwardable

     def_delegators :todo, :name_only?
     ........
end
```

So we're forwarding the invocation of the `name_only?` method on the decorator to the actual Todo model. This way, in our controller we can just pass the decorators to the view, and the view can call methods defined  in either the decorator or on the Todo domain model itself and it will give the right result.

Decorators are valuable when we presist models one way in the databse and we present them differently on the web page. And we can use decorators to define presentation logic to bridge this gap. Becase we're seperating the domain logic from the presentaion logic, we can then test them seperately. So we can have a spec just for the TodoDecorator that tests all the presentation logic on this model that we need to use on the view.

There is gem called draper for creating decorators
https://github.com/drapergem/draper


helpfull methods in draper

* delegate_all - this will pass through all the method calls for the delegator but not define delegaor to the domain model. It also follows the convention over configuration so if you call your decorator `TodoDecorator` it know it goes to the `Todo` model. With decorators you can actually pull a lot of the presentation code in your helpers into decorators if they are centered around one single model. You can also refactor a lot of the ruby in-line code in the view templates into decorators for a cleaner solution. 


## Policy Objects

In this example we have some complicated logic on the `TodosController` `create` action. 

```ruby
def create
  @todo = Todo.new(params[:todo])
  if @todo.save_with_tags
    if current_user.created_at < Date.new(2010,1,1) || current_user.plan.premium?
      new_credit_balance = current_user.current_credit_balance - 1
    else
      new_credit_balance = current_user.current_credit_balance - 2
    end

    current_user.current_credit_balance = new_credit_balance
    current_user.save

    if new_credit_balance < 0
      AppMailer.notify_insuficient_credit(current_user).deliver
    elsif current_user.current_credit_ballance < 10
      AppMailer.notify_low_balance(current_user).deliver
    end

    redirect_to root_path
  else
    render :new
  end  
end
```



