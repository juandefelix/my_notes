DESIGN PATTERNS
===============

**Decorator**: A class that wraps **a single class** and adds functionality methods to it. View code should not be written in the model, should belong to a Decorator.  
**Presenter**: Logic in a view template that doesn't belong to a model, should not be in the controller or in the view. You can extract the logic into a presenter object. If you have so many variables that are available in the view, move them also to the presenter.   

PRY
===

### Pry key bindings  
`pry -r ./path/to/file.rb`: load files  
`cd`: go inside the class or method that you type  
`self`: will display the object you are in as well as the instance variables  
`nesting`: will show the levels of nesting you are in  
`jump-to <number>`: go to the nesting in the <number>  
`exit`: will bring you to the previous nesting level  
`edit_method`: will open the editor in the method that you pass  
`ls`: lists the methods and variables in the current scope (ls -h for help)  
`ls -mj`: only methods in the singleton class.  
`. <shell_command>`: will execute the shell command  
`show-input`: show the buffered input  
`amend-line <number> <some_code>`: edit a line in a buffered input  
`!` : clear the buffered input   
`edit <method>`: opens an editor so you can edit that method.  
`exit-all`: will exit pry  
`a-method;`:will not print on the screen the result of the method  



BUNDLER
=======


`bundle update your_gem` will update only the specified gem.



RUBY 
====

### Ruby Methods  

- **_send_** `object.send("method", "arg1", "arg2")` executes the method in the object with the arguments.  

### Strings

A different way to represent strings:

	<<-STR
	your string here
	also here
	STR

### \_\_FILE__

`__FILE__` (with two underscores) represent the string with the name of the current file

`File.expand_path(“../../Gemfile”, __FILE__)` returns a string of a path that starts in the second argument directory, and will have the structure and name of the first argument.

### Rake (not the same as _rack_)

Rake is Ruby Make, a standalone Ruby utility that replaces the Unix utility 'make', and uses a 'Rakefile' and .rake files to build up a list of tasks.  
In Rails, Rake is used for common administration tasks, especially sophisticated ones that build off of each other.



### Rack (not the same as _rake_)

Rack provides a minimal, modular and adaptable interface for developing web applications in Ruby.  
By wrapping HTTP requests and responses in the simplest way possible, it unifies and distills the API for web servers, web frameworks, and software in between (the so-called middleware) into a single method call.  
read about Rack
[http://chneukirchen.org/blog/archive/2007/02/introducing-rack.html](http://chneukirchen.org/blog/archive/2007/02/introducing-rack.html)

```ruby
# my_rack_app.rb 
require 'rack'
app = Proc.new do |env|
  ['200', {'Content-Type' => 'text/html'}, ['A barebones rack app.']]
end
Rack::Handler::WEBrick.run app
```
Or, you can use the rackup command line tool and avoid specifying details like port and server until runtime:

```ruby
# config.ru
run Proc.new { |env| ['200', {'Content-Type' => 'text/html'}, ['get rack\'d']] }
```  
**Setting RSpec for a small ruby program**  
  1.  Createa a folder. Change directory to that folder  
  2.  gem install bundler  
  3.  `bundle init`  
  4.  Modify the Gemfile created, include gem ‘rspec’  Save the file  
  5.  `bundle install`  
  6.  Create a file inside the spec/ folder with the rspec file  
  7.  Create a folder lib/ and file inside with the ruby program to test  



RAILS
=====

### What happens when you run rails server?

1. The Gemfile is readed  
2. The boot.rb is executed. ENV[“BUNDLE_GEMFILE”] is added with the path to the gemfile.  
3. The application.rb is executed  
4. Rakefile is executed  
5. the correspondent config/enviroments/ id executed  
6. the init files are executed  
7. the routes are readed  
8. environment.rb is executed. There’s a call to initialize! on the app class  
9. config.ru 	There’s a call run the application  



### Middleware

Rack middleware is more than "a way to filter a request and response”.  
Rack middleware is everything between application servers (Webrick, Thin, Unicorn, Passenger, ...) and the actual application, such as your Rails application.  
Any software component/library which assists with but is not directly involved in the execution of some task. Very common examples are logging, authentication  

[http://stackoverflow.com/questions/3217088/what-is-middleware-when-referenced-in-the-context-of-ruby-on-rails](http://stackoverflow.com/questions/3217088/what-is-middleware-when-referenced-in-the-context-of-ruby-on-rails)

`rake middleware` is a terminal command. It displays the classes involved in the middleware.  

### Rails Gemfile  
Reading a gem from a local file  
  `gem "foo", :path => "/path/to/foo”`

from [http://stackoverflow.com/questions/4487948/how-can-i-specify-a-local-gem-in-my-gemfile](http://stackoverflow.com/questions/4487948/how-can-i-specify-a-local-gem-in-my-gemfile)  

### HTTP PROTOCOL- The request and response objects

There are two methods that contains the request from the browser and response from the application.  
They are `request` and `response`. They are methods of `ActivaController::Base` and they both instances of `ActionDispatch` objects.  
The request will contain the parameters, URL, cookie, protocol, etc. You can access to them by calling response.url, `response.headers[cookie]`  
The response will contain the status, content_type, the body, etc. If you want to inspect the body, you have to call the `response.body`   

#### Cookies, Params, Flash, ActionDispatch 

Look like the params, cookie, and flash methods of the controller belong to the ActionDispatch class  


###Active Record  
Interesting Active Record methods:  
- **_new\_record?_** `my_car.new_record?` will tell you if this particular object has been saved in the database.  
- **_pluck_** `User.where(active: true).pluck(:name)` Queries the database, retrieveing the colums asked but it will not instanciate an Active Record object, speeding up the quering process. This is good for large queries. This method is not chainable.  
[http://guides.rubyonrails.org/v4.0.8/active_record_querying.html#finding-by-sql](http://guides.rubyonrails.org/v4.0.8/active_record_querying.html#finding-by-sql)  
- **_try_**  `object.try(:method_or_variable)` won't raise an exception if the object doesn't exist. This is not an ActiveRecord specific method. It is available for all objects in Rails.  


### Application Controller  
The methods in Application Controller will be available to all the controllers.  
They can be called with a filter (before, around or after filter) or they can be called inside the methods in the controller, same as private methods.  
The same private method in different controllers can be refactored in one ApplicationController method.  
An ApplicationController method can deal with setting instance variables like @current_user, etc.  

### Helpers Methods  
Method helpers are available in all views. A helper from one controller will be available in all view template, even from a different controller. So why you should have an Application Helper file?  
Helpers are modules, and basically are a group of methods, so they can be included in other classes.  

### The helper_method in controllers  
If you have a method that might be interesting for views, you can make it available to the views by typing after the class declaration:  
`helper_method :your_method`  

### Rails Migrations  
Check the status of your migrations:  
`rake db:migrate:status`
In order to rollback a migration, type:  
`rake db:rollback STEP=1` to rollback a number of steps.  
`rake db:rollback VERSION=20141013232321` to rollback to a specific migration.  
`rake db:version` you'll get the last migration runned.  

Check the class **ActiveRecord::Migrator** has some methods that you can call to get some information about the migrations:  
`ActiveRecord::Migrator.current_version` will return the current version.  
`ActiveRecord::Migrator.get_all_versions` will return an array with the migrations.  


### Adding API keys and secret to a yaml file in a Rail app  
I'm following this tutorial [http://railsapps.github.io/rails-environment-variables.html](http://railsapps.github.io/rails-environment-variables.html)  
Create a file:  
`config/local_env.yml`   
Add to .gitignore:  
`/config/local_env.yml`  
Add to the file `config/local_env.yml` the following:
  ```FACEBOOK_API_KEY: ‘the_api_key’  
  FACEBOOK_API_SECRET: ‘the_api_secret’  ``` (Don’t forget the quotes, they are important)  
Modify the file `config/application.rb` and add inside the class the following:  
```ruby
config.before_configuration do
  env_file = File.join(Rails.root, 'config', 'local_env.yml')
  YAML.load(File.open(env_file)).each do |key, value|
    ENV[key.to_s] = value
  end if File.exists?(env_file)
end
```
Start the application server typing `rails s` in terminal.  
I had an error `no implicit convertion of fixnum into String` because I forgot the single quotes in the YAML file. Added the quotes and the sever started without problem.  
  
### Configuring a Rails app to use Facebook sign in

First of all: I'm following this tutorial from Rails Casts to do the implementation of facebook: [http://railscasts.com/episodes/241-simple-omniauth](http://railscasts.com/episodes/241-simple-omniauth)  
Creating the application: `rails new facebook_oauth`  
Moving to the directory: `cd facebook_oauth`  
Add the omniauth gem to your Gemfile `gem ‘omniauth’`  
In your terminal, run `bundle`  
Create the file `config/initializers/omniauth.rb `and add
```
Rails.application.config.middleware.use OmniAuth::Builder do
  provider :facebook, 'CONSUMER_KEY', 'CONSUMER_SECRET'
end
```
Substitute the key and secret for the secret and key of your registered application. You’ll need to hide this in the future.  
Starting the server `rails s`
gives the following error: `warning: already initialized constant APP_PATH`  
Commented out the line where the `gem “spring”` is. Run `bundle` in terminal. Now I get another error:  
`Could not find matching strategy for :facebook. You may  need to install an additional gem (such as omniauth-    facebook)`  
Addind gem ‘omniauth-facebook’ to Gemfile. Running `bundle` in terminal. Running `rails s` on the terminal is now working.  
Add to application.html.erb: `<%= link_to “Sign in with facebook”, “/auth/facebook” %>`

### Using Ruby Debugger (now byebug gem replaced debugger)

Based in the RailsCast video [http://railscasts.com/episodes/54-debugging-ruby-revised?autoplay=true](http://railscasts.com/episodes/54-debugging-ruby-revised?autoplay=true).  
This gem works on ruby version 1.9.x only.  
In your Gemfile: gem ‘debugger’, group: [:development, :test]  
In your teminal: rails s  
Set a breakpoint in your code typing debugger somewhere in your code  
In the debugger console:  
`help` lists all the commands  
`help <command>`  shows help on a command  
`list` or `l` shows the code where you are. You have to type it everytime you hit next or step in order to see the code.  
`next` execute the line with the arrow and break on the next line  
`step` stepping inside the next method call  
`continue` Continue the execution  

### Rails Factories (Factory Girl)

[http://railscasts.com/episodes/158-factories-not-fixtures](http://railscasts.com/episodes/158-factories-not-fixtures)  
In the video you will learn how to create a Factory, with sequences, associations and parameters.  
```ruby
Factory.create(:user) # Creates a user with the whole factory
Factory.create(:user, :username => ‘bob’) # Creates the user but passing custom fields
Factory.create(:user) # saves it to the database
Factory.build(:user) # doesn’t save. Works in memory only
Factory.attributes_for(:user) # doesn’t save. Works in memory.
Factory(:user) # same as Factory.create(:user)
```

GIT
====  

### Creating a repo  
- Create a new repo on Github WITHOUT adding a .gitignore or a README.
- Then, Github will show some terminal commands to:
	- Create a new repo from the command line
	- Push an existing repo
Use the commands you need. If you decide to push an existing repo, make sure the repo exists. and you have the changes committed.  
If not, you can create it by typing ‘git init’ in the project folder, then add the files to the staging area with `git add -A` and then commit it with `git commit -m ‘message’`



### Git Fetch  
In you local repo there are some branches called “Remote Tracking Branches” and you can access them typing  
`git branch -r`  
You can not checkout to this branches. When you fetch, you ask to bring to this branches the changes made in the correspondent remote and branch repo.  
In orger to integrate these changes to you local repo you have to merge them. You can do this by:  
```
git checkout your-branch
git merge remote/branch
```
(slash between the remote and branch)  

### Merging locally  
- Typing in your local repo `git merge <local branch>` will merge your local current branch with the local branch provided in the command.  
- Your current local branch will merge the changes if there’s no conflict, but the branch you merged will remain untouched.  

### Which files have a conflict?  
`git status` will give you the answer.  

### Pushing to a remote repo from a local one  
- When you push to the remote master, it gets merged in your remote master branch every time.  
- When you push to a different remote branch like `git push origin other-branch`:
	- the first time a pull request will be created.  
	- if the pull request is accepted, the changes in that branch will merge to master. You have the option of deleting the branch.  
    If you don’t, the branch will be part of the remote repo and your commits will show up in the branch.  
	- future commits to this branch will be pushed to the branch with no pull request. You can merge these changes to master clicking the pull request button.  

### If you forgot to add a file before commiting  
-Add the file to the staging area  
`git add -A`  
-Then type:  
`git commit --amend -C HEAD`  
Your file will be added to the last commit.  

### Amending the commit message  
`git commit --amend`  Will open your editor, allowing you to change the commit message of the most recent commit.  
Additionally, you can set the commit message directly in the command line with:  
`git commit --amend -m "New commit message"`   
[http://stackoverflow.com/questions/179123/edit-an-incorrect-commit-message-in-git](http://stackoverflow.com/questions/179123/edit-an-incorrect-commit-message-in-git)  

### Renaming local branches  
`git branch -m <oldname> <newname>`  
If you want to rename the current branch, you can simply do: `git branch -m <newname>`  

### Checking out a previous commit  
First you have to commit all your changes. Otherwise git will complain.  
Then type: `git checkout number_of_commit`  
To go back to the tip of the branch you were, you will have to type: `git checkout branchname`  

### Git diff  
In general, it will show you the differences between comits.  
`git diff <filename>`
will show the difference in that file between the staged file and the same file in the working directory  
`git diff <remote> <branch>`  
will show the difference between your local branch and the remote branch  

### Git log  
Will show a list of the recen commits.  
Only one line per commit `git log --oneline `  
Only n commits	`git log -1`  
It shows the differences `git log -p`  

### Unstaging files  
When you want to unstage files, type: `git reset HEAD <filename>`  
To clear the whole staging area, type: `git reset`  

We are assuming that we have a file in the staging area.  
`git rm --cached <filename>` will unstage the file but i'll keep it in your working directory.
`git rm -f <filename>` will unstage the file and it will erase from your working directory.

  


UNIX
====
### Looking for a word inside your directory  
`grep -nr <yourString> <your directory>` e.g.   `grep -nr binding.pry ./app/controllers`

### Writing content in a file
`echo "my content" > file.txt

SUBLIME
=======  
#### Macros  

**_ctrl + q_**  to start/stop recording the macro  
**_ctrl + mays + q_** to execute the macro. In sublime you can execute it with different cursors.  

#### Divide the screen in groups

**_command + alt + num_**    Divide the screen vertically  
**_command + alt + mays + num_**    Divide the screen horizontally  

#### Tabs, Groups  
**_ctrl + alt_**  Move between the tabs  
**_ctrl + num_**  Move between the groups  
**_command + num_**  Move between the screens in a group  
**_ctrl + shift + num_**  Move a tab to a group  



OTHER
=====



### Design Patterns  

[http://sourcemaking.com/design_patterns](http://stackoverflow.com/questions/179123/edit-an-incorrect-commit-message-in-git)  

### Topics to research  

Unix: the pipe, using regular expressions  
Rails: Html protocol, Caching, Middleware, Capybara, Selenium, Dir.  
Active Record: Transactions.  
Git: rebase, interactive commit, cherry pick  
Other: ITerm, System Preferences/Keyboard/Shortcuts/Keyboard  



**PORO**: Plain Old Ruby Object
