---
layout: post
title: "Add personal Python Package path"
description: "add personal Python Package, Library path on OS X"
category: python
tags: [python, setting, mac, osx]
---
<div id="toc"><p class="toc_title">목차</p></div>

## Background
개발을 하다 보면 자주 사용하는 코드는 자신만의 패키지, 라이브러리(이하 패키지)를 작성하여 사용하게 되곤 한다. 필자 또한 파이썬 패키지를 개발을 하여 여러 프로젝트에 사용을 하는데, 아직 PyPI 등 으로 배포를 시키지 않고 로컬에서 개발 중인 단계의 패키지일 경우, 여러 프로젝트에서 해당 패키지를 단순히 복사해와 import 하여 사용하다 파편화 등 불편함을 겪게 되어 찾게 된 방안들을 소개하고자 한다.

Local Python 환경에 그냥 install 한 후 사용할 수도 있지만 한참 개발 중인 패키지의 경우 패키지가 빈번하게 수정 및 업데이트가 발생하는데, 그때마다 재설치, 업데이트하기는 귀찮기 마련이다. 이 같은 고민을 하고 있다면, 아래의 방법 중 상황 및 성향에 맞게 시도해보면 도움이 될 수 있을 것이다.


![python](http://i.imgur.com/h02XYV8.png)

## Test Environment
- OS X El Capitan 10.11.3
- Macbook Pro 15 Retina
- Python 2.7.9 |Anaconda 2.1.0 (x86_64)|
- 개발 중인 패키지 Path : /Users/dongsamb/PycharmProjects/crawlib

## sys.path 일시적 추가
- (일회성 임시적 방법)
- 개발 중인 패키지 Path가 다음과 같다고 가정한다.  : /Users/dongsamb/PycharmProjects/crawlib
- 위 패키지를 타 Python 소스에서 import 하여 사용하고자 하는 상황, 현재는 해당 패키지를 인식하지 못한다.

```python
import crawlib
ImportError: No module named crawlib
```

- 아래와 같이 코드를 추가 후 시도하면 정상적으로 import 되는 것을 확인할 수 있다.

```python
import sys
sys.path.append('/Users/dongsamb/PycharmProjects/crawlib')
```

```python
import crawlib
# import 성공
```

### 장점
- 코드 1~2줄 추가로 간편하게 적용할 수 있다

### 단점
- 대상 패키지를 import 하여 사용하고자 하는 모든 소스에 모두 코드를 추가해야 한다.
- 일회성 임시적 방법


## export를 통한 PYTHONPATH 추가
- (터미널 환경에 한한 임시적 방법)
- os x 의 bash shell 기반의 설정 예시

```sh
$ export PYTHONPATH=/Users/dongsamb/PycharmProjects/crawlib:$PYTHONPATH
```

```python
import crawlib
# import 성공
```

- 터미널 세션 종료 이후에도 반영구적으로 적용하고 싶을 시 ~/.bash_profile 에 위 구문 추가

### 장점
- 터미널에 환경에 한해 반영구적인 적용

### 단점
- (터미널 환경에 한한 임시적 방법)
- Jupyter(ipython) notebook 환경 등에는 PYTHONPATH 적용이 안되 import 가 정상적으로 안 될 수 있다.


## symbolic link를 통한 패키지 추가 (추천)
- (설치와 동일 효과를 주는 영구적인 방법)
- 아래와 같이 Python에서 실행해보면 sys.path, 즉 자신 로컬 환경의 패키지 경로들을 확인할 수 있다.

```python 
import sys
print(sys.path)
['',
 '/Users/dongsamb/anaconda/bin',
 '/Users/dongsamb/anaconda/lib/python2.7/site-packages/Scrapy-0.24.4-py2.7.egg',
 '/Users/dongsamb/anaconda/lib/python2.7/site-packages/cssselect-0.9.1-py2.7.egg',
 '/Users/dongsamb/anaconda/lib/python2.7/site-packages/queuelib-1.2.2-py2.7.egg',
 '/Users/dongsamb/anaconda/lib/python2.7/site-packages/w3lib-1.11.0-py2.7.egg',
 '/Users/dongsamb/anaconda/lib/python2.7/site-packages/Twisted-14.0.2-py2.7-macosx-10.5-x86_64.egg',
 '/Users/dongsamb/anaconda/lib/python2.7/site-packages/zope.interface-4.1.2-py2.7-macosx-10.5-x86_64.egg',
 ...
 ...
]
```

- 위 환경 기준으로 `/Users/dongsamb/anaconda/lib/python2.7/site-packages/` 에 패키지 폴더를 위치시킨다면 정상적으로 import가 가능하다.
- 하지만 위 환경에 개발 중인 패키지를 위치하고, 그 위치에서 수정, 업데이트하며 개발할 순 없으니 개발 중인 패키지의 Path를 [symbolic link](https://en.wikipedia.org/wiki/Symbolic_link) 를 통해 위 경로에 링크해 준다.

- 개발 중인 패키지 Path가 다음인 경우 : /Users/dongsamb/PycharmProjects/crawlib

```sh
$ cd /Users/dongsamb/anaconda/lib/python2.7/site-packages
$ ln -s /Users/dongsamb/PycharmProjects/crawlib ./
```

```sh
$ ls -al | grep crawlib
lrwxr-xr-x    1 dongsamb  staff        50 Jan 28 14:22 ko2vec -> /Users/dongsamb/PycharmProjects/crawlib
```

```python
import crawlib
# import 성공
```

### 장점
- (설치와 동일 효과를 주는 영구적인 방법)

### 단점
- 개발 중인 패키지의 path가 변경됐을 시 link 수정, 재적용 필요




물론 개인적으로 겪었던 사례를 소개한 것이라 필자가 모르는 더 좋은 방법이 있을 수 있다.
더 좋은 방법이 있다면 댓글을 통해 말씀해주시면 감사하겠습니다.