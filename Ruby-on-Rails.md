# View (UI)
-.html.erb files can use ruby in html file (executable ruby).  To insert ruby line in html document, use <% [code here] %>, to print ruby line use <%= [code here] %> syntax

-/app/views/layouts/application.html.erb is automatically created by RoR, is used to put boiler plate parts of your application (headers/footers..), it will be used by default; use <% yield %> to show where to put the template pieces

-How to link to a webpage: <% link_to text_to_show, model_instance %>

-index.html.erb lists all info needed (tweets)

-edit links with <%= link_to "Edit", edit_tweet_path(tweet) %>

-delete links with <%= link_to "Destroy", tweet, method: :delete %>
