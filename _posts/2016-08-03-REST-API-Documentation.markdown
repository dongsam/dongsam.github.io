---
layout: post
title: "Tools for REST API Documentation"
description: "Tools for REST API Documentation"
category: Documentation
tags: [REST, modeling, API, Documentation, TDD, Agile]
---

<div id="toc"><p class="toc_title">목차</p></div>

## 서문
회사에서 REST API 모델링, 문서화 등을 어떻게 하면 효율적일까 서베이 한 흔적을 두서없이 남겨놉니다. 아직 모두 사용해보진 못했지만 몇개 사용 및 리뷰 후 실제 도입한 후 경험도 추후 업데이트 할 계획입니다.

## swagger
* 에디터
    * http://editor.swagger.io/#/
    * 로컬에 editor 깔아서 사용 가능(오픈소스)
    * 팀단위 개발은 안됨, file 을 공유해서 import 해서 확인해야됨 
    * 테스트 가능
* format
    * yaml
    * json
* ui 에서 별도로 파일 yaml 혹은 json 임포트하면 더 상세하게 사용 가능
* 서버에 직접 깔아서 관리 필요

## apiary ( api blueprint )
* format
    * api blueprint
    * swagger
* 오픈소스인 api blueprint 포멧 
* 웹 에디팅과, interactive API문서화
* mock server 제공 
* 에디터
    * 웹 기반,
    * ex) http://docs.pgv5.apiary.io/#reference/code-api/example
* public 으로는 무료지만 private 하게 팀단위 작업은 유료
    * 10명 기준 99$
* 쓰다보니 web 기반이라그런지 버벅이고 느려지는 부분이있음, 웹말고 에디터에서 수정하는게 나아보임

## RAML
* http://raml.org/
* editor
    * API Designer 를 독립설치형, 웹기반으로 제공 ( 오픈소스 )
        * 팀단위 개발은 안됨, file 을 공유해서 import 해서 확인해야됨
    * 상업용 서비스로 제공 
        * https://anypoint.mulesoft.com/apiplatform/
    * API Workbench
        * Atom 기반으로 작성, 테스트 가능
        * http://apiworkbench.com/docs/
* 계층형 uri 명세 가능 
* format
    * yaml과 유사한 형태의 RAML

## apidoc
* http://apidocjs.com
* 코드 기반으로 주석을 통해 문서화 내용 명시  
* 독립적으로 웹 서버 제공
* 버전별 비교 가능

## sphinx
* Python 문서화 라이브러리, 
* 코드 기반으로 주석을 통해 문서화 내용 명시,  Html 생성
* rest api 용이 아니다보니 단순 문서일 뿐이지 api 에 대해 실질적인 테스트와 명세는 불가능

## 소감
apidoc, sphinx, swagger(inline) 와 같이 코드 상에 규칙에 따라 정의 후 자동으로 문서를 생성해주는 방법은, 문서화만 하기엔 좋지만, API를 개발에 들어가기 앞서 모델링하거나 App, Frontend 단에서 API 를 요청하기 위한 포멧으로는 부적절하여, swagger(editor), apiary(api blueprint), RAML 중 선택하는것이 위 사안을 고려해보면 좋아보임

### Reference
- https://www.slideshare.net/mobile/brotherjinho/restful-api-64494716
- http://www.mikestowe.com/blog/2014/07/raml-vs-swagger-vs-api-blueprint.php
