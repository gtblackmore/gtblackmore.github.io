---
layout: post
title:      "Building a Dashboard for My Sinatra Project "
date:       2020-04-13 03:15:21 +0000
permalink:  building_a_dashboard_for_my_sinatra_project
---

Many of the lessons in the Sinatra module focus on having separate views for each model. While this made sense for most of the labs, I felt that it would be a poor choice for my project. I thought about many of the webapps that I use every day and what was actually the most user-friendly and secure way to structure my webapp. I ultimately decided that building a dashboard to display all of a user's data on one page and allow CRUD functions to be made from the dashboard.

After a lot of reading and watching videos about sessions, I found that it was much easier to use a dashboard to protect the database. The most important method in the entire application is the `current_user` method:
```
def current_user
      @current_user ||= User.find(session[:user_id]) if session[:user_id]
    end
```

This method looks for a user session by the `user_id` and sets the `@current_user` instance variable to the `session[:user_id]` if there is not already a `@current_user`. The `@current_user` variable is only the first step. In order to ensure that only data that `:belongs_to` the `@current_user` is displayed, proper associations through ActiveRecord are vital.

## Creating the Proper Associations
There are many ways to associate data with ActiveRecord. This specific project only required the `has_many` and `belongs_to` be used. I have three models in my app: `User`, `Property`, and `Entity`. Because we want the dashboard to only display data that `belongs_to` the `@current_user`, we have to properly link each model. Since a `User` is our point of focus, we have to figure out how to logically get information from each other model to be available with `@current_user`. My associations for this webapp look like this:
```
class Entity < ActiveRecord::Base
  belongs_to :user
  has_many :properties
end

class User < ActiveRecord::Base
  has_secure_password
  has_many :entities
  has_many :properties, through: :entities
  validates_uniqueness_of :email
end

class Property < ActiveRecord::Base
  belongs_to :entity
end
```
Let's break this down. A `User` has many `:entities` and it has many`:properties`. Notice that a `Property` does not `belong_to` a `:user`. This is because ActiveRecord specifies a `belongs_to` association as  "a one-to-one connection with another model, such that each instance of the declaring model "belongs to" one instance of the other model."

Since `Property` can only `belong_to` one other model (and I wanted it to `belong_to` and `Entity`), I had to use a `has_many :through` association. This allows ActiveRecord to go through `Entity` to get to a `Property`. As you can see from the models, a `User` `has_many :properties, through: :entities` which allows ActiveRecord to go through the `User`'s `has_many` relationship with the `Entity` model to get the `:properties` that belong to the `User` through the `User`'s association with an `Entity`.

This is the setup that allows a `@current_user` to be able to look at its entities by calling `@current_user.entities` which returns an array of all the entities that belong to the `@current_user`. It also allows us to call `@current_user.properties` which returns an array of the properties that belong to the `@current_user` through the `Entity` model.

## Setting up the Dashboard
I set up a route:
```
get '/users/home' do
    @user = User.find(current_user.id)
    if logged_in? && current_user = @user.id
      erb :'users/show'
    else
      redirect to "/"
    end
  end
	```
	and the corresponding view:
	```
	<body>
        <%= @user.first_name %>'s Properties
        <table>    
          <tr>
          <th>Address</th>
          <th>City</th>
          <th>State</th>
          <th>Zip</th>
          <th>County</th>
          <th>Rent</th>   
        </tr>
          <% @user.properties.each do |property| %>
          <tr>
          <td><%= property.address %></td>
          <td><%= property.city %></td>
          <td><%= property.state %></td>
          <td><%= property.zip %></td>
          <td><%= property.county %></td>
          <td>$<%= property.rent %></td>
          <td><a class="button" href="<%= "/properties/#{property.id}/edit" %>">Edit Property</a></td>
          <td>
            <form method="post" action="/properties/<%= property.id %>">
              <input type="hidden" name="_method" value="delete">
              <input type="submit" class="button" value="Delete Property">
            </form>
          </td>
          </tr>
          <% end %>
         </tr>
        </table>
        <%= @user.first_name %>'s Entities
        <table>    
          <tr>
          <th>Name</th>
          <th>Address</th>
          <th>City</th>
          <th>State</th>
          <th>Zip</th>
          <th>Entity Type</th>
          <th>Phone</th>   
          <th>Email</th>   
        </tr>
          <% @user.entities.each do |entity| %>
          <tr>
          <td><%= entity.name %></td>
          <td><%= entity.address %></td>
          <td><%= entity.city %></td>
          <td><%= entity.state %></td>
          <td><%= entity.zip %></td>
          <td><%= entity.entity_type %></td>
          <td><%= entity.phone %></td>
          <td><%= entity.email %></td>
          <td><a class="button" href="<%= "/entities/#{entity.id}/edit" %>">Edit Entity</a></td>
          <td>
            <form method="post" action="/entities/<%= entity.id %>">
              <input type="hidden" name="_method" value="delete">
              <input type="submit" class="button" value="Delete Entity">
            </form>       
          </td>
          </tr>
          <% end %>
         </tr>
        </table>
```
As you can tell, the `current_user` method is super important. By validating the session and setting that to the `@user` we can access all of that `@user`'s data and display it. Because we're only displaying data that `belongs_to` the `@user` we only give that `@user` the option to see, edit, and delete data that belongs to it. Then we only need to add some basic route protection to each route and we've insulated our data from misuse.
## Final Thoughts
I found this project to be a great experience in the basics of software development. A lot of the labs in the Flatiron curriculum deal with one concept at a time, and this project was a challenge to organize. I know in the future I will devote more time to thinking and wireframing everything before jumping right in. I think I overhauled my code more than once, and it was due to not taking the time to really understand the relationship between all of the models and what I wanted my user to be able to do. 
				
			
