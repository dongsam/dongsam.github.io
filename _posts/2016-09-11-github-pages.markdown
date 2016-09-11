---
layout: post
title: "Creating Github Pages"
description: "Creating Github Pages"
category: Documentation
tags: [github, domain, blog, jekyll]
---

<div id="toc"><p class="toc_title">목차</p></div>


### 공통작업
- [Github](https://github.com/new) 에서 repository 를 하나 생성 후 settings 에 들어간다
![settings](http://i.imgur.com/FgEstu5.png)

## Option 1. Using Automatic page generator
![automatic](http://i.imgur.com/dT7EpNO.png)
- 설정할 Github repository 의 Settings 메뉴로 들어간다
- Automatic page generator 의 "Launch automatic page generator" 버튼을 누른다


## Option 2. Using jeykill

# 도메인 연결 

- 구매한 도메인에 네임서버(서브도메인) 설정에서 A 레코드로 github 주소를 추가한다
![domain_settings](http://i.imgur.com/4AUN6E7.png)
	- A 192.30.252.153
	- A 192.30.252.154
	
- github repository 의 최상단에 'CNAME' 이란 파일을 생성 후 도메인 주소 입력
![setting_domain](http://i.imgur.com/9FERbSu.png)

### Reference
- https://help.github.com/articles/setting-up-an-apex-domain/