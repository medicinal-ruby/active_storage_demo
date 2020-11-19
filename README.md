# Active Storage Overview [![Generic badge](https://img.shields.io/badge/EASY-YES-FF00FF.svg)](https://shields.io/)


## What is Active Storage?
Active storage is an easy, built-in rails service that provides integration to your local disk and popular services like S3, Azure and Google Cloud.

## Setup 
Make sure you have Rails 5.2 (AT LEAST!) before starting. Run the command: <br>
```ruby
bin/rails active_storage:install && bin/rails db:migrate
```
Navigate to ```config/storage.yml``` and confirm the yml file replicates this one:

```yml
#config/storage.yml

local:
  service: Disk
  root: <%= Rails.root.join("storage") %>

test:
  service: Disk
  root: <%= Rails.root.join("tmp/storage") %>

amazon:
  service: S3
  access_key_id: ""
  secret_access_key: ""
  bucket: ""
  region: "" # e.g. 'us-east-1'
```
This tutorial, we will be using the disk locally for some image uploads. Double check your development enviorment that we are writing to our local disk:

```ruby
# config/environments/development.rb

config.active_storage.service = :local
```

We can now scaffold our Photo resource to create an upload form to test Active Storage!
<br><br>

```ruby
rails g scaffold Photo description:text 
```
then run the db migrations 
```ruby
rails db:migrate
```
## Active Storage 

The important thing is to add the ```has_one_attached :image``` association in the Photo model. 

Then add the file_upload element to the scaffolded form:
```ruby
  <div class="field">
    <%= f.label :image %>
    <%= f.file_field :image %>
  </div>
  ```
  
 
 Also, add the photo to show up in the show.html.erb file
 ```
 <%= image_tag event.image %>
 ```
 
 Finally, add image to the permitted params in the photo controller
 ```ruby
 def photo_params
  params.require(:photo).permit(:description, :image)
 end
   ```
