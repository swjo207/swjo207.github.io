---
layout: post
title: "Study: Rails 설치하기"
comments: true
description: "Rails 설치하는 법"
keywords: "ruby, rails"
---

## TOC 
1. Installation
  - 1.1 ruby installation
  - 1.2 rails installation
  - 1.3 mysql installation
2. First project 

## 1. Installation

[Ref](http://guides.rubyonrails.org/v4.2/getting_started.html) 

### pre-requisite 
- OS
  - Ubuntu 14.04 or 16.04 
- RUBY 
- RAILS 
  
### 1.1 ruby installation
- install the dependent packages on ruby 

```
sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev nodejs
```
- install ruby via RVM

```
sudo apt-get install libgdbm-dev libncurses5-dev automake libtool bison libffi-dev
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
curl -sSL https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
rvm install 2.4.0
rvm use 2.4.0 --default
ruby -v
```
- install bundler

```
gem install bundler
```

### 1.2 rails installation
- nodejs (for javascript runtime) 

```
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install -y nodejs
```

- install rails

```
gem install rails -v 5.1.1
```

### 1.3 mysql installation
- install mysql server, client

```
sudo apt-get install mysql-server mysql-client libmysqlclient-dev
```

## 2. First project 

### create a project 
```
rails new myapp
```
### use mysql 
```
rails new myapp -d mysql
```
### create database 
- specify username/password at config/databse.yml file
```
cd myapp
rake db:create
```
### run server 
```
rails server
```


