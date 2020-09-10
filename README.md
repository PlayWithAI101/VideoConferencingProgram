
# 실시간 화상 토론 서비스

## 역할
서버: 김재현, 안예지 <br>
클라이언트: 고진호, 진선경


## 스킬셋
- Python
- Raspberrypi
- PuTTY
- mjpg-streamer
- JSP
- Apache Tomcat
- TCP 프로토콜

<br>

## 목차
1. [화상 토론 서비스 개요](#1-화상-토론-서비스-개요)
2. [프로그램 구성도](#2-프로그램-구성도)
3. [주요 기능](#3-주요-기능)
4. [시연](#4-시연)
5. [애로사항](#5-애로사항)

<br><br>



## 1. 화상 토론 서비스 개요
- 모든 토론 참가자는 라즈베리 카메라를 이용하여 영상 촬영
- 서버에서 프로그램에 입장한 참가자의 ip주소를 이용하여 참가자들의 영상에 접근가능 (mjpg 이용)
- 모든 참가자들의 영상을 담는 웹 페이지에 해당 영상들을 모아서 송출
- 현재 발언권을 잡은 참가자의 영상이 중앙에 배치됨
- 발언 시간이 지나면 자동으로 다음 참가자의 영상이 중앙에 배치되게 변경

<br>

## 2. 프로그램 구성도
<img src="https://user-images.githubusercontent.com/62331803/92752938-585f4680-f3c4-11ea-9657-5306b7d1b014.png" width="70%">
<br>

## 3. 주요 기능
### A. 클라이언트 입장 : 연결된 소켓과 ip정보 딕셔너리에 추가 
<img src="https://user-images.githubusercontent.com/62331803/92749824-70819680-f3c1-11ea-9ad7-86aa3dca4479.png" width="50%">
<img src="https://user-images.githubusercontent.com/62331803/92749922-8c853800-f3c1-11ea-8b81-68c9bff77750.png" width="70%">
<br>

### B. 발언신청 : 클라이언트가 발언신청을 하면, 서버에서 신청 조건을 확인하고 발언대기 큐에 추가
<img src="https://user-images.githubusercontent.com/62331803/92750126-bc344000-f3c1-11ea-85a1-d442426c1e4b.png" width="50%">
<img src="https://user-images.githubusercontent.com/62331803/92750228-d706b480-f3c1-11ea-99fb-5a87394ab911.png" width="80%">
<br>

### C. 의견발언 
<img src="https://user-images.githubusercontent.com/62331803/92750372-f6054680-f3c1-11ea-954b-9bffc8c7ff15.png" width="50%">
<img src="https://user-images.githubusercontent.com/62331803/92750466-0b7a7080-f3c2-11ea-8d29-a92104a8e569.png" width="80%">
<br>

### D. 발언중단 : 발언 중인 클라이언트가 할당된 시간 내에 발언이 모두 끝났을 경우 중단요청
<img src="https://user-images.githubusercontent.com/62331803/92750528-1b925000-f3c2-11ea-82c9-494618cbb13e.png" width="50%">
<img src="https://user-images.githubusercontent.com/62331803/92750594-31077a00-f3c2-11ea-88e2-e7bceadb8e29.png" width="80%">
<br>

### E. 발언취소 : 클라이언트가 발언하겠다고 신청한 내역을 취소하고 싶을 때 취소요청
<img src="https://user-images.githubusercontent.com/62331803/92750670-47153a80-f3c2-11ea-9478-150bb27feff1.png" width="50%">
<img src="https://user-images.githubusercontent.com/62331803/92750778-5eecbe80-f3c2-11ea-8e7d-cc15c60143ad.png" width="80%">
<br>

### F. 클라이언트 퇴장 : 퇴장 요청한 클라이언트의 소켓과 ip정보 딕셔너리에서 제거
<img src="https://user-images.githubusercontent.com/62331803/92750854-6d3ada80-f3c2-11ea-8763-dba4e169523d.png" width="50%">
<img src="https://user-images.githubusercontent.com/62331803/92750935-7f1c7d80-f3c2-11ea-8f52-d9f1162adf70.png" width="80%">
<br>

## 4. 시연
<img src="https://user-images.githubusercontent.com/62331803/92751014-922f4d80-f3c2-11ea-8b5a-09ff3f9fd52f.png" width="50%">

- 왼편에 현재 발언권자, 오른편에 나머지 토론 참가자가 위치해 있다.
- 현재 발언권을 잡은 사람만 텍스트를 입력할 수 있으며
- 서버는 발언권자의 메세지를 받아 모든 참가자에게 전달한다.

<br>

## 5. 애로사항
<img src="https://user-images.githubusercontent.com/62331803/92751105-a7a47780-f3c2-11ea-940b-63128fe7b20d.png" width="50%">
