IBK 시스템 필기 대비 스터디
# JAVA 프로그래밍 40문제
## 배열할당
```
ex) int[] arr =new int[n];
    int arr[] = new int[n];
  ArrayList<T> arr[] = new ArrayList[N];
arr[n] = new ArrayList<T>;
```
## 제너릭사용

제네릭은 컴파일시에 변수의 형태를 정하는것
데이터의 타입을 나중에 인스턴트 사용시에 지정

```
Class Person<T>{
    public T info; // info의 데이터 형태는 그때그때 다르다.
}
Person<String> p1 = new Person<String>();
//이 경우엔 info는 String타입
Person<StringBuilder> p2 = new Person<StringBuilder>();
//이경우에는 info가 StringBuilder 타입으로

Class Person<T,S>{
    public T info;
    public S Name; //복수도 가능
}
Person<Stirng,Intger> p1 = new Person<String,Integer>();
```

장점 - 타입 안정성을 제공한다, 타입체크 형변환 생략으로 간단한 코드

특징 - 부모클래스를 제네릭으로 지정할 경우 여러가지 자식객체로 할당가능.
```
Class Info{}
Class Num extends Info{}
Class ID extends Info()

ArrayList<Info> infoList = new ArrayList<Info>();
infoList.add(new Num); //ok
infoList.add(new ID); //Ok //가져올때 다운 캐스팅은 필요하다.

ID id =(ID) infoList.get(1);
```

제네릭의 와일드 카드
단 하나의 타입을 지정하지만, 와일드 카드'?'를 사용하면 된다. 보통 제네릭에서는 단 하나의 타입을 지정하지만. 와일드 카드는 하나 이상의 타입을 지정하는 것을 가능하게 해준다.
```
public static void print(ArrayList<? exetends Product> arr){
    //Product의 자식모두 매개변수 가능
    for(Unit u:arr){
        System.out.println(u.info);
    }
}

```
메소드에도 적용이 가능하다.
```
Class Demo{
    public <S> void Sample(S info){
        System.out.println(info);
        //S라는 미정의 파라미터 받을수잇따.
    }
}
Demo d = new Demo();
d.<String>Sampe("info");
```
extends 키워드로 특정 클래스 자식만으로 제네릭 타입 한정도 가능

## 상속
extends 부모의것 자식이 사용가능 반대불가능
부모는 여러개의 자식 가지는 것이 가능하지만 Java는 중복상속은 불가능
부모의 메소드(이름,파라미터가 같고,@Override 어노테이션사용)으로 오버라이딩 가능.
super와 super()메소드의 기능.
super() = 자신의 부모의 생성자 호출. 여러개일 경우 파라미터로 선택
super = 부모의 필드나 메소드를 사용하기 위해서 사용
ex) super.부모의 메소드 or 변수 ;
super 의 경우 바로위 슈퍼클래스에서 해당 내용이 없으면 해당내용이 있는 슈퍼클래스까지 올라가서 참조.


## 인터페이스

### 추상클래스
인스턴스 변수 ,생성자 ,일반 메소드, 추상메소드 를 가질 수 있다.
추상클래스는 인스턴스 생성이 불가능.
하위 메소드에게 일부 메소드 구현 강제시키기 위해 만든다
클래스이기 때문에 extends사용해야 하고 단일 상속해야한다.
상속으로 슈퍼클래스도 해아하고 하위클래스에서 자식객체마다 다르게 사용해야하는 메소드가 있는경우에 추상메소드로 해놓고 구현



### 인터페이스
상수 및 추상 메소드만 가질 수 있다. (추상메소드는 메소드내부 구현X)
인터페이스 구현시 인터페이스를 implements할 경우 필요 메소드 구현해야한다
때문에 한가지 공통된 특성을 다른 클래스에서 다른 행동으로 구현하게 한다.
파라미터로 인터페이스를 명시해주고 인터페이스를 구현한 객체를 넘겨받아 실행하면 같은 파라미터로 서로 다른 결과 실행 가능


## 업캐스팅 다운캐스팅
instanceof 로 무슨객체인지 알수있다.


업캐스팅 자식 > 부모 부모클래스로 업캐스팅시 자식객체의 정보 참조 불가
다운 캐스팅 부모 > 자식  명시 필요

## 기본 문법

### 자료형

- boolean  = true,false;
- byte  = -127 ~128; (8bit)
- short = -32768 ~ 32769 (16bit)

- char = 2byte 문자 (숫자 입력시 ascii code로 변환 +48)
- int = 4byte
- long = 8byte;
- float = 실수형.
- float a = 3.231f; (f로 float형 명시)   

### 형변환
char의 경우 정수와 사칙연산 수행하면
ascii 코드값으로 사칙연산 수행

#### 문자 > 숫자
- String to int

Integer.paraseInt(String);

Integer.ValueOf(String);

- String to Double, float

Double.valueOf();
Float.valueOf();

- String to Short, Long
Short.parseShort();
Long.parseLong();

#### 숫자 > 문자


String.valueOf();
Integer.toString();
Double.toString();
Float.toString();

### 오버로딩
한클래스안에 파라미터마다 다른 기능수행하는 함수생성

### 오버라이딩
부모자식 관계에서 메소드 재정의해서 사용 다형성
없을시에 더욱 상위 부모로 찾아감

# DB 20문제
## SQL 작성 (DDL, DML, DCL)

### DDL(Data Define Langugue)
데이터 정의 언어 릴레이션 생성 수정 제거


- CREATE
제약조건
PRIMARYKEY - 기본키 지정
UNIQUE KEY - 유일키 지정
NOT NULL - Null 불가 지정
CHECK - 입력할 수 있는 값의 범위 지정
FOREIGN KEY - 외래키로 지정
```
CONSTRAINT PLAYER_PK PRIMARY   KEY (PLAYER_ID),
      CONSTRAINT PLAYER_FK FOREIGN KEY (TEAM_ID) REFERENCES TEAM(TEAM_ID)
```
```
SQL > CREATE TABLE(VIEW) table
    (id NUMBER(3), name VARCHAR2(50),
    addr VARCHAR2(100), phone VARCHAR2(30),
    email VARCHAR2(100));

SQL > CREATE TABLE(VIEW) table
    (id NUMBER(3), name VARCHAR2(50),
    addr VARCHAR2(100), phone VARCHAR2(30),
    email VARCHAR2(100))
    AS SELECT * FROM address;
서브쿼리로 데이터 복사도 가능
```
- ALTER
```
ALTER TABLE address
    ADD (birth date);

ALTER TABLE adress
    ADD (name varchar2(100) DEFAULT 'NO');
    DROP COLUNM commnet;
    MODIFY phone VARCHAR2(50);
RENAME 테이블이름 TO 바꿀테이블 이름
테이블 이름 변경 가능
```

- DROP
```
DROP TABLE 테이블이름
```

### DML(Data Manipulation Langugue)
데이터 조작 언어 데터 생성 수정 제거

- SELECT

순서  = FROM 으로 테이블 가져온다. WHERE로 거른다.
GROUP BY로 소규모 그룹화 그룹화 된 데이터 조건 HAVING절에서 검사
그룹화 되어진 데이터중에서 필요한 칼럼 SELECT절에서 선택해 출력


```
SELECT [DISTINCT]columm1, colunm2
FROM TABLE
WHERE columm ='condition'
GROUP BY columm1
HAVING COUNT(columm2)
ODER BY DESC columm1, ASC columm2

HAVING 절은 GROUP BY절에서 취합한 컬럼에 대해 조건을 거는 절이다.
ex)
SELECT 부서이름, COUNT(*) AS 부서 인원
FROM 사원
GROUP BY 부서
HAVING COUNT(사번)>5;
사원이 5명인 부서만 선택해서
부서이름과 부서 인원 쿼리

```
- INSERT
```
INSERT  
INTO 테이블 이름(컬럼1,컬럼2,컬럼3)
VALUES (컬림1데이터,컬럼2데이터,컬럼3데이터), (데이터셋)
```

- UPDATE
```
UPDATE
SET 속성1 = 데이터 , 속성2 = 데이터2
WHERE 조건
조건에 맞는 행들 수정
속성들을 일괄 수정
```
- DELETE
```
DELETE
FROM 테이블 이름
WHERE 조건
```

### DCL(Data Control Langugue)
데이터 제어언어

- GRANT
```
GRANT CONNECT, RESOURCE TO SAMPLE_USER;
```
- REVOKE
```
REVOKE CONNECT, RESOURCE FROM SAMPLE_USER;
```
## 내,외부 조인
조인이란 쿼리의 결과로 얻어지는 테이블이 여러테이블을 참조해야 얻을수 있을 경우 테이블을 연결시켜 데이터를 조회하는것
- Cross Join
가능한 모든 결과값가져온다

- Inner Join
조인되는 테이블의 특정 컬럼을 지정해
컬럼의 값이 같은 경우에 튜플을생성해서 가져온다.
```
SELECT A.a B.b
FROM A INNER JOIN B ON A.컬럼 = B.컬럼
```
- Outer Join
같지 않아도 가지고온다
만약 A에만 있꼬 B에 없으면 Null값으로 지정하고 가져온다.
```
SELECT A.a B.b
FROM A OUTER JOIN B ON A.컬럼 = B.컬럼
```


## 서브쿼리

쿼리안의 쿼리
쿼리의 결과를 쿼리의 조건으로 사용

## 정규화

1. 1차 정규화

속성값의 원자화

2. 2차 정규화

부분함수 종속 제거

3. 3차 정규화

이행적 함수 종속 제거

4. BC/NF

결졍자이면서 후보키가 아닌것 제거

5. 4차  

다치종속

6. 5차

조인 종속성 제거


# 인프라 및 보안 10문제
## 네트워크 OSI 7계층

1. 물리계층
시스템의 전기적 ,물리적 표현
케이블종류, 전압 등

2. 데이터링크 계층
노드간 데이터 전송 담당 및 물리 계층 전송과정에서의 오류 수정
MAC add를 이용해서 위치를 찾아간디.

3. 네트워크 계층
라우터의 기능이 대부분 이 계층에서 자리잡는다.
라우터를 이용한 라우팅 및 패킷 전송
4. 전송 계층
최종 시스템 및 호스트사이의 연결을 관리  
보낼 데이터의 용량 속도 목적지 등을 설정한다.
- TCP
3 hand shake 연결
4 hand shake 연결해지
연결지향 자체 오류제어 및 패킷순서 재조합 기능

- UDP
주로 실시간 멀티미디어 분야에서 사용
오류교정 등 기능을 제외하고 단순히 패키승 주고받는 기능만있다.
때문에 속도가 빠르나 데이터 손실이 생길 수 있다.

5. 세션 계층
6. 표현
7. 응용


- TCP/IP
네트워크 계층의 ip프로토콜과 전송계층의 TCP프로토콜 사용
IP전달여부등을 보증하거나 하지않고 패킷이 순서대로 도착하는것을 보장하지 않는다.
TCP가 IP의 윗계층에서 이 행동을 수행해준다. 패킷 순서 배치등


## 네트워크 장비 기본적인거
허브 - 회선 관리를 위해 가까운 거리의 네트워크 들을 연결 , 네트워크 공유
리피터 - 물리계층 장비 전송되는 신호 재생
브릿지 - 데이터링크 계층 lAN과 LAN 연결 OR laN안에서의 컴퓨터 그룹 연결
라우터 - 네트워크 계층 lan과 lan연결 및 경로선택 , LAN과 WAN연결
게이트웨이 : 프로토콜 구조가 전혀다른 네트워크의 연결 수행하는장비
세션 표현 응용 계층간 연결

## 네트워크 기본

## 보안 정의
물리적인 또는 SW를 위용해 네트워크 인프라를 승인되지 않는 엑세스나 오용 오작동 파괴등 에서 보호하는것


## 정보보호의 목표
기밀성
인가된 사용자 프로세스만 시스템의 리소스에 접근해야 한다.
접근제어, 암호화 등의 방법이 있따.


무결성
네트워크를 통하여 송수신 되는 정보의 내용이 생성 또는 변경 삭제 되지않고 온전히 전달 되어야 한다
무결성 보장 위해 접근 제어, 메시지 인증등이있다.
이미 변경 된경우 변경 탐지해 복구하는 기술이나 백업등 필요

가용성
시스템이 지체없이 동작하도록 하고 합법적 사용자가 거절당하지 않고 사용할 수 있도록

데이터 백업, 중복성 유지등


## 해킹 종류

## 포트스캐닝
해커가 악의적인 공격 수행 전 취약점을 찾는 과정 중 사전 작업
해킹전에 어떤포트 열어서 서비스하느지 알아내기 위해 실행
TCP Connect 스캔으로 일일히 모든 포트 스캔


## 암호화 대칭키/비대칭키 비교
양방향 암호화: 암호화 복호화 둘다 한가지 암호로 가능
단방향 암호화 : 암호화만 가능 복호화는 다른 키로

대칭키 : 암호화에 사용된 키를 일반에게 공개하지 않고 개인이 비밀로
암호화 복호화 키가 동일
키 교환을 위한 안전한 매커니즘 전달방법필요
인증기능 X
키의 숫자 증가

비대칭키 (공개키 /개인키)
인증기능 제공 (개인키로 전사서명)
속도 느림
송신자는 공개키로 평문 암호화
수신자는 개인키로 복호화

HTTPS 사용시 웹서버는 RSA기반의 공개키인증서 설치


## 운영체제 기본


# 소프트웨어공학 10문제

# IT상식 10문제
