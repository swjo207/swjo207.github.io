---
layout: post
title: "Study: Rails Tutorial 2"
comments: true
description: "Rails Model"
keywords: "rails, ruby, activerecord, model"
---

# Models 

## TOC


## 1. Introduction

### Active Record 
- refer to [Active Record Pattern](https://www.martinfowler.com/eaaCatalog/activeRecord.html) 
- we can simply consider M(Model) is a mapping function, from ORM(class object) to Relational DB table. 

### Naming Convention
- Database Table - Plural with underscores separating words
- Model Class - Singular with the first letter of each word capitalized

### Schema Convention
- **Foreign key**: naming like *singularized_table_name_id (e.g., item_id, order_id)*
- **Primary Key**: by default, use *id* as a primary key
- **created_at**: Automatically gets set to the current date and time when the record is first created.
- **updated_at**: Automatically gets set to the current date and time whenever the record is updated.

## 2. Create a Model 

### subclass *ActiveRecord::Base* class
```
class Product < ActiveRecord::Base
end
```

## 3. Read & Write Data 

### Create 
- using create method of a model class 
  - create and save 
```
user = User.create(name: "David", occupation: "Code Artist")
```
- using new method of a model class
  - only created, use **save** to commit the record to database
```
user = User.new
user.name = "David"
user.occupation = "Code Artist"
```

### Retrieve
- [reference to Query Interface](http://guides.rubyonrails.org/v4.2/active_record_querying.html) 
- methods 
>
bind
create_with
distinct
eager_load
extending
from
group
having
includes
joins
limit
lock
none
offset
order
preload
readonly
references
reorder
reverse_order
select
uniq
where
>
- return a collection with all users
```
users = User.all
```
- return the first user
```
user = User.first
```
- return the first user named David
```
david = User.find_by(name: 'David')
```
- find all users named David who are Code Artists and sort by created_at in reverse chronological order
```
users = User.where(name: 'David', occupation: 'Code Artist').order(created_at: :desc)
```

### Update
- find a record, and modify the data of it, finally commit to database
```
user = User.find_by(name: 'David')
user.name = 'Dave'
user.save
```
- update method 
```
user = User.find_by(name: 'David')
user.update(name: 'Dave')
```
- batch update
```
User.update_all "max_login_attempts = 3, must_change_password = 'true'"
```

### Delete
- find a record and remove it
```
user = User.find_by(name: 'David')
user.destroy
```
