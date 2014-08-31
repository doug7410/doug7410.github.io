---
layout: page
title: "Week 3 Notes from Tealeaf Course 3"
date: 2014-08-14 14:44
comments: true
sharing: true
footer: true
---
##Structural refactor

Candidate for refactor
  - You can think about some business logic
  - be careful about putting business logic in controllers
  - instead put them in the model

##Skinny Controller Fat Model

Moving logic from the controller to the model is the most common refactor in rails

assumes model has most responsibility

http://www.weblog.jamisbuck.org/2006/10/18/skinny-controller-fat-model

##Fat controllers in the wild

example project - redmine
example project - chiliproject

Both projects have very fat controllers

By pushing most of the logic to the models it is much easier to understand waht is going on in the app
also it makes it possible to test the individual pieces of logic in isolation

**Notes from assignment**

**NOTE:** To update an attribute with out validation use this syntax

review.update_column(:rating, new_rating)

**NOTE:** To create a record and bypass validatoin use this syntax

```ruby
review = Review.new(user: user, video: video, rating: new_rating)
review.save validate: false
```

##Rspec Macros

create a new directory in spec called support
`/spec/support`

Any file in the support folder will automatically load when you run rspec

create macros folder in that support folder
`/spec/support/macros.rb`

inside there create the macros

```ruby
def set_current_user
  john = Fabricate(:user)
  session[:user_id] = john.id
end
```

Now you can use this in the test

```ruby
describe TodosController do
     before { set_current_user }

     #tests go here
end
```

To create a macro that finds the signed in user

```ruby
def current_user
  User.find(session[:user_id])
end
```

Now if you need to use the current user in a test you can do this

`bob = current_user`

This way you could use `bob` in your tests

##Shared Examples

create a macro to sign out the user

```ruby
def clear_user
  session[:user_id] = nil
end
```

You can use this is spec that require the user to not be signed in

```ruby
it "redirects the user to the root path if they are not signed in" do
  clear_current_user
  get :index
  response.should redirect_to root_path
end
```

This spec might be needed for several controller actions `INDEX`, `UPDATE`, `CREATE`, etc..

Respec has a way to share this code with those actions

Create a new file  `/spec/support/shared_examples.rb`

```ruby
shared_examples "require_sign_in" do
  it "redirects to the front page" do
    response.should redirect_to root_path
  end
end
````

In the controller spec you can replace 

`it "redirects the user to the root path if they are not signed in" do`

with 

```ruby
context "not signed in" do
before do
  clear_current_user
    get :index
  end
  it_behaves_like "require_sign_in"
end
```

It would be better to have the code in the `before` block included in the shared example. The problem is that the action `get :index` will be different depending on where the shared example is used. This is how the shared example would look if the `before` block code was included. 

```ruby
shared_examples "require_sign_in" do
  it "redirects to the front page" do
    clear_current_user
    get :index
    response.should redirect_to root_path
  end
end
````

To make this work, you have to get rid of the `get :index` and replace it with something that can inject the required code

```ruby
shared_examples "require_sign_in" do
  it "redirects to the front page" do
    clear_current_user
    action
    response.should redirect_to root_path
  end
end
````

In the spec file

```ruby
context "not signed in" do
  it_behaves_like "require_sign_in" do
    let(:action) { get :index }
  end
end
```

The let block will assign the code `get :index` to the `action` variable`, which can be used in the shared example!

To make this even cleaner you can get rid of the context block

```ruby
it_behaves_like "require_sign_in" do
  let(:action) { get :index }
end
```


The documentation for the shard examples are at 
https://www.relishapp.com/rspec/rspec-core/v/3-0/docs/example-groups/shared-examples

                    






