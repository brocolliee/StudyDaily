## Data Scraping

- '빅데이터 서비스' 강의 들은 후 정리

### 웹 스크래핑

- 웹 사이트에서 데이터를 추출하는데 사용되는 데이터 스크랩

- 원하는 부분에 위치한 정보를 자동으로 추출하여 수집



### 웹 브라우저의 작동 방식과 HTML 구조 (중요 개념)

- URL(Uniform Resource Locator) : 인터넷에 연결된 여러 컴퓨터의 위치를 나타내는 방식

- HTTP(HyperText Transfer Protocol) : 하이퍼텍스트를 주고받기 위한 규약을 의미
  - 하이퍼텍스트 : 텍스트를 차례대로 읽어나갈 수 있고 링크를 클릭시 원하는 곳으로 이동할 수 있는 기능이 포함된 텍스트
- HTML 태그 table : 표를 나타내는 태그로 read_html로 테이블 정보를 읽어서 데이터프레임으로 변환해주는 기능



### Pandas 이용한 데이터 수집

- 네이버 영화 랭킹을 데이터 프레임으로 가져오기

```python
import pandas as pd
url = "url 넣어주기"
df = pd.read_html(url) # url 안에 있는 테이블을 가져오게 됨

df = df.dropna(axis = 1, thresh = 10) # column 중에 nan이 10개 이상인거 지우기
df = df.dropna(axis = 0, thresh = 2) # row 중에 nan이 2개 이상인거 지우기
df = df.drop('변동폭.1', axis = 1) # '변동폭.1' column 지우기

df.columns = ['20200922'] # column 이름 할당

## for 문을 통해 여러 날짜
movie = []
for i in range(7):
    url = "url 넣어주기, i를 사용해서 url 안에 있는 날짜 수정" 
    df = pd.read_html(url)[0] # url 안에 있는 테이블을 가져오게 됨

    df = df.dropna(axis = 1, thresh = 10) # column 중에 nan이 10개 이상인거 지우기
    df = df.dropna(axis = 0, thresh = 2) # row 중에 nan이 2개 이상인거 지우기
    df = df.drop('변동폭.1', axis = 1) # '변동폭.1' column 지우기

    df.columns = ['2020092' + str(i)] # column 이름 할당
    movie.append(df)
    
df2 = pd.concat(movie, axis = 1) 
```



### Beautifulsoup을 이용한 데이터 수집

- HTML 태그내에서 원하는 내용 가져오기

```python
import urllib.request as URL
from bs4 import BeautifulSoup as bs

url = "위키피디아 url 넣기"
response = URL.urlopen(url) # url 열기
data = response.read()

soup = bs(data, 'html.parser') # bs가 html을 분석해서 soup에 저장
# soup을 이용해 원하는 거 사용 가능

g = open('cat.txt', 'w', encoding = 'utf-8')
g.write(soup.prettify()) # 파일에 내용 적기
g.close()

all_tag = soup.find_all("p") # p 태그 안에 있는 것 가져오기 위함
g = open('cat_p.txt', 'w', encoding = 'utf-8')
for i in all_tag:
    g.write(i.get_text() + '\n') # p 태그 안에 있는 내용을 저장해나감
g.close()

all_link = soup.find_all("a") # a 태그 안에 있는 것 주소를 뽑아 저장
g = open('cat_url.txt', 'w', encoding = 'utf-8')
for i in all_link:
    # g.write(str(i) + '\n') # a 태그 자체를 가져옴
    # a 안에 href 안 다른 url 링크 가져오기
    # 페이지 내에서 원하는 정보 수집 후 연결된 페이지로 이동해서 정보 수집하는 크롤러를 만들 수 있음
    if 'href' in i.attrs:
        if i.attrs['href'][:4] == 'http':
            g.write(i.attrs['href'] + '\n')
g.close()
```



### selenium 라이브러리

- xpath : 태그들의 포함관계, 순서를 이용하여 한 페이지 내에 속한 원소들 각각의 주소
  - 개발자 도구 이용하여 해당 태그의 xpath 구할 수 있음

``` python
from selenium import webdriver
import time # page loading 되도록 기다려주기 위함 

path = './chromedriver.exe' # 다운로드 받아서 폴더에 넣기
driver = webdriver.Chrome(path)

url = 'site url' # 가지고 오고자 하는 url 넣기
driver.get(url)
time.sleep(3) # 3초 기다려주기

# 프로그램을 통해 어떤 작업을 하기 위해 xpath를 사용하기
driver.find_element_by_xpath('xpath') # xpath 복사 후 넣어주기

# 예 : 날짜 입력하기 (input 값 넣기 => 조회 버튼)
date = driver.find_element_by_xpath('input xpath') # input xpath 넣어주기
date.clear()
date.send_keys(2020.07.20) # 자동으로 날짜를 넣어줌
bt = driver.find_element_by_xpath('button xpath') 
bt.click() # 버튼 클릭하기

```