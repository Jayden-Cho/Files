*시중에 나와 있는 책은 대부분 <u>API</u>를 이용해 데이터를 수집하는 차원의 웹 크롤링을 소개하는 것이 대부분. 크롤링 자체가 합법과 범법 사이에서 줄타기를 하는 작업이기 때문에.*

자신이 원하는 데이터가 API로 존재하지 않는다면 직접 크롤링(crawling)하는 수 밖에 없다.

> **API?**
>
> Application Programming Interface. 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스(Wikipedia).
>
> 쉽게 말해 프로그램과 프로그램을 이어주는 매개체. 응용 프로그램에서 데이터를 주고 받기 위해 API라는 징검다리를 제공하는 것.



## 데이터 크롤링을 위한 준비 도구 selenium 

BeautifulSoup로 다루는 방법도 있지만, 다음에 다루기로 하자(아직 못배웠다...)

> **Selenium?**
>
> 사용자가 프로그램을 이용하는 방식을 대신해주는?



- *브라우저의 동작을 자동화 해주는 프로그램. 사용자 대신에 컴퓨터가 브라우저를 뒤져가며 자료를 수집함.*
- *웹 앱을 테스트할 때 주로 사용하는 프레임워크.*
- *selenium의 webdriver라는 api를 통해 chrome 브라우저를 제어하고자 함.*
- *몇몇 사이트들을 홈페이지를 사용자가 직접 동작시키지 않으면 정보가 공개되지 않도록 설계되어 있어 태그 기반으로 정보를 가져오는 방법(BeautifulSoup)으로는 정보를 가져오기 힘들어짐.*
- *사이트를 보면서 콘텐츠를 열고 닫고 넘어가는 등 정보를 불러오는 방식으로 정보를 수집할 수 있음.*



#### 1. selenium 설치

명령 프롬프트(터미널)에 한 줄만 입력하면 간단히 다운 가능하다.

```python
pip install selenium
```



#### 2. Chromedriver 설치

크롬 버전에 맞게 다운.

- 설정 - Chrome 정보에서 확인 가능.

- 브라우저 별로 driver를 다운로드 해야한다. 



#### 3. Selenium 구동

단 4줄로 간단하게 chrome 창을 켤 수 있다.

```python
#selenium 라이브러리에서 webdriver를 import.
from selenium import webdriver 

# chromedriver를 다운받은 path를 입력.
path = "/Users/Downloads/chromedriver"

# chrome을 조종할 수 있는 driver를 생성한다.
driver = webdriver.Chrome(path)

# get() 함수로 원하는 사이트 주소를 넣는다. 이 경우 구글 주소를 입력했다.
driver.get("https://www.google.com")
```

브라우저 종료를 시키기 위해서는 close() 함수를 이용하면 된다.

~~~python
driver.close()
~~~







프레임워크















