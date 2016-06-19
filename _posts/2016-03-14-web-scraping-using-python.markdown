---
layout: post
title: "Web Scraping using Python"
description: "Web Scraping using Python"
category: NLP
tags: [python, finace, scraping, crawling, crawlib, bs4, mongodb, mysql]
---

<div id="toc"><p class="toc_title">목차</p></div>

# FinAlgML(놀러온특강) Python을 통한 웹 스크래핑 및 DB화

## 크롤링 예제 대상

### 상장사 리스트
- http://finance.daum.net/quote/all.daum?type=S&stype=P
- ![duam_lit](http://i.imgur.com/7DLMoST.png)
- bs4 사용 방법 소개
- HTML
    
### 네이버 증권 종목분석
- 네이버 금융에서 제공되는 코스피, 코스닥 상장사들의 재무재표, 주식 메타데이터(Financial Summary) 데이터 
- ex) [SK하이닉스](http://finance.naver.com/item/coinfo.nhn?code=000660)
- ![naver_stock](http://i.imgur.com/7jaAVAx.png)
- 비동기 데이터 (ajax)
- source : data_crawler/naver_stock_meta_info/crawler.py
- 저장 : mysql
    
### 네이버 증권 종목토론
- 네이버 금융의 각 종목별 종목 토론실 게시판의 날짜, 제목, 투자의견, 글쓴이, 조회, 공감, 비공감, 내용 등 수집
- 투자의견( 의견없음 매수, 강력매수, 매도, 강력매도, 중립 ) 을 라벨로서 기반하여 제목, 내용에 나타나는 단어를 분석하여 긍, 부정 단어를 확보하기 위한 학습용 데이터로 활용 가능 
- ![naver_discussion](http://i.imgur.com/EpocU5n.png)
- source : data_crawler/naver_stock_discussion/crawler.py
- 저장 : mongodb

### 네이버 증권 실시간 데이터
- 장 마감 이후에도 실시간 데이터가 온다면 라이브 코딩

## 오늘 예제에서 사용되는 Tool, Library

- Chrome Developer Tools (개발자도구)
- BeautifulSoup4
    - Python 에서 HTML 구조 분석, 객체화하는 Library
    - `pip install BeautifulSoup4`
    - ```import bs4```
    
- requests
- gevent
- http://curl.trillworks.com/
- har2requests
- crawlib
    - https://github.com/dongsam/crawlib
- pymysql
- pymongo

### 상장사 리스트
- http://finance.daum.net/quote/all.daum?type=S&stype=P
- ![duam_lit](http://i.imgur.com/7DLMoST.png)
- bs4 사용 방법 소개
- HTML


```python
import urllib2
import bs4
```


```python
url = 'http://finance.daum.net/quote/all.daum?type=S&stype=P'
html = urllib2.urlopen(url).read()
```


```python
len(html)
```




    384272




```python
print html[:1000]
```

    <!doctype html public "-//w3c//dtd html 4.01 transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    
    
    
    
    
    
    
        
                    <html lang="ko">
    <head>
        <meta http-equiv="content-type" content="text/html; charset=utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=10" />
    <title>전종목 시세 - Daum 금융</title>
    <meta name="verify-v1" content="iXgHW7UooMcyeiV/Zb0Tk/yK2yB+IuA5/5GgIzGBEns=" >
    <meta property="og:image" content="http://i1.daumcdn.net/img-media/mobile/meta/finance.png"/>
    <link rel="stylesheet" href="http://s1.daumcdn.net/stock/css/common.css?ver=20160220214249" type="text/css">
    <link rel="stylesheet" href="http://s1.daumcdn.net/stock/css/newHeader.css?ver=20160220214249" type="text/css">
    <link rel="stylesheet" href="http://s1.daumcdn.net/stock/css/column.css?ver=20160220214249" type="text/css">
    <link rel="stylesheet" href="http://s1.daumcdn.net/stock/css/trade.css?ver=20160220214249" type="text/css">
    <script type="text/javascript" src="http://s1.daumcdn.net/stock/js/common.js?ve



```python
soup = bs4.BeautifulSoup(html)
```


```python
title = soup.find('title')
print title
print title.text
```

    <title>전종목 시세 - Daum 금융</title>
    전종목 시세 - Daum 금융


![duam_1](http://i.imgur.com/wibLFPd.png)


```python
print len(soup.find_all('td'))
print len(soup.find_all('td','txt'))
```

    1724
    571


#### 기업 개수 미달, HTML파일을 끝까지 파싱하지 못한 상황
- BeautfulSoup 함수호출시 파서를 'html.parser' 로 지정해줌으로서 해결가능


```python
soup = bs4.BeautifulSoup(html, 'html.parser')
print len(soup.find_all('td'))
print len(soup.find_all('td','txt'))
```

    3580
    1189



```python
for i in soup.find_all('td','txt')[:20]:
    print i.text
```

    able KQ Monthly Best 11 ETN
    able Monthly Best 11 ETN
    able Quant비중조절 ETN
    able 우량주 Monthly Best 11 ETN
    able 코스피200선물플러스 ETN
    AJ네트웍스
    AJ렌터카
    AK홀딩스
    ARIRANG 200
    ARIRANG AC 월드(합성 H)
    ARIRANG K100EW
    ARIRANG KOSPI50
    ARIRANG S&P; 배당성장
    ARIRANG 고배당주
    ARIRANG 단기유동성
    ARIRANG 미국고배당주(합성 H)
    ARIRANG 바벨 채권
    ARIRANG 방어주
    ARIRANG 선진국(합성 H)
    ARIRANG 스마트베타 LowVOL


#### URL에서 code 추출


```python
for i in soup.find_all('td','txt')[:20]:
    print i.text, i.a['href']
```

    able KQ Monthly Best 11 ETN /item/main.daum?code=580004
    able Monthly Best 11 ETN /item/main.daum?code=580003
    able Quant비중조절 ETN /item/main.daum?code=580002
    able 우량주 Monthly Best 11 ETN /item/main.daum?code=580005
    able 코스피200선물플러스 ETN /item/main.daum?code=580001
    AJ네트웍스 /item/main.daum?code=095570
    AJ렌터카 /item/main.daum?code=068400
    AK홀딩스 /item/main.daum?code=006840
    ARIRANG 200 /item/main.daum?code=152100
    ARIRANG AC 월드(합성 H) /item/main.daum?code=189400
    ARIRANG K100EW /item/main.daum?code=141240
    ARIRANG KOSPI50 /item/main.daum?code=122090
    ARIRANG S&P; 배당성장 /item/main.daum?code=222170
    ARIRANG 고배당주 /item/main.daum?code=161510
    ARIRANG 단기유동성 /item/main.daum?code=190160
    ARIRANG 미국고배당주(합성 H) /item/main.daum?code=213630
    ARIRANG 바벨 채권 /item/main.daum?code=190150
    ARIRANG 방어주 /item/main.daum?code=161490
    ARIRANG 선진국(합성 H) /item/main.daum?code=195970
    ARIRANG 스마트베타 LowVOL /item/main.daum?code=236460



```python
company_dic = {}
for i in soup.find_all('td','txt'):
    company_dic[i.text] = i.a['href'].split('=')[1]
```


```python
print len(company_dic)
company_dic[u'AK홀딩스']
```

    1189





    u'006840'



#### 위 과정 함수화시켜 kosdaq도 간편히 가져와보기 


```python
def get_company_list(url):
    soup = bs4.BeautifulSoup(urllib2.urlopen(url).read(),'html.parser')
    company_dic = {}
    for i in soup.find_all('td','txt'):
        company_dic[i.text] = i.a['href'].split('=')[1]
    return company_dic
```


```python
kospi_url = 'http://finance.daum.net/quote/all.daum?type=U&stype=P'
kosdaq_url = 'http://finance.daum.net/quote/all.daum?type=U&stype=Q'

kosdaq_dic = get_company_list(kosdaq_url)
for k, v in kosdaq_dic.items()[:20]:
    print k, v
```

    이테크건설 016250
    해덕파워웨이 102210
    산성앨엔에스 016100
    엔에이치스팩5호 215790
    서부T&D; 006730
    이스트아시아홀딩스 900110
    웰크론 065950
    아이리버 060570
    대주산업 003310
    우리이티아이 082850
    흥국에프엔비 189980
    CS 065770
    시그네틱스 033170
    성우전자 081580
    신진에스엠 138070
    바이오스마트 038460
    동양이엔피 079960
    심엔터테인먼트 204630
    피제이메탈 128660
    한창산업 079170


#### pymysql 을 이용한 mysql 세팅 및 db insert(replace)


```python
import pymysql # pip install pymysql
mysql_host = "127.0.0.1"
mysql_user = "root"
mysql_passwd = "mysql"
mysql_db = "stock"
mysql_port = 3306
conn = pymysql.connect(host=mysql_host, user=mysql_user, passwd=mysql_passwd, db=mysql_db, port=mysql_port, charset='utf8')
conn.autocommit(True)
cur = conn.cursor()

'''
CREATE TABLE `COMPANY2` (
  `company_id` varchar(11) NOT NULL DEFAULT '',
  `company_name` varchar(255) DEFAULT '',
  `company_type` tinyint(10) DEFAULT NULL,
  PRIMARY KEY (`company_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
'''

for k,v in kosdaq_dic.items():
    cur.execute("replace into COMPANY2 (company_id, company_name, company_type ) values ('{}', '{}', '{}')".format( v.encode('utf-8'), k.encode('utf-8'), 0 ))

for k,v in company_dic.items():
    cur.execute("replace into COMPANY2 (company_id, company_name, company_type ) values ('{}', '{}', '{}')".format( v.encode('utf-8'), k.encode('utf-8'), 1 ))
```


```python
cur.execute("""select * from COMPANY2""")
cur_tmp = cur.fetchall()
for i in cur_tmp[:10]:
    print i[0], i[1], i[2]
```

    000020 동화약품 1
    000030 우리은행 1
    000040 KR모터스 1
    000050 경방 1
    000060 메리츠화재 1
    000070 삼양홀딩스 1
    000075 삼양홀딩스우 1
    000080 하이트진로 1
    000087 하이트진로2우B 1
    000100 유한양행 1


### 네이버 증권 종목분석
- 네이버 금융에서 제공되는 코스피, 코스닥 상장사들의 재무재표, 주식 메타데이터(Financial Summary) 데이터 
- ex) [SK하이닉스](http://finance.naver.com/item/coinfo.nhn?code=000660)
- ![naver_stock](http://i.imgur.com/7jaAVAx.png)
- 비동기 데이터 (ajax)
- source : data_crawler/naver_stock_meta_info/crawler.py
- 저장 : mysql


```python
import requests
import urllib
import bs4
import json
import re
import crawlib
import datetime
import sys
import crawlib
import pymysql # pip install pymysql
```


```python
mysql_host = "127.0.0.1"
mysql_user = "root"
mysql_passwd = "mysql"
mysql_db = "stock"
mysql_port = 3306
conn = pymysql.connect(host=mysql_host, user=mysql_user, passwd=mysql_passwd, db=mysql_db, port=mysql_port, charset='utf8')
conn.autocommit(True)
cur = conn.cursor()
```


```python
def extract_table(html):
    soup = bs4.BeautifulSoup(html)
    th = soup.find_all("th","title")
    vertical_columns = [i.text.strip() for i in th]

    bg = soup.find_all("th",re.compile(r"^r"))[2:]
    horizon_columns = [crawlib.getOnlyDigit(i.text.strip()) for i in bg]

    cBk = [int(crawlib.getOnlyDigit(i.text)) for i in soup.find_all("td","num")]

    # colums_count_check
    if len(cBk) != (len(vertical_columns) * len(horizon_columns)):
        print(error)
        sys.exit()
        
    return vertical_columns, horizon_columns, cBk


def request_and_store(company_code, freq_typ, fin_typ=0):
    company_code = str(company_code).zfill(6)
    # zero padding 6
    url = 'http://companyinfo.stock.naver.com/v1/company/ajax/cF1001.aspx?cmp_cd={}&fin_typ={}&freq_typ={}'.format(company_code, str(fin_typ), freq_typ)
    print url
    headers = {
        'Accept-Language' : 'ko-KR,ko;q=0.8,en-US;q=0.6,en;q=0.4',
        'Accept-Encoding' : 'gzip, deflate, sdch',
        'X-Requested-With' : 'XMLHttpRequest',
        'Connection' : 'keep-alive',
        'Accept' : 'text/html, */*; q=0.01',
        'User-Agent' : 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_2) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/47.0.2526.106 Safari/537.36',
        'Host' : 'companyinfo.stock.naver.com',
    }
    cookies = {
    }
    data_dic = {
    #     'freq_typ' : '''Y''',
    #     'fin_typ' : '''0''',
    #     'cmp_cd' : '''051910''',
    }
    data = ""
    for k, v in data_dic.items():
        data += urllib.quote_plus(k)+"="+urllib.quote_plus(v)+"&"
    res = requests.post(url, headers=headers, cookies=cookies, data=data)
    vertical_columns, horizon_columns, cBk = extract_table(res.content)

    cnt = 0
    print len(cBk)
    for value in cBk:
        vertical_i = cnt / len(horizon_columns)
        horizon_i = cnt % len(horizon_columns)
#         print vertical_columns[vertical_i], horizon_columns[horizon_i]
#         print value
        try:
            cur.execute("""replace into META (company_id, meta_type, meta_freq_type, meta_value, meta_date, meta_crawled_date ) values ('{}', '{}', '{}', '{}', '{}', '{}')""".format( 
                    company_code, vertical_columns[vertical_i].encode("utf-8"), freq_typ , value, datetime.datetime.strptime(horizon_columns[horizon_i],"%Y%m"), datetime.datetime.now())
                        )
        except Exception as e:
            print e
        cnt += 1
    print cnt
```


```python
cur.execute("""select * from COMPANY2""")
cur_tmp = cur.fetchall()
for i in cur_tmp[:3]:
    request_and_store(i[0],'Q')
    request_and_store(i[0],'Y')
```

    http://companyinfo.stock.naver.com/v1/company/ajax/cF1001.aspx?cmp_cd=000020&fin_typ=0&freq_typ=Q
    256
    256
    http://companyinfo.stock.naver.com/v1/company/ajax/cF1001.aspx?cmp_cd=000020&fin_typ=0&freq_typ=Y
    256
    256
    http://companyinfo.stock.naver.com/v1/company/ajax/cF1001.aspx?cmp_cd=000030&fin_typ=0&freq_typ=Q
    256
    256
    http://companyinfo.stock.naver.com/v1/company/ajax/cF1001.aspx?cmp_cd=000030&fin_typ=0&freq_typ=Y
    256
    256
    http://companyinfo.stock.naver.com/v1/company/ajax/cF1001.aspx?cmp_cd=000040&fin_typ=0&freq_typ=Q
    256
    256
    http://companyinfo.stock.naver.com/v1/company/ajax/cF1001.aspx?cmp_cd=000040&fin_typ=0&freq_typ=Y
    256
    256


### 주기적 실행, 자동화
- cron ( crontab )
- [supervisor](http://supervisord.org/)

### 네이버 증권 종목토론
- 네이버 금융의 각 종목별 종목 토론실 게시판의 날짜, 제목, 투자의견, 글쓴이, 조회, 공감, 비공감, 내용 등 수집
- 투자의견( 의견없음 매수, 강력매수, 매도, 강력매도, 중립 ) 을 라벨로서 기반하여 제목, 내용에 나타나는 단어를 분석하여 긍, 부정 단어를 확보하기 위한 학습용 데이터로 활용 가능 
- ![naver_discussion](http://i.imgur.com/EpocU5n.png)
- source : data_crawler/naver_stock_discussion/crawler.py
- 저장 : mongodb


```python
import logging
import pymongo
import crawlib
import time
from datetime import datetime
from gevent import monkey
monkey.patch_all()
from gevent.pool import Pool

collection = pymongo.MongoClient().stock.naver_discussion

```


```python
class NaverCrawling(crawlib.Crawling):
    def get_item_list(self, cate, page):
        url = self.make_target_url(cate, page)
        soup = crawlib.getSoup(url)
        link_list = []
        for i in soup.find_all('tr',{'onmouseover':'mouseOver(this)'}):
            link = i.find_all('td')[1].a['href'].split('&st=&sw=&page')[0]
            link = crawlib.urljoin('http://finance.naver.com',link)

            # already exist this data
            if self.data_dic.has_key(link):
                print "exist", link
                continue

            self.data_dic[link] = {}
            self.data_dic[link]['date'] = i.find_all('td')[0].text.strip()
            self.data_dic[link]['title'] = i.find_all('td')[1].a['title'].strip()
            self.data_dic[link]['opinion'] = i.find_all('td')[2].text.strip()
            self.data_dic[link]['view'] = i.find_all('td')[4].text.strip()
            self.data_dic[link]['sympathy'] = i.find_all('td')[5].text.strip()
            self.data_dic[link]['unsympathy'] = i.find_all('td')[6].text.strip()
            self.data_dic[link]['_id'] = link

            link_list.append(link)
            # self.get_item(link)

        if len(link_list) == 0:
            return 'stop'

        pool = Pool(len(link_list))
        res = pool.map(self.get_item, link_list)

    def get_item(self, url, key=''):
        if not key:
            key = url
        soup = crawlib.getSoup(url)
        content = '\n'.join([i.text for i in soup.find_all('div','view_se')]).strip()
        user = soup.find('th','info').find('span').text.strip()
        nid = crawlib.get_param_from_url(url, 'nid')
        code = crawlib.get_param_from_url(url, 'code')

        self.data_dic[key]['content'] = content
        self.data_dic[key]['nid'] = nid
        self.data_dic[key]['code'] = code
        self.data_dic[key]['user'] = user

        print key, self.data_dic[key]['opinion']
        # runtime_check = time.time()
        collection.replace_one({"_id": key}, self.data_dic[key], upsert=True)
        # print time.time() - runtime_check


    # todo: mongo db library 화
    # todo: 최신글부터 가져오되 몇개이상(한페이지이상)  중복 감지시 stop


```


```python
target_name = 'naver_stock_discussion'
naver_dicussion = NaverCrawling(target_name=target_name, base_url='http://finance.naver.com/item/board.nhn?', cate_param='code',
                                page_param='page', cate_list_path='category.txt', page_list=range(1, 1000))


naver_dicussion.crawling_cate_list(cate_delay=0, page_delay=0)
# 결과는 console 에서 확인 
```

### 네이버 증권 실시간 데이터
- 장 마감 이후에도 실시간 데이터가 온다면 라이브 코딩
- http://finance.naver.com/item/main.nhn?code=035420
- live coding youtube 영상 : https://youtu.be/2UP91K7SUzE


```python
import crawlib # https://github.com/dongsam/crawlib
```


```python
res = crawlib.har2requests('finance.naver.com.har') # 각자 크롬 개발자도구통해 받은 har 파일 경로 입력 
```


```python
# print res # 아래 코드 생성
```


```python
import requests
import urllib
import json
from pprint import pprint
url = 'http://polling.finance.naver.com/api/realtime.nhn?query=SERVICE_ITEM:035420|SERVICE_RECENT_ITEM:035420&_callback='
headers = {
    'Accept-Language' : 'ko-KR,ko;q=0.8,en-US;q=0.6,en;q=0.4',
    'Accept-Encoding' : 'gzip, deflate, sdch',
    'Connection' : 'keep-alive',
    'Accept' : '*/*',
    'User-Agent' : 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_11_3) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/49.0.2623.87 Safari/537.36',
    'Host' : 'polling.finance.naver.com',
    'Referer' : 'http://finance.naver.com/item/main.nhn?code=035420',
}
cookies = {
}
data_dic = {
}
data = ""
for k, v in data_dic.items():
    data += urllib.quote_plus(k)+"="+urllib.quote_plus(v)+"&"
res = requests.post(url, headers=headers, cookies=cookies, data=data)
res_str = res.content.decode('euc-kr').encode('utf-8')
res_json = json.loads(res_str)
pprint(res_json)
```

    {u'result': {u'areas': [{u'datas': [{u'aa': 37807000000,
                                         u'aq': 59460,
                                         u'cd': u'035420',
                                         u'cnsPer': 31.27,
                                         u'cr': 0.47,
                                         u'cv': 3000,
                                         u'hv': 642000,
                                         u'll': 446000,
                                         u'lv': 630000,
                                         u'ms': u'CLOSE',
                                         u'mt': u'1',
                                         u'nav': None,
                                         u'nm': u'NAVER',
                                         u'nv': 639000,
                                         u'ov': 633000,
                                         u'pbr': 8.78,
                                         u'pcv': 636000,
                                         u'per': 40.6,
                                         u'rf': u'2',
                                         u'sv': 636000,
                                         u'tyn': u'N',
                                         u'ul': 826000}],
                             u'name': u'SERVICE_RECENT_ITEM'},
                            {u'datas': [{u'aa': 37807000000,
                                         u'aq': 59460,
                                         u'cd': u'035420',
                                         u'cnsPer': 31.27,
                                         u'cr': 0.47,
                                         u'cv': 3000,
                                         u'hv': 642000,
                                         u'll': 446000,
                                         u'lv': 630000,
                                         u'ms': u'CLOSE',
                                         u'mt': u'1',
                                         u'nav': None,
                                         u'nm': u'NAVER',
                                         u'nv': 639000,
                                         u'ov': 633000,
                                         u'pbr': 8.78,
                                         u'pcv': 636000,
                                         u'per': 40.6,
                                         u'rf': u'2',
                                         u'sv': 636000,
                                         u'tyn': u'N',
                                         u'ul': 826000}],
                             u'name': u'SERVICE_ITEM'}],
                 u'pollingInterval': 60000,
                 u'time': 1458441607440},
     u'resultCode': u'success'}

<script src="https://gist.github.com/dongsam/55a0f00d4eab9185c55a.js"></script>