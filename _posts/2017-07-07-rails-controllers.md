---
layout: post
title: "Study: Rails-Controller"
comments: true
description: "Rails Controller"
keywords: "activerecord"
---



## 일반사항 
### Naming Convention
- CamelCase 스타일로 클래스를 정의 
### Method and Action
- 기본적으로 ApplicaitonController 에서 상속 받는다. 
- URL 명령어로 입력을 받아, routes 를 통해 어떤 Controller 가 작업을 수행할 지 정하며, routes 의 파싱 결과(액션)에 따라 클래스 메소드를 실행하도록 액션이 매핑된다. 
- routes 에서 위임할 때 해당 컨트롤러의 인스턴스가 생성된다. 
- public 영역으로 제한된 메소드만 액션으로 호출할 수 있다. 
### Session
### Cookie
### Filters
### Request Forgery Detection
### HTTP Authentication


## 참고 
### class ApplicationController < ActionController::Base
- protect_from_forgery
- before_filter
- default_url_options
- 
### class [Component]Controller < ApplicationController
- index
- create
- new
- show
- edit 
- update
