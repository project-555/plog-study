# 우리는 백엔드를 배웠는가?
지금까지 배운 스프링을 사용하여 백엔드 서버를 구현하려 한다면, 사실 반쪽짜리 기능밖에 못하거나, 프론트 엔드 프레임워크 (Vue, React 등)만 사용했을 때와 별반 다를바가 없다.

왜냐하면 컨트롤러와 같은 부분은 결국 다른 개발자들의 소통 창구(API)일 뿐, 유저가 접근할 때마다 로그인 정보와 같은 개인화된 데이터를 내보낼 것이라 기대할 수 없다.

<img width="808" alt="그림1" src="https://user-images.githubusercontent.com/59782504/184634483-c619b20e-a177-4803-9a49-5383066b449b.png">

이는 위 그림에서와 같이 프론트 엔드가 보여주는 자료양은 빙산의 일각에 불구하기 때문이며, 빙하가 제대로 떠 있으려면, 즉 프론트엔드가 제대로 동작하기 위해서는 백엔드 서버를 통해 개별적인 데이터를 적절히 가져와야 한다.

# 데이터베이스

데이터 베이스는 자료가 모여있는 곳이라고 생각하면 좋다. 

엑셀, 파일과 같은 1차원적인 시스템으로도 간단히 데이터베이스를 구성할 수 있으나,_(실제로 로그와 같은 데이터는 파일로 저장한다.)_ 데이터베이스라 함은 여러 사람이 공유할 목적으로 구성되어야 하므로, 원격지에 특정한 DBMS를 두어 따로 데이터 베이스 서버를 구축하는 것이 일반적이다.

사실 초기 웹만 하더라도 데이터베이스는 필요치 않았다. HTML, CSS, JS와 같은 언어로 간단하게 웹 페이지를 구성하여 내보냈기 때문이며, 개인화된 데이터는 필요치 않았기 때문이다.

하지만 현대의 웹은 다르다. 

블로그와 같은 목적성을 띄지 않는 이상, 많은 서비스가 개인화된 데이터를 사용하기 위해 "로그인" 이라는 절차를 통해 사용자를 구분하고 개인화된 데이터베이스를 통해 주고 받고 있다.

# JPA

[Description_1](https://dbjh.tistory.com/77)

[Description_2](https://dbjh.tistory.com/80?category=853400) 

## Spring Data JPA

[Description](https://velog.io/@junho918/Spring-Data-Jpa-JPA..%EA%B7%B8%EB%9E%98-%EC%95%8C%EA%B2%A0%EC%96%B4..-%EA%B7%B8%EB%9E%98%EC%84%9C-%EC%8A%A4%ED%94%84%EB%A7%81-%EB%8D%B0%EC%9D%B4%ED%84%B0-JPA%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%93%B0%EB%8A%94%EB%8D%B0)

## Query Method

[Description](https://ppomelo.tistory.com/155)

## JPQL

[Description](https://wonit.tistory.com/470)

## QueryDSL

[Descriotion](https://ykh6242.tistory.com/107)
