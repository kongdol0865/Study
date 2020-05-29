## JSP

### 1. 웹 프로그래밍

![image-20200529090311225](image/image-20200529090311225.png)

- 웹프로그램의 동작

![image-20200529090633327](image/image-20200529090633327.png)

- 어떠한 로직이 수행되는 WAS에 접근함 (웹 어플리케이션 서버)

### 2.  JSP 문서 작성하기

-  동적 웹어플리케이션 컴포넌트
-  mvc패턴에서 view로 이용됨
- Client가 요청하면 **Controller**가 무엇을 작업할지 판단 -> **model**에게 넘기고 다시 받아서 **view**로 사용자들에게 response함

#### 1) 아키텍쳐

![image-20200529093000865](image/image-20200529093000865.png)

### 3. Servlet 문서 작성하기

1) Servlet

- java thread 이용하여 동작!
- MVC패턴에서 Controller로 이용됨

2) 닉네임 매핑 방법

1. annotation

```java
@WebServlet("/HWorld") //annotation으로 닉네임 매핑
```

**기존 경로** **: http://localhost:8181/helloworld/servlet/com.javalec.ex.HelloWorld**

URL맵핑 **경로** **: http://localhost:8181/helloworld/HWorld**

2. web.xml파일에서

- <servlet-name>

   : 임의의 이름을 만들어 줍니다.

  **<****servlet-class>**

   : 매핑할 클래스 파일명을 패키지명을 포함하여 정확하게 입력 합니다.

  **<****url-pattern>**

   : servlet-class의 클래스를 매핑할 임의의 이름을 입력 합니다. 주위할 점은 ‘/’로 시작해야 합니다.

```java
<servlet>
  	<servlet-name>helloworld</servlet-name> //servlet 이름 정하기
  	<servlet-class>com.javalex.ex.HelloWorld</servlet-class>
  </servlet>
  <servlet-mapping>
  	<servlet-name>helloworld</servlet-name>
  	<url-pattern>/hw</url-pattern>
  </servlet-mapping>
```

***project import할 때*** 

***Project > Properties> Javascript> Project Facets> Java 버전 1.7***

***Project > Properties>Java Compiler> 1.7***