#Ruby on Rails

scaffold- the basic building block for most rails app, gives view to list, edit, create new items.  For rails generate scaffold command, must list field:type where field is variable and type is string, text, integer, boolean, decimal, float, binary, date, time, dateline

database migrations- how we version our database/ keep track of our changes without stepping on anyone's toes.  Migration commands: rename_column, rename_table, drop_table, change_column, change_column_default

REST in Ruby: CRUD Read = get user; Create = post user; Update = put user; Destroy = delete user



## Commands

rails new (creates new rails application)

rails server (runs app on server short-cut alias "s")

rails generate (shows all of the commands)

rails generate model (shows more commands)

rails console (opens up rails console short cut alias "c")

reload! (reloads console, must be done after each time the model txt files are updated)

rake routes (tells you the paths and controller names necessary in you model)

rails generate (generate new code, short-cut alias "g")

rails dbconsole (start a console for the database in config/database.yml shortcut "db")

rake db:migrate (runs all missing migrations files)

rake db:rollback (rolls back to previous migration)

rake db:schema:dump (dumps to current db state)

rake db:setup (creates db, runs schema and seed)

rails g migration (generates migration, can be run with Add<Anything> to <Table name> to have data organized in table, can also specify defaults, limit, first, after, email, null, unique...  can also be run with Remove<anything>from<tablename>)


all commands can be run with -h for more information

### AJAX  
-Creating AJAX links  
How to have link fade out when delete is pressed instead of refreshing browser  
1.) Make the link a remote call 
add , remote_true to link  
2.) Allow controller to accept Javascript request  
add format.js to respond_to block in zombies_controller  
3.)Write the JavaScript to send back to the client  
in zombies/destroy.js.erb write  $('#<%= dom_id(@zombie) %>').fadeOut();
How to have a create zombie field:  
1.) Write the format.js in the controller  
2.) Refactor the view and create the form  
refactor into partial (takout div, put into partial), add render zombie, in views, add  
<%= form_for(Zombie.new, remote: true) do |f| %>  
3.) Create JavaScript  
$('div#zombies'.append("<%= escape_javascript(render @zombie) %>");  
$('div#<%= dom_id(@zombie) %>').effect('highlight');  
Create an AJAX form that can set a custom decomposition phase on the zombie show page.  
1.) Create new custom route for our action  
2.) Define the form  
3.) Create the action in the controller  
4.) Write the JavaScript to send back to the client  


##Models

Scopes help sort out certain demographics and allow symbols to be searched for (zombie.rotting)  
scope :rotting, where(rotting: true) 

Callbacks, define in models; before_validation, after_validation, before_save, after_save, before_Create, after_create, before_update, after_update, before_destroy, after_destroy, can call before_save :method  
example:  def make_rotting  
if age > 20  
self.rotting = true  (use self instead of @zombie because we don't need instance variable because they come from controller; reading attributes doesn't need self, setting attributes needs self)
end  

Zombie Mailer: in terminal run rails g mailer ZombieMailer decomp_change, lost_brain  
then in app/mailers/zombie_mailer.rb create instance variables, can include attachments, then mail to: @zombie.email, subject: 'Your decomp stage has been changed." ... can also include from:, cc:, bcc:, reply_to...  
you can create html emails by changing text file to html, can also create multipart (text and html emails) by making two files  
Remember to update the model to include sending email and include methods previously defined in mailers.deliver.  method can pass self.  Can also run after_save :decomp_change_notification, if :decomp_changed?  
Note: for mailing lists, subscribe, unsubscribe etc. the gem MadMiMi is good.

## View (UI)
-.html.erb files can use ruby in html file (executable ruby).  To insert ruby line in html document, use <% [code here] %>, to print ruby line use <%= [code here] %> syntax

-/app/views/layouts/application.html.erb is automatically created by RoR, is used to put boiler plate parts of your application (headers/footers..), it will be used by default; use <% yield %> to show where to put the template pieces

-How to link to a webpage: <% link_to text_to_show, model_instance %>

-index.html.erb lists all info needed (tweets)

-edit links with <%= link_to "Edit", edit_tweet_path(tweet) %>

-delete links with <%= link_to "Destroy", tweet, method: :delete %>

-partials are how we reuse view code.  Their files start with an underscore

-app = app-specific code; lib = shared code; vendor = 3rd party code; in production these locations get fingerprints (md5 codes) which help to cache/version them because fingerprint only changes when file changes; asset_path will include fingerprint in .erb file

-by default, sassy css is used in rails -- supports nesting css

-You also get CoffeeScript, a programming language that compiles into javascript; can make toggle fields, 

-To precompile all files into /public/assets (on your server) run $ rake assets:precompile   and will minify your code (save loading time)

###Sprockets //=  
-tells application to grab jquery framework and include it all at this point in the file  
//= require jquery   include the jQuery framework JavaScript  
//= require jquery_ujs include Rails specific unobtrusive JavaScript  
//= require_tree /   include all files in this directory  


###Input Helpers  
f.text_area (renders multiline text area)  
f.check_box (used for booleans)    
f.radio_button :decomp, 'fresh', checked: true (radio button)  
f.radio_button :decomp, 'rotting' (radio button)  
<%= f.select :decomp, ['fresh', 'rotting', 'stale'] %> (select box with 3 options)  
<%= f.select :decomp, [['fresh', 1], ['rotting', 2], ['stale', 3]] %> (select box with 3 options, each with a numerical value)  
f.password_field :password (gives dots instead of characters when text entered)  
f.number_field :price (gives number field with up/down arrows)  
f.range_field :quantity (slider bar)  
f.email_field :email (useful on mobile)  
f.url_field :website (useful on mobile)  
f.telephone_field :mobile (number pad on mobile)  
div_for helps display title/body info

## Controllers 

-Control models and views

-rails follows convention over configuration; make sure url, folder, method named appropriately

-remember @ indicates an instance variable

-can require(:tweet) or permit([:location, :status]) if you want to be sure a part is included and other parts are allowed.

-strong parameters are only required when creating or updating with multiple attributes

### Conventions("thing" is the name of your program)

1.) thing_controller.rb 
class ThingController < ApplicationController
def show (maps to show.html.erb; where we typically call our models)
@thing= Thing.find(params[:id]) (pulls out first thing, our action)
render action: 'status' (redirects show method to status.html.erb)
end
end

2.) To be able to respond with Json (or XML)
respond_to do |format|
format.html
format.json {render json: @tweet}

### Controller Actions

def index   List all tweets

def show  Show a single tweet

def new  Show a new tweet form

def edit  Show an edit tweet form

def create  Create a new tweet

def update  Update a tweet

def destroy  Delete a tweet

### Authentication

if session[:zombie_id] != @tweet.zombie_id (session works like a per user hash)
 flash[:notice] = "Sorry, you can't edit this tweet." (flash[:notice] to send messages to the user)
redirect_to(tweets_path) (redirects request)

Also remember to update application.html.erb to include

<% if flash[:notice] %> 
<div id ="notice">
<%= flash[:notice] %>  
<% end %>

note: to make code more dry, create check_auth method and get_tweet method instead of re-creating in each method

## Routes
-routes defined in router in config/routes.rb 

-this means that the url for certain code and methods is defined here

-Custom routes (i.e. two urls for the same page) can be defined by "path" => "controller#action"
resources :tweets
get '/new_tweet => 'tweets#new'

-to link to the custom path: <%= link_to "All Tweets", all_tweets_path %>

-URL can be redirected by get '/all' => redirect ('/tweets')

-Set root path with root to: "tweets#index", can link with root_path

-Nested Routes look like  
resources :zombies do  
  resources :tweets  
end  
and remember to update the controller  
def show  
   @tweet = @zombie.tweets.find(params[:id])  
end

-2 types of custom routes: :member Acts on a single resource, :collection Acts on a collection of resources

- can customize JSON response.  Example: @zombie.to_json(only: [:name, :age])  
can also use except:, include:  
can set default in zombie model, def as_json(options = nil)  
super(options ||
              {include: :brain, except: :created_at)  
end  


### HTTP Status Codes  
200 :ok  
201 :created  
422 :uprocessable_entity  
401 :unauthorized  
102 :processing  
404 :not_found