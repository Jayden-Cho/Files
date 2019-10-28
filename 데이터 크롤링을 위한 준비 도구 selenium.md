자신이 원하는 데이터가 API로 존재하지 않는다면 직접 크롤링(crawling)하는 수 밖에 없다. 



> **API?**
>
> Application Programming Interface. 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스(Wikipedia).
>
> 쉽게 말해 프로그램과 프로그램을 이어주는 매개체. 응용 프로그램에서 데이터를 주고 받기 위해 API라는 징검다리를 제공하는 것.



## 데이터 크롤링을 위한 준비 도구 selenium 

BeautifulSoup로 다루는 방법도 있지만, 다음에 다루기로 하자(아직 배우지 못했다...)

> **Selenium?**
>
> 브라우저의 동작을 자동화시켜주는 프로그램. 웹 앱을 테스트할 때 주로 사용된다고 한다. 여기선 사용자가 설정한대로 자동으로 데이터를 수집하게 도와준다.



#### 1. selenium 설치

명령 프롬프트(터미널)에 한 줄만 입력하면 간단하게 설치가 가능하다.

```python
pip install selenium
```



#### 2. Chromedriver 설치

> https://chromedriver.chromium.org/

크롬 버전에 맞게 다운하면 된다.

- 크롬 버전은 설정 - Chrome 정보에서 확인 가능하다.

- 크롬 이외의 브라우저를 사용한다면, 브라우저 별로 driver를 다운로드 해야한다. 



#### 3. Selenium 구동

단 4줄로 간단하게 chrome 창을 켤 수 있다.

```python
#selenium 라이브러리에서 webdriver를 import.
from selenium import webdriver 

# chromedriver를 다운받은 path를 입력. 필자는 Downloads 파일에 설치했다.
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











