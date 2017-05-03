---
layout: post
title: "Search Engine Trends" 
description: "Search Engine trends and research status of Naver"
category: Documentation
tags: [search engine, Naver, information retrieval, IR]
---

<div id="toc"><p class="toc_title">목차</p></div>


# 검색기술 트렌드와 네이버의 연구현황

본 내용은 고려대학교 대학원 정보검색론 수업에서 발표된 네이버의 김상범님 세미나에 대한 개인 노트 입니다.


## 검색서비스 flow
- matcher
- ranker
- features

- 검색서비스 중요한 4가지
    - 정확하게
    - 빨리
    - 빠짐없이
    - 공정하게

- 한 국가의 트레픽을 퍼펙트한 검색엔진을 만들 수 있다(사견)
    그걸 사기업에게 몰아주는게 윤리적으로 문제가있기 때문에 국내는 - 불가능했지만
        - 러시아나 중국은 그걸로인해 자사 검색 서비스가 크지않았나 추정



## matching

- 색인(indexing)
    - 1952년에 최초 제안 

- 현재까지는 단어기반 매칭이 주류
    - 형태론적 분석, 동의어 처리가 도전과제,

- semantic matching
    - 네이버에서는 두개의 양방향으로 접근

        - query rewrite


        - document expansion

            - click graph


            - word2vec 과의 analogy, note2vec


            - click graph embedding 기반하여 자동번역기법(SMT/NMT) 기반으로 유사질의 생성 가능
                - 수줍게 넣어보고 클릭이 발생하면 CGE 로 선순환, 발생하지않으면 negative


## ranking
- old approaches
    - BM25
        - 한계효용의법칙
        - 여러 단어 질의에 대한 and/or 제어를 k 값으로 수행( 단어 연속빈도에 대한 가중치 )

    - language model based IR

    - LDA


- 시그널(피쳐)
    - 질의에 있는단어가 얼마나 많이 또 얼마나 많이 가깝게
    - 많은 사람들이 보거나 링크를 걸었나
    - 다른사람들이 어떤 단어로 링크를 걸었나
    - 문서 작성자가 과거에 스팸작성자로 경고받았나
    - 언제 만들어진 문서인가
    - 몇 명이 조회한 문서인가
    - 문서의 제목과 본문의 관련성은 높은가 

- 학습집합
    - 클릭여부와 그 위치
    - last click
    - quick click
    - ...

- learning to rank

- 제작년까진 네이버도 ranking svm 을 썻었음
    - slack variable, 틀린 정도도 모델링
    - c값은 overfitting 을 제어하는 hyperparameter
        - 약간의 오류는 허용해도, general 하게 margin 은 커지게
        - c값 튜닝이 필요


- 평가
    - 필드에선 nDCG 로 평가함 
        - DCG의 normalize
            - DCG는 각 문서별 discounted gain, 높은순위일수록 크게


- GBRT (gradient boosted regression tree)
    - 검색 대상, 쿼리에 따라 점수 부여
    - 무작정 tree depth 를 늘리기엔 overfitting 이 발생하니 트리의 개수를 늘려 여러 tree 를 ensemble


- 일단 샘플데이터로 돌려보고, 괜찮다 싶으면 우리데이터로도 돌려보며 감잡고, 이거다싶으면 개념을 파보고, 코드를 서비스에 적용 


- 딥러닝은 컴퓨터는 어려워하는데 어린애들은 잘만한거에 적용가능
    - 이미지, 등

    - IR엔 적용이 힘들수있음
        - 그래서 최근엔 query와 단어, 결과에 대해 이미지 화해서 적용하는 시도들 있음 
        - 하지만 아직까진 임팩트있는 효과는 있지 않았다.



## 이미지와 텍스트의 만남

- 문서에는 글만 있지않고, 이미지와 함께다보니, 그거에대한 분석, ranking 이 필요

- 이미지와 NLP 와 경계가 허물어지고 있음

- wordnet 리소스에 image 를 붙여나가기 시작하면서 리소스가 생김, 시소러스 

- image Q & A


- bias & variance 딜레마
    - 데이터가 얼마 없으면 simple 한 model 을 쓰는게 나음
    - 데이터가 많을수록 feature, layer 가 복잡해져야 좋은데, 그걸 deeplearning 이 수행

- caffe tool 로 clustering 하여 naver 검색결과에 이미지 tagging 

    - 음식 데이터셋으로 pretrain 후 학습

    - 텍스트는 이미지근처에 공통적으로 같이 등장한 ngram 으로 

- 연예인 timeline


분류, ranking, clustering 에 집중 중 

