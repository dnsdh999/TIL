# 1강

1. FrameWork
 프레임워크 - 틀 안에서만 동작한다는 것.
 틀 안에서만 개발할 수 있게 만들어 놓은 틀.

2. OpenSource
 소스코드가 공개되어 있음.
 불편한 사항이 있거나 바꾸고 싶은 부분이 있다면 내부를 뜯어 고칠 수 있다.

3. IoC(Inversion of Controll)컨테이너 - Spring의 핵심
 제어의 역전이라는 뜻으로, 주도권이 Spring에 있다는 것을 의미한다.

 Class -> 설계도
 abstract Class -> 추상적인 의미의 Class (ex 가구) 
 Object -> 실체화가 가능한 것. (ex 침대, 의자)
 Instance -> 객체(ex 오브젝트로 있다가 튀어나오면, 그것이 instance가 됨. -> 침대, 의자)

 객체와 힙 메모리의 관리, 로직의 설계가 힘들다.
 그래서 나온 IoC
 class를 모두 읽어 메모리에서 객체들을 Spring이 직접관리

4. DI - Dependency Injection
 Spring이 관리하는 객체들을 개발자가 원하는 곳에서 가져와서 사용할 수 있다는 것.

 의자, 책상클래스가 있다고 한다면 이를 IoC가 스캔하여 Spring이 객체를 단 한번만 만들어 직접 생성하게 된다.
 DI에 의해서 사용이 가능하다.
 IoC, DI로 인한 매우 편한 프로그래밍이 가능.

# 2강

5. Spring의 필터
 Spring에는 아주 많은 필터가 있다. 
 특정한 권한을 가지고 있는지 확인하고, 출입을 시킬지 필터에서 결정한다.
 스프링 자체의 필터를 사용할 수도 있고
 사용되지 않고 있는 필터를 사용하게 설정할 수도 있고
 사용자가 직접 필터를 만들어 사용할 수 있다.

 ex)
 성 = tomcat
 왕집 = Spring

 톰캣의 필터 'web.xml'
 스프링의 필터 '인터셉터' (AOP) 권한체크


6. Spring은 매우 많은 어노테이션을 가지고 있음 - 리플렉션, 컴파일체킹
 어노테이션 - 주석의 역할과 동시에 힌트를 준다. - 컴파일러가 무시하지 않음 (주로 객체를 생성하는 역할을 한다.)
 리플렉션은 런타임 시 작동하여 분석한다.

 ex)
 @Component - 클래스 메모리에 로딩
 @Autowired - 로딩된 객체를 해당 변수에 집어 넣어라

 ex)
 @Component
 Class A ...

 @Component라는 태그가 있다면
 Spring이 해당 클래스를 스캔하여 
 힙 메모리 공간에 해당 클래스를 로드한다. -> IoC

 Class B{
     @Autowired
     A a;
 }

 Spring이 B Class를 스캔할 때 어떤 객체가 있는지 확인하는 것이 리플렉션 (분석)이다.
 해당 작업을 통해 메서드, 필드, 어노테이션이 있는지 체킹할 수 있다.
 heap에 같은 타입의 A클래스로 된 객체가 있는지 확인하고, 있다면 해당 객체를 사용하는 것으로 설정한다. -> DI  
 체킹 뿐만 아니라 있다면 특정 작업을 수행하게끔 설정도 가능하다.


# 3강

7. 
 메시지를 통한 소통을 위해 중간 데이터(중간 언어)를 하나 만든다.
 중간 언어로 xml이 주로 쓰이다가 요즘은 JSON을 주로 사용한다.

 자바의 Object와 파이썬의 Object가 있다고 한다면
 서로 주고 받기가 힘들 것.
 이 때 자바와 파이썬은 Object를 JSON으로 바꾸고 전송한다.

 자바 Object -> JSON -> 파이썬 Object 
 자바에서 파이썬으로 바꾸기는 어렵지만 JSON에서 바꾸기는 쉽다. 반대로도 마찬가지.

 - MessageConverter
 자바 Object를 전송할 때 JSON으로 컨버팅해주는 것.
 Jackson 추가 후 사용할 수 있다.
 request(요청), response(응답) 시 데이터를 주고 받을 때 모두 컨버팅이 가능한다.

 Jackson - JSON데이터로 변경해주는 라이브러리

8. Spring은 BufferedReader와 BufferedWriter를 쉽게 사용 가능하다.
 8비트씩 끊어 읽는다면 한 문자씩 받을 수 있을 것이다.
 8비트로 256가지의 문자 전송이 가능 (영문 기준)
 하지만 한국에서는 16비트가 있어야 글자 표현이 가능하다.

 바이트 스트림을 읽어들일 때 InputStream으로 읽는다.
 여러개의 문자를 받는 배열로 InputStreamReader로 받는다.
 이는 배열로 저장하게 되는데, 배열은 크기가 정해져 있으므로 데이터 낭비나 데이터 손실이 일어나게 된다.
 그래서 이를 BufferedReader로 감싸 가변길이의 문자를 받을 수 있다.

 @ResponseBody 를 쓰면 BufferedWriter가 동작
 @RequestBody를 쓰면 BufferedReader가 동작

 보내는 데이터를 받을 수 있다.

# 4강
JPA란 무엇인가
9. 
 persistence(영속성)은 데이터를 생성한 프로그램 실행이 종료되더라도 사라지지 않는 데이터의 특성을 의미.
 램 = 휘발성 데이터
 영구적 데이터 기록을 위해 DB에 저장하여 DBMS로 관리
 JPA - 영구히 기록할 수 있도록 제공하는 API

API란 ?
애플리케이션 프로그래밍 인터페이스
인터페이스를 통해 프로그래밍을 하여 프로그램을 만듬.

- 인터페이스란?
약속.
A,B,C 존재 시
B가 선언한 약속을 A,C가 지켜주는 것.
상의가 불필요. 선포하면 지켜야만 함.
그러므로 상하관계가 존재하는 약속.

- 프로토콜이란?
약속.
A,B,C 존재 시 모두 관계가 평등
서로에게 잘 맞는 프로토콜(약속)을 타협하여 정함

JPA는 JAVA PERSISTENCE Application Programming interface
-> 자바프로그램을 할때 영구적으로 데이터를 저장하기 위하여 필요한 인터페이스가 JPA

# 5강
10. JPA는 ORM기술이다.
- ORM
Object Relational Mapping
오브젝트를 데이터베이스에 연결하는 방법론같은 것.

Team 테이블
id - int
name - varchar
year - varchar

자바에서 이를 input하는 과정을 DML(delete, update, insert)
output하는 과정을 select한다.

이 와중, db의 언어와 자바의 언어가 서로 다름.
그러므로 이를 모델링하는 작업이 필요.

class Team{
    int id;
    String name;
    String year;
}

데이터베이스에 있는 데이터를 자바에 모델링

그런데 ORM은 Object Relation임. 이 상황과 반대
class를 먼저 생성하고 난 다음 db를 생성할 수 있다.
JPA인터페이스의 규칙을 지킨다면 ORM기술을 사용가능함.

11. JPA는 반복적 CRUD의 과정을 생략가능하게 해줌
SELECT, SELECT ALL, DELETE, UPDATE, INSERT의 과정 중
DB에서 자바로 DATA를 넘길 때 데이터의 타입이 다른데, 이 과정이 매우 힘들다(노가다)
이를 JPA에서 도와줌. 세션오픈, 쿼리전송, CONNECTION 등 일련의 과정을
단순하게 처리가능 하도록 함수 1개로 제공

# 6강
12. JPA는 영속성 컨텍스트를 가지고있다.
영속성 : 어떤 테이터를 영구적으로 저장하게 해주는 속성 - 데이터베이스에 저장
context : 모든 컨텍스트를 알고있다 - 대상에 대한 모든 것을 알고 있다.

- 자바가 select 시 영속성 컨텍스트로 이동하여 특정 데이터를 요청
영속성컨텍스트는 db에서 자료를 가져온 뒤 자바로 돌려줌

모든 영속성컨텍스트는 자동으로 처리됨.

13. JPA는 DB와 OOP의 불일치성을 해결하기 위한 방법론을 제공

Class Team{
    int id;
    String name;
    String year;
}

Class Player{
    int id;
    String name;
    int teamId; (Team의 id 참조)
}

player를 조인해서 가져올 수 있지만

Class Player{
    int id;
    String name;
    Team team;
}

으로도 가능

ORM을 통해서 db와 oop의 불일치성을 해결 가능

# 7강
14. JPA는 OOP의 관점에서 모델링을 할 수 있게 해준다. - 상속 콤포지션, 연관관계

Class Car extends EntityDate{   // 상속을 해주면 해당 부분들이 추가로 생성됨
    int id;
    String name;
    String color;
    Engine engine;
}

Car
name color engineId(oop관점에서 자동생성이 가능)
...

Class Engine extends EntityDate{
    int id;
    int power;
}

Engine
id power
...

Class EntityDate{
    TimeStamp createDate;
    TimeStamp updateDate;
}

15. 방언 처리가 용이하여 Migration하기 좋음. 유지보수에도 좋음.
추상화 객체로 원하는 db로 지정이 가능 (연결해서 사용이 가능) - 방언처리
JPA는 쉽지만 어려움 - 적응을 하면 쉽다.

# 8강
1. 스프링부트 동작원리
(1) 내장 톰켓을 가진다.
톰캣을 따로 설치할 필요 없이 바로 실행이 가능
socket - 운영체제가 가지고 있는 것.
소켓 오픈, ip주소 : 5000으로 포트 연결.
메인 스레드, 스레드가 존재.
5000, 5001, 5002로 늘어나면서 스레드가 1, 2.. 생긴다.
소켓통신은 time slice방식으로 동시동작함.
연결되어 있어 부하가 크지만 연결된 사람끼리 통신이 빠름

http 통신 - stateless방식
문서통신이 가능함.

모든데이터가 몰려있는 서버에서 개인 데이터를 관리함.(개인 집중화)

# 9강
톰켓이란 무엇인가
웹서버 - 원하는 데이터를 url로 request 시 서버가 response해주는 과정
보통 아파치를 사용.

아파치는 자바코드의 요청이 들어올 시 인식하지 못하는데
이 때 톰켓을 달아주면 읽을 수 있다(컴파일 한 뒤 html문서로 만들기 가능)

# 10강
서블릿 컨테이너
클라이언트가 요청 -> 서블릿 컨테이너 -> 최초요청이면 메모리로딩, 객체생성, init() -> ...

url : 자원 접근
uri : 식별자를 통해 접근하는 방식

spring에서는 식별자를 통해서 접근을 해야함.
특정한 파일 요청을 할 수 없다는 의미.
요청시에는 무조건 자바를 거친다.
그러므로 자바를 컴파일 할 수 있는 톰켓을 반드시 거쳐야한다.

ex)
https:///naver.com/picture/a -> uri

요청을 하게되면 서버(서블릿컨테이너, 톰켓)은
첫번 째로 서블릿 객체를 생성한다.
두번 째로 init()으로 초기화 이후 service()에서 post인지 get인지 put인지 delete 인지 확인

새로운 스레드가 생성이되면서 요청이오는 방식.
많은 스레드가 생기면 재사용 하게 됨.

리퀘스트 -> 서버는 서블릿 객체를 만든다.
필요한 메소드를 호출한다 (get)
호출시 스레드1이 생성. response시 스레드1을 할일을 다하지만 남겨둠
새로운 요청이 들어온다면 스레드1을 재사용.
동시접근 20개가 오면 스레드 20개가 만들어진다.
추가로 들어오는 5개의 요청은 (5명 대기하는 스레드는) 곧 재사용된다.

100명이 들어오면 스레드 100개를 생성 -> 풀링기술

# 12강
- 디스패처 서블릿이 무엇인가요?