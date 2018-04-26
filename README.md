# rails-sample-ActiveStorage

ActiveStorage Sample Code

## Refelence

[Active Storage の概要 \| Rails ガイド](https://railsguides.jp/active_storage_overview.html)

## Prep

```
$ rails active_storage:install
$ rails g scaffold user name:string
```

## Model

```
# app/models/user.rb
class User < ApplicationRecord
  has_one_attached :avatar
end
```

## Controller

```
 def user_params
   params.require(:user).permit(:name, :avatar)
 end
 ```
 
 ## View
 
 ```
 # app/views/users/_form.html.erb
 
<div class="field">
  <%= form.label :avatar %>
  <%= form.file_field :avatar %>
</div>
 ```
 
 ```
 # app/views/users/show.html.erb
 
 <% if @user.avatar.attached? %>
  <p>
    <strong>Avatar:</strong>
    <%= @user.avatar.filename %>

    <% if ( @user.avatar.filename.to_s =~ /\.jpeg$|\.jpg$|\.png$/ ) %>
      <br>
      <%= image_tag @user.avatar, size: '100' %>
    <% end %>

  </p>
<% end %>
 ```
