# View (UI)
-.html.erb files can use ruby in html file (executable ruby).  To insert ruby line in html document, use <% [code here] %>, to print ruby line use <%= [code here] %> syntax

-/app/views/layouts/application.html.erb is automatically created by RoR, is used to put boiler plate parts of your application (headers/footers..), it will be used by default; use <% yield %> to show where to put the template pieces

-How to link to a webpage: <% link_to text_to_show, model_instance %>

-index.html.erb lists all info needed (tweets)

-edit links with <%= link_to "Edit", edit_tweet_path(tweet) %>

-delete links with <%= link_to "Destroy", tweet, method: :delete %>

# Controllers 

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
<div id ="notice><%= flash[:notice] %>
<% end %>

