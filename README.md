# rails-sample-ActiveStorage

ActiveStorage Sample Code

## Refelence

[Active Storage の概要 \| Rails ガイド](https://railsguides.jp/active_storage_overview.html)

## Qiita

[ActiveStorageでアップロードされたファイルのうちブラウザで表示できる画像のみサムネイル表示させる \- Qiita](https://qiita.com/NaokiIshimura/items/d6bbbe5a444879b187a9)

## Prep

```
$ rails active_storage:install
$ rails g scaffold user name:string
$ rails db:migrate
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
  <%= form.file_field :avatar, accept: '.jpeg, .jpg, .gif, .png, .bmp' %>
</div>
 ```
 
 ```
 # app/views/users/show.html.erb
 
<%# ファイルが添付されてるか？ %>
<% if @user.avatar.attached? %>
  <p>
    <strong>Avatar:</strong>
    <%# ファイル名を表示 %>
    <%= @user.avatar.filename %>

    <%# ファイルがの拡張子がjpeg,jpg,gif,png,bmpか？ %>
    <% if @user.avatar.filename.to_s =~ /\.jpeg$|\.jpg$|\.gif$|\.png$|\.bmp$/ %>
    　　 <p>
       <%# 画像ファイルを表示 %>
       <%= image_tag @user.avatar, height: '100' %>
      </p>
    <% end %>

  </p>
<% end %>
 ```
