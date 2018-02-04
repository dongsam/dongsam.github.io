---
layout: post
title: "How to get Ethereum without mining and buying"
description: "개발자가 마이닝, 구매 없이 이더리움을 얻는 방법들"
category: Documentation
tags: [Ethereum, Blockchain, Bitcoin, ETH]
---

<div id="toc"><p class="toc_title">목차</p></div>

# 개발자가 마이닝, 구매 없이 이더리움을 얻는 방법들

안녕하세요 dongsamb 입니다. 

저는 작년부터 이더리움 등 블록체인 기술에 관심을 가지고 연구하며, 현재는 스타트업에서 Ethereum 을 이용하여 Blockchain Backend 를 개발하고있습니다. 

블록체인을 통해 중개자를 없애 수수료를 낮추면서도 신뢰를 가지는 계약이 가능해지고 DAO(Decentralized autonomous organization), ICO, Crypto Economic 등 새로운 개념에 의해 현재의 중앙화된 많은 서비스들이 탈중항화되어 재개발되는 시기가 올 것이라 기대하여 블록체인 분야의 개발로 뛰어들었고, 이미 하루하루 주변에 많은 회사와 서비스들이 생기는 것을 목격할 수 있었습니다. 

## 발단

그러던 중 최근에 재미있고 기분 좋은 제의 메일을 받았습니다. 이더리움과 같은 Crypto Currency 가 정말 화폐로서 국경없이 글로벌하게 실제 비지니스에서 사용이 시작되었구나를 피부로 느끼게 해주었는데요, 그 내용은 아래와 같습니다.

![](http://i.imgur.com/g9oc43C.png)



Join 시 10 ETH 를 선지급해주고, 일당으로 0.5~2 ETH 를 지급, 현재 1ETH 가 약 100만원이라는 점에 있어서 꽤나 매력(?)적인  제안입니다. 

최근 블록체인 및 스마트컨트랙의 기술 베이스의 많은 시도들이 기하급수적으로 생기며, 개발 수요가 공급을 못따라가는 현상이 생기다보니 조금 이라도 Github 에서 주요 블록체인 오픈소스에 Contribution 한 개발자들에게 여러 제의들이 빗발치는것으로 보입니다. 



![](http://i.imgur.com/sLaB4q2.png)



저 또한 간단하게는 typo 나 잘못된 code convention 수정부터, Bug 나 Issue 해결을 위주로 조금씩 Ethereum, Bitcoin 등의 오픈소스에 Contribution 을 해오고 있었는데요, 실제로 2주에 한 번꼴로 위 같은 메일을 받을 수 있었습니다.  

위 같은 제의가 개발자들에게 매력적인 점은 대부분 remote 로 communication 하며 세계 어디에서든 팀에 참여하여 근무할 수 있고, 간단히 ETH 를 통해 그 보수를 받음으로써 복잡한 환전 및 해외송금의 과정을 생략할 수 있다는 점입니다.

물론 보수로 받은 ETH는 추후 필요시 국내 거래소를 통해 원화로 판매 후 해당 수익에 대해 소득신고를 해야겠지만, 싫기만 했던 한국의 김치(?) 프리미엄이 감사해지는 순간도 올지도 모르겠다는 생각도 드네요 :)

해당 포스트에선 이같은 offer 없이도 자발적으로 참여하여 이더리움 등으로 보수를 받을 수 있는 서비스들에 대해 정리해 보았습니다.

## Gitcoin [(https://gitcoin.co)](https://gitcoin.co)


![](http://i.imgur.com/0nbFkz5.png)

![](http://i.imgur.com/FPVrf70.png)

Gitcoin 은 Github 에서 개발되는 Open Source Software(이하 오픈소스) 의 Issue ( Bug, Feature, etc ) 에 현상금(Bounty) 을 ETH 를 통해 걸 수 있고, 해당 Issue 를 해결한 개발자가 해당 Bounty 를 가져갈 수 있게 함으로써 오픈소스 재단이나 팀, 후원 단체, 개인 등이 오픈소스 개발 활성화를 위해 Funding 을 할 수 있게 되며, 오픈소스 개발자들은 Job 없이도 오픈소스 개발 참여만으로도 ETH 를 통한 수익을 낼 수 있는 플랫폼입니다.



![](http://i.imgur.com/noBXnRP.png)

[issue explorer](https://gitcoin.co/explorer) 를 통해 실제로 어떤 오픈소스 프로젝트의 이슈들에 얼마의 ETH Bounty 가 걸려있는지 볼 수 있음으로써 많은 개발자들이 오픈소스에 참여할 수 있도록 유도할 수 있습니다. Gitcoin 은 현재 Consensys 에 Pilot Project 로서 Join 하여 진행되고 있으며, 그런만큼 Ethereum 관련 오픈소스 프로젝트 위주로 Bounty 가 진행되고 있는것을 볼 수 있습니다. 



![](http://i.imgur.com/tlUIC5d.png)



또한 실제로 해당 Github Issue 페이지에 gitcoinbot 이 Bounty 의 상태를 알려줌으로써 Github 서비스와 자연스럽게 융화되는것을 볼 수 있는데요, 위 같은 큰 이슈에 대해서는 하나의 이슈에 여러 개발자들이 참여하기도 하며 그럴 경우 아래와 같이 기여한 양에 따라 여러 개발자가 Bounty 를 나눠가져가기도 합니다.  Issue 해결에 참여한 개발자들은 해당 Bounty 에 Claim 을  걸어 자신의 참여에 대한 검증과 보상을 요구하는 절차를 가질 수 있으며, 이같은 모든 절차는 MetaMask 나 Mist, Parity 같은 브라우저형 이더리움 지갑을 통해 Dapp 으로서 gitcoin.io 페이지를 통해 진행하게 됩니다. 

![](http://i.imgur.com/qjyQ0uo.png)



큰 이슈 하나를 해결하면 많게는 1ETH 이상도 받을 수 있고, 오픈소스 기여 경력도 쌓을 수 있다니 매력적이지 않나요?



## Ethlance [(https://ethlance.com)](https://ethlance.com)


![](http://i.imgur.com/RyQLzje.png)



프리랜서와 고용주를 ETH 를 지불수단으로서 연결해주는 플랫폼입니다. 

국내에 위시켓, 크몽같은 서비스의 탈중앙화 형태라고 보실 수 있는데요, Smart Contract 기반의 Dapp 으로서 작동하여 중개자 를 없애 Ethereum Gas 외에 수수료를 없앤것이 특징으로 볼 수 있습니다. 

Part-time, Full-time 이든 상관없이 시간단위로 지급할 ETH 량에 따라 계약을 성사할 수 있습니다. 

현재 기준으로는 개발자 및 개발 위주의 채용이 상당수지만 마케팅, 매니저 등 다양한 직업군에 대한 채용글들도 보이는 등 굳이 개발자에 한정적인 서비스는 아니므로 장차 여러 분야의 업무와 채용도 활발해질 수 있다고 보여집니다. 

![](http://i.imgur.com/Cu0HJMa.png)



프리랜서로 등록한 Candidate 들을 Skill Tag 로 검색하여 시간당 ETH 가격 기준으로 볼 수 있으며, 



![](http://i.imgur.com/h6ll5aq.png)



채용중인 Work 는 고용주(Employer) 가 deposit 한 ETH Balance 를 보고,  구직자들은 시간당 ETH 가격을 입력하여 제안(Proposals) 할 수 있는 형태입니다.

고용주는 제안된 사용자들 중 시간당 ETH rate 와 해당 프리랜서의 Experience 를 보고 선택하여 일을 시작할 수 있게되며 일을 한 후 Invoice 를 요청하여 고용주가 해당 Invoice 를 승낙하므로서 보수가 지급되게 됩니다. 다만 프리랜서가 일을 정상적으로 완수 후 Invoice 를 발행하였음에도 불구하고 고용주가 보수를 지급하지 않는 상황이 올 수 있음을 경고하고있습니다. 이에 대해 Ethlance 는 책임을 지지 않으며, 이같은 상황을 피해기 위해 Feedback 리뷰를 확인 후 진행하길 권장하며, Invoice를 자주 발행하여 해당 처리가 되기전까지 추가 작업을 진행하지 않기를 권장하고 있습니다. 





## 정리하며

얼마전 JTBC 토론 등에서 제기된 암호화폐가 정말 화폐로서 사용가능한가에 대한 논란은 이 같은 서비스가 나오고 실제 사용하는 유저들이 있다는 것으로 증명할 뿐만 아니라 오히려 국가의 경계와 중간자의 수수료를 없애버림으로써 정부가 발행하는 기존의 화폐를 대체할만한 큰 장점들을 발견할 수 있다는 점에서 앞으로의 발전과 변화가 더욱 기대가 됩니다. 

