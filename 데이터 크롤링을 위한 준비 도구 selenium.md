> 참고!! 배우면서 정리하기 위해 쓰여진 글이므로 부정확한 내용이 있을 수 있습니다.
     
많은 기업들과 공공기관에서 자신들의 데이터를 API를 통해 공유하고 있다. 하지만 공유된 데이터는 제한적이고, 자신이 원하는 데이터가 API로 존재하지 않는다면 직접 크롤링(crawling)하는 수 밖에 없다. 이 포스트에 크롤링에 필수적인 도구인 selenium  기초에 대해 정리했다.
     
> **API?**
>
> Application Programming Interface. 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스(Wikipedia).
>
> 쉽게 말해 프로그램과 프로그램을 이어주는 매개체. 응용 프로그램에서 데이터를 주고 받기 위해 API라는 징검다리를 제공하는 것.
     
## 데이터 크롤링을 위한 준비 도구 selenium 

BeautifulSoup로 다루는 방법도 있다고는 한데, 다음에 시간나면 배우자(아직 배우지 못했다...).

> **Selenium?**
>
> 브라우저의 동작을 자동화시켜주는 프로그램. 웹 앱을 테스트할 때 주로 사용된다고 한다. 여기선 사용자가 설정한대로 자동으로 데이터를 수집하게 도와준다.



#### 1. selenium 설치

명령 프롬프트(터미널)에 한 줄만 입력하면 간단하게 설치가 가능했다.

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

이것만 했는데도 거의 해커 수준의 뿌듯함을 느꼈다..



브라우저 종료를 시키기 위해서는 *close()* 함수를 이용하면 된다.

~~~python
driver.close()
~~~



## 예제 - selenium를 이용한 자동 로그인

selenium을 이용해 다음(www.daum.net)에 자동으로 로그인 해보자. 다음 아이디가 기억이 안나서 카카오 아이디로 대신 접속함.

```python
from selenium import webdriver

driver = webdriver.Chrome("chromedriver가 저장된 PATH")
driver.implicitly_wait(3)
# get() 메소드로 다음 로그인창 주소 접속.
driver.get("https://accounts.kakao.com/login?continue=https%3A%2F%2Flogins.daum.net%2Faccounts%2Fksso.do%3Frescue%3Dtrue%26url%3Dhttps%253A%252F%252Fwww.daum.net%252F")
```

*Implicitly_wait()* 메소드로 브라우저에서 사용되는 엔진 자체에서 파싱되는 시간을 기다리게 할 수 있음.



로그인을 하기 위해선 id와 password가 필요하다. 각각의 id와 password를 입력하는 창을 찾기 위해서 웹페이지 소스에 접속한다. 크롬 옵션에 도구 더보기 - 개발자 도구에서 웹페이지 소스 확인 가능하다.

```python
driver.find_element_by_name('email').send_keys('이메일 주소')
driver.find_element_by_name('password').send_keys('비밀번호')
```

> find_element_by_name() 같은 메소드를 사용하기 위해선 Javascript 기초 내용을 알고있어야 한다. 다음에 시간이 되면  정리해보자.



여기서 조금 어려웠는데, selenium에서 자동으로 버튼을 클릭하기 위해선 *find_element_by_xpath()*라는 메소드를 사용해 페이지가 넘어가는 버튼을 찾고, click()으로 그 버튼을 클릭해야 한다. 이 XPath 배운다고 한참 고생했는데, 그냥 우클릭으로 간단하게 구할수 있더라..

> 페이지 소스에서 버튼에 해당하는 class를 찾고 그에 대한 xpath를 copy한다.
>
> button class를 오른쪽 클릭 - Copy - Copy XPath

```python
driver.find_element_by_xpath('//*[@id="login-form"]/fieldset/div[8]/button').click()
```

이메일 주소와 비밀번호를 올바르게 입력했다면 로그인이 자동이 된다.



### 전체 코드

몇줄 안되는 코드로 해커뽕을 맞을 수 있었다.

```python
from selenium import webdriver

driver = webdriver.Chrome("chromedriver가 저장된 PATH")
driver.implicitly_wait(3)
driver.get("https://accounts.kakao.com/login?continue=https%3A%2F%2Flogins.daum.net%2Faccounts%2Fksso.do%3Frescue%3Dtrue%26url%3Dhttps%253A%252F%252Fwww.daum.net%252F")

driver.find_element_by_name('email').send_keys('이메일 주소')
driver.find_element_by_name('password').send_keys('비밀번호')

driver.find_element_by_xpath('//*[@id="login-form"]/fieldset/div[8]/button').click()
```

 





