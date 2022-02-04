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

 