# Hobserver
###  - 드론과 자율주행 로봇을 이용한 항만 감시 시스템   

![image](https://user-images.githubusercontent.com/24893215/95682434-2b4ebf80-0c20-11eb-9f3c-77334a34f68f.png)

 - Embedded-Software-2020_ Smart things 부문 출품작

## 1) 프로젝트 개요

   
항만은 크기가 너무 넓어 감시하기가 까다롭고, 보안상의 허점이 많아 범죄의 표적이 되기쉽다.    
특히 밀입국과 도난사고가 잦은데, 이를 감시하기 위해서는 많은 인력과 노력이 필요하다.   
이를 극복하기 위해 우리는 항만 감시 시스템인 Hobserver를 고안하게 되었고    
이는 자동화 시스템으로써 보안과 관련해 발생하는 비용적 부담을 절감하는 효과를 가져올 것이다.


## 2) How to build

 ![image](https://user-images.githubusercontent.com/24893215/95682473-5fc27b80-0c20-11eb-8b05-326d5c64cded.png)

### 1. HW

HW 구성

![image](https://user-images.githubusercontent.com/24893215/95682523-9f896300-0c20-11eb-9420-d8631554e86d.png)


 본 프로젝트 Hobserver에서 하드웨어는 자율주행 감시로봇(TurtleBot3), 항만Observer(CoDroneII),
 OTP 인증모듈(ATmega128)로 구성되어 있다. 하드웨어의 전체적인 구성은 다음과 같다.

 - 드론

 ![image](https://user-images.githubusercontent.com/24893215/95682602-0e66bc00-0c21-11eb-9b87-a286c36e0f6f.png)

구역마다 항만 위를 비행하며 항만을 감시하다가 객체를 탐지하면 서버로 객체의 좌표와 항만의 현장 사진을 보낸다.

 - Turtlebot

 ![image](https://user-images.githubusercontent.com/24893215/95682645-5c7bbf80-0c21-11eb-863d-ebbb09b643cc.png)

 항만의 지상에서 대기모드를 유지하고 있다가 
 서버로부터 객체의 위치 경로를 받으면
 해당 경로에 맞춰 주행해 객체를 찾고, 
 객체를 발견하면 OTP인증을 요청한다.

 - OTP 모듈(ATmega128)

 ![image](https://user-images.githubusercontent.com/24893215/95682685-94830280-0c21-11eb-815a-dd5ffe084a49.png)

 자율주행 감시 로봇에 부착되어 있으며 서버로부터 OTP인증 요청 신호를 받으면OTP인증을 실행한다. 


### 2. SW

SW 구성 

![image](https://user-images.githubusercontent.com/24893215/95683185-99958100-0c24-11eb-858f-0f4e27653893.png)


-  드론의 객체 인식 및 추적 알고리즘

드론은 객체를 발견한 뒤 카메라에 포착된 이미지를 바로 전송하는 것이 아닌 객체의 위치 
데이터를 추출하고 담당하고 있는 구역 전체를 담기 위해 여러가지 이미지 operation과정을
거친다. 이러한 과정을 거쳐 적절한 이미지라고 판단되면 서버로 데이터를 전송한다.
데이터를 전송한 드론은 서버의 답변이 오기 전까지는 객체를 추적한다. 
추적 모드의 드론에게 서버로부터 객체를 이미지와 관련해 재탐색을 요청하면 앞선 과정을 
되풀이 하고 종료하라는 응답이 오면 다시 감시 모드로 돌아가 항만을 비행한다.

-  서버의 항만 맵 도출 및 경로 데이터 생성 알고리즘

서버는 항시 통신 대기모드를 유지하고 있으며 드론으로부터 데이터가 들어오면 다음과 같은 
과정을 통해 객체를 추적할 수 있게 연산을 하며 인증 결과를 바탕으로 판단을 내리는 역할을
 한다. 

- 터틀봇의 객체 추적 및 OTP인증 알고리즘

터틀봇은 서버로부터 받은 경로대로 이동하면서 목적지까지 도달한다. 이때 터틀봇이 자체적으로 객체의 
판단 유무를 처리하지 않고 서버에게 객체 발견 판단을 위임하여 OTP와 같은 인증시도와 
결과 값을 주고 받으며 서버와 계속 통신하도록 한다. 



### 3. web

![image](https://user-images.githubusercontent.com/24893215/95683470-68b64b80-0c26-11eb-9b3c-706016f9d648.png)

관제 시스템 화면 구성시, 사람의 직접적인 개입 없이도 간접적으로 모든 상황을 한눈에 파악할 수 있도록 현장을 담은 영상이나 
이미지들로 배치하였다. 최상단에는 OTP인증 결과를 나타내는 텍스트를 배치하였고 좌측 상단에는 터틀봇의 시야의 웹 캠을 두어 
지상에서의 항만 상황이 보일 수 있도록 하였다. 우측 상단에는 드론이 전송한 객체 포착 이미지를, 하단 좌측에는 항만 이미지로 도출한 항만의 맵,
우측에는 침입자의 모습을 담은 현장 사진을 배치하였다.






## 3) Member
정현성, 조혜영, 박민정, 배한빈
## 4) Deadline
참가 신청 및 개발계획서 제출 :	2020년 05월 07일 ~ 06월 08일   
본선진출팀 기술지원 교육 :	2020년 07월 ~ 09월   
본선진출팀 개발완료보고서 제출 :	2020년 09월 07일 ~ 10월 12일 (연장)  
결선 :	2020년 12월 09일 ~ 12월 11일   
