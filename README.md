# Active Storage Overview


## What is Active Storage?
Active storage is an easy, built-in rails service that provides integration to your local disk and popular services like S3, Azure and Google Cloud.

## Setup 
Make sure you have Rails 5.2 (AT LEAST!) before starting. Run the command: <br>
```
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

```
# config/environments/development.rb

config.active_storage.service = :local
```
