---
layout: post
title: "Setting up Nitrous.io for Ruby on Rails development"
date: 2014-08-30 15:44:51 +0000
comments: true
categories: nitrous.io ruby rails development environment
---

Nitrous.io provides a great alternative for Ruby developers who are on Windows. In this post I'll share my setup for using nitrous with Ruby and Ruby on Rails. 

The main reason I use Nitrous is because I'm on Windows, and as you probably know, Ruby development on Windows is quite a pain. There is another great benefit to Nitrous though. You will be able take your development box with you to any machine with an internet connection. I mostly switch between 2 computers, so having one development environment that I can use on any computer is a huge plus.

## My Nitrous development workflow

* Sublime Text 2
* Nitrous desktop
* Github
* any browser

That's it. That's all you need to work with Nitrous on your computer

Now I'm going to walk you through setting up your development environment from start to finish

## Go to Nitrous.io and get your box

* Go to https://www.Nitrous.io/ and sign up for an account. It it's free and super easy. 
* Once you're signed up, go ahead an log in. You'll see a big green button **"Open Dashboard"**, go ahead and click it. 
* They will ask you to pick a template, we're doing Ruby on Rails, so you'll click that. They also have templates for Node.js, Python/Django, Go, and PHP. We don't have to worry about them, but it's nice to know they're there. 
* you can give your box a name or leave the one they choose for you. 
* pick your region
* they also have an option for downloading a Github repo, but you should leave this blank. You can download you're repos from the command line once you get your box running.
* the next screen is "Get More N2O". N2O is like credit for upgrading your box. You can use it to add more memory or storage. There are a few things you can do on this page, "Connect GitHub", "Connect Google", etc.. You can do these if you like, or just click next.
* the next page just has some info about using Nitrous on the web, or locally with a text editor. Just go to the bottom and click **"Okay, Take Me to my Box!"**

##Using your Nitrous box

The first thing you will see after setting up and going to your box is the Web IDE(integrated development environment). There are three main sections to the Web IDE

* the files pane(on the left)
* the editor(on the right)
* the console(on the bottom)

{% img /images/IDE.jpg %}

In the files pane there will be a **workspace** folder already set up. This is an important folder because it's where all your files go that are synced with your desktop. (more about that later). There is also a nice readme file in there with some info on getting set up. This web based editor is nice, but if you like to use your own editor, like sublime, you'll probably get tired of using the web IDE pretty quickly. There's one more thing I want to show you before we set up Nitrous desktop. 

Click on the boxes link in the upper right corner of the screen

{% img /images/boxes_link.jpg %}

This will take you to your boxes dashboard

{% img /images/dash.jpg %}

You can always get back here by clicking on the **Boxes** link, or the **Open Dashboard** button on the Nitrous home page. 

Here you can see information on you box, how much memory it has, storage, your SSH URI, Preview URI, and Public Key. You can access the IDE and Terminal here. You can also adjust your box setting here. The settings allow you to add memory and storage, but you need to purchase N2O to do that.

This is a good spot to set up your public key with github. This is necessary to push and pull code from Github, which you will hopefully be doing a lot! 

### Linking your box to Github with your public key

This step is super easy. You do need to have a Github account. If you don't have one yet,go create one at https://github.com

On the dashboard click the link that says **Reveal Public Key**

{% img /images/public_key_link.jpg %}

This will create a public key. Click on the scissor icon to copy it to you clipboard.

{% img /images/copy_key.jpg %}

Now go to your Github account. Go to your settings

{% img /images/github_settings.jpg %}

**Inside of settings**

* click on **SSH keys** on the left side
* click **Add SSH key**
* give your key a title, it could be something like "Nitrous-ruby-box"
* past the key you copied from the Nitrous dashboard in the Key box

{% img /images/adding_key.jpg %}

That's all there is to it. Now you can access your github account from your Nitrous box.

### Setting up Nitrous desktop

Go to the Nitrous home page and click on desktop. You can also visit https://www.Nitrous.io/desktop#windows to go directly to the Nitrous Desktop page. It's available for Windows and Mac. I haven't tried out the Mac version, but it probably works much like the Windows version.

Go ahead and download and run the application for your operating system. Once you get it set up it will ask you to log into your Nitrous account. After logging in it will give you a message saying you need to register a SSH key with Nitrous.io . If you already have a SSH key set up on your computer there will be a button to register it with Nitrous, if you don't have a SSH key, there will be a button to generate one and register it with Nitrous. Go ahead and take the appropriate action. After that you'll see the desktop application. It should look like this

{% img /images/Nitrous_desktop.jpg %}

Here is a rundown of the Nitrous desktop app from top to bottom

* **Boxes** - this is a list of all the boxes you have on your account. When the box is running there will be a green dot next to it. When it's down there is s red dot. When it's restarting or shutting down there is a yellow dot
* **Shut Down and Restart** - these are pretty self explanatory. 
* **memory, storage, region, stack** - this is just info on the specs for your box
* **SSH URI** - you can use this to access your box via an SSH client like putty. 
* **File Sync** - toggle file synchronization on and off. This is what will allow you to work in your local text editor. More on this later
* **Port forwarding** - this allows you to add ports so you can view your Rails and Sinatra apps in your local browser
* **IDE button** - this will open a browser window with the Nitrous web based IDE
* **Shell button** - this will open a terminal window with an instant connection to your box

### Accessing your local Nitrous folder

Go headed and click the **File Sync** button to enable syncing with your local Nitrous folder. Once it's synced up it should say **Monitoring**

{% img /images/monitoring.jpg %}

Nitrous gives a shortcut to your local Nitrous folder. To get to it go to the Nitrous tray icon, right click, and choose **Open Nitrous Folder...**

This folder should be located at `C:\Users\YourUserName\Nitrous` . In here you should see a folder with the same name as your Nitrous box. Any files you put in this folder will go into the **workspace** folder on your remote Nitrous box. **This is important, because it's easy to put files outside of the workspace folder when you're working in the command line, and you won't have access to them on your local machine**
 
To clarify this , lets assume your box is called **my-ruby-box**. When you open your Nitrous folder, you'll see a folder inside of there called **my-ruby-box**. You need to create all your files and projects inside of there. You can work on these in you local text editor (like sublime) and keep them synced up with your box. Every time you save a file Nitrous automatically syncs with your box. If you ever need to sync manually just click the **Sync Now** button on Nitrous desktop.

{% img /images/sync_now.jpg %}

### Working with the terminal window

You can open a shell connection with your box by clicking the *Shell* button

{% img /images/terminal.jpg %}

As I said before, all the files in your local Nitrous folder will be in the remote *workspace folder*, so you need to do `cd workspace` to got to them. 

For example:

* I'll create a file called `test.rb` in my local Nitrous folder and put some ruby code in there. I'll just put `puts 'hello Nitrous box user!'` in it.
* I'll save it and it will automatically sync with my box
* now in the terminal I'll navigate to the workspace folder `cd workspace`cd
* I can do a `ls` command to see that the file is actually there. Here is a screenshot, just to show you
  - {% img /images/ls_command.jpg %} 
* now I can run my ruby file

```
action@beefy-harrenhal-69-141781:~/workspace$ ruby test.rb
=> hello Nitrous box user!
```

Nitrous comes with git, ruby, rails, and heroku toolbelt already set up. 

### installing ruby gems

{% img /images/versions.jpg %}

NOTE: You can install ruby gems on your Nitrous box just like you do on any other machine. Just run `gem install <some_gem>`

### working with Rails and Sinatra apps in your local browser. 

Nitrous desktop uses port forwarding to run apps on your local machine.

* rails uses port 3000
* sinatra uses 4567
* shotgun uses 9393

You need to add any port you want to use for web development to the port list. Here's how:

* Turn on the port forwarding switch
{% img /images/turn_on_port_forwarding.jpg %}

* add a port
{% img /images/add_port.jpg %}

Windows firewall will prompt you about network access. Check both boxes and click ok.

* Now you can go to the command line and run your app. You will now be able to access your app in a local browser at `locolhost:9393` You will change the port from 9393 to what ever port your app is runiung on. So if you're running a rails app it will probably be `localhost:3000`. 

**Here I'm starting up a rails app**
{% img /images/starting_rails_server.jpg %}

**Here it is running in the browser**
{% img /images/browser_running_app.jpg %}

**and you can see port 3000 in the port forwarding list on Nitrous desktop**
{% img /images/3000_in_the_list.jpg %}

That should be all the info you need to get going with basic Ruby and Ruby on Rails development with Nitrous. If you aren't doing TDD, then the information above is enough to give you a good workflow. If you are doing testing you'll want to continue reading below. 

## TDD'ing with Nitrous with Rspec, guard, and spring

If you're going to doing TDD in you Nitrous box you'll quickly realize it can get pretty slow. This is becase every time you make a change to your code and save, Nitrous has to sync your changes before you can run your test. This can take up to 10+ seconds to save, then another 10+ seconds for your tests to run. Guard and spring speed this up considerably and make TDD with Nitrous a lot more enjoyable. You need to be on rails 4 to use spring, but that's what Nitrous comes with, so it wont be a problem.

Here's how to get it set up. Note, I got this information from [Girders blog post](http://girders.org/blog/2014/02/06/setup-rails-41-spring-rspec-and-guard/)

You need these 3 gems in your Gemfile

* [rspec-rails](http://rubygems.org/gems/rspec-rails) - The RSpec testing framework with Rails integration
* [spring-commands-rspec](http://rubygems.org/gems/spring-commands-rspec) - Adds rspec command for spring. Includes a dependency for the [spring](http://rubygems.org/gems/spring) Rails application preloader.
* [guard-rspec](http://rubygems.org/gems/guard-rspec) - The Guard file watcher for running rspec

Add these to the development and test group in the Gemfile of your project

```ruby
group :development, :test do
  gem 'spring-commands-rspec'
  gem 'rspec-rails'
  gem 'guard-rspec'
end
```

Run bundler to install the gems

```
$ bundle install --without production
```

**Set up spring**

Run  `spring binstub --all`. 

```
$ spring binstub --all
* bin/rake: spring already present
* bin/rspec: generated with spring
* bin/rails: spring already present
```

This does the configuration to let spring work with rspec. More info here http://girders.org/blog/2014/02/06/setup-rails-41-spring-rspec-and-guard/

**Set up guard and Rspec**

NOTE: if you already have Rspec set up skip the first line below and just do `guard init`

NOTE: you may need to run `bundle exec guard init` instead if just `guard init`

NOTE: you will need to sync your files manually from Nitrous desktop to open them on your local machine for editing

```ruby
$ rails g rspec:install
      create  .rspec
      create  spec
      create  spec/spec_helper.rb
$ guard init
11:32:14 - INFO - Writing new Guardfile to /Users/username/src/myapp/Guardfile
11:32:14 - INFO - rspec guard added to Guardfile, feel free to edit it
```
Now we have to tell guard to use the spring runner when using rspec. Edit your Guardfile and change the command for rspec to spring rspec. The Guardfile will be in your main app directory right next to the Gemfile.

Change this line:

```ruby
guard :rspec, cmd: 'bundle exec rspec' do
```

to

```ruby
guard :rspec, cmd: 'spring rspec' do
```

### Start up guard and do TDD on your Nitrous box

To start up guard and spring just run the `guard` command from your project directory. You might need to do `bundle exec guard`. This will watch your app for changes and starts up the `spring rspec` command for when you're working with anything related to your test suite.

```
$ bundle exec gurd
23:18:45 - INFO - Guard is using TerminalTitle to send notifications.
23:18:46 - INFO - Guard::RSpec is running
23:18:46 - INFO - Guard is now watching at '/home/action/workspace/punch-clock'
[1] guard(main)>
```

If you need to change something basic in your app, such as adding a gem, updating a local dependency that could be cached, you need to restart both guard (Ctrl-D at the console) (or a server or console process), and spring (spring stop). Restarting guard will restart spring as well, with your dependencies reloaded.

### One last tip I want to share for doing TDD with Nitrous and guard. 

Every time you save a file Nitrous has to sync up your local file with the remote. It can take a little time to do this, so it would be nice to know what's going on. Nitrous desktop has a nice little tray icon that shows a little refresh symbol wile the synchronization is in progress. I like to drag this out to my task bar so I can see it. Normally you would have to click the little up arrow on the right side of your task bar to see the icon, nut you can drag this down to the taskbar so it's always visible.

{% img /images/tray_icon_1.jpg %}

After dragging to taskbar

{% img /images/tray_icon_2.jpg %}

Here's what it looks like while it's syncing your files

{% img /images/while_synching.jpg %}

This part isn't essential, but it does make developing with Nitrous just a little bit nicer. 

## Conclusion

I hope this post takes some of the pain out of setting up a Ruby development environment with Nitrous. It takes a little time to get used to, but it's a great solution for windows users. They also have a lot of team collaboration features that I've never even looked in to. Another nice thing is the tech support is fantastic. I've only have a handful of issues with the service, but they usually get resolved very quickly. 


hhh