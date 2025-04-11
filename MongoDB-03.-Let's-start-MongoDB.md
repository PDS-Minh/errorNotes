본격적으로 MongoDB를 사용해봅시다.

# MongoDB의 구성

기본적으로 Database 가 있고 그 하위에 데이터가 저장 될 collection 이 있습니다.

RDBMS로 비유하면 collection 은 table 과 같은 개념 입니다.

# Create Database & Collection

새로운 Database를 만들어보겠습니다.

1. create database click

![image](https://github.com/user-attachments/assets/121143e8-6b7d-4548-8a6d-46fabbb369ff)

2. Database & collection name 설정

Database 의 이름을 지을 때 권장사항은 다음과 같습니다.

* 알파벳(A-Z, a-z), 숫자(0-9), 밑줄(_)

* 일반적으로 소문자를 사용하는 것이 권장됩니다.

저는 mydatabase 로 설정하겠습니다.

Collection 의 이름을 지을 때 권장사항은 다음과 같습니다.

* 알파벳(A-Z, a-z), 숫자(0-9), 밑줄(_), 마침표(.)

* 일반적으로 소문자와 밑줄(_) 또는 카멜 케이스(camelCase) 사용을 권장합니다.

저는 예시로 users 로 하겠습니다.

3. Create Database click

![image](https://github.com/user-attachments/assets/6eb811af-7b1b-40e6-8388-71dd06a2b535)

새로운 Database 와 collection이 생성됐습니다.

다른 collection 을 추가하고 싶으면 자유롭게 추가 할 수 있습니다.

![image](https://github.com/user-attachments/assets/d33d7f6b-671d-4903-90f0-d189c7292f13)

# Edit Data

Collection 에 데이터를 넣어보겠습니다.

편리한 기능으로 Import Data 버튼을 눌러 데이터를 CSV나 JSON 데이터를 일괄 입력 할 수도 있고 직접 쿼리문을 작성하여 입력을 할 수도 있습니다.

## Insert Document(add data)

ADD DATA 버튼을 눌러 Insert Document 를 클릭합니다.

![image](https://github.com/user-attachments/assets/f5d57a05-ce97-4b51-a27e-de7c896a14a2)

데이터는 반드시 각자 고유의 ID 값을 가져야 합니다. 

MongoDB는 기본적으로 _id 라는 ObjectID 가 생성이 됩니다.

Insert 버튼을 클릭합니다.

![image](https://github.com/user-attachments/assets/7cd38d7c-5636-41d7-ada4-f9d8725bc5c0)

데이터가 생겼습니다.

![image](https://github.com/user-attachments/assets/14787226-cbc7-4372-a2e5-535a89f5f93f)

## Update Data

여기에 내가 넣고싶은 데이터를 넣어줍니다.

데이터는 JSON 규칙으로 입력할 수 있습니다.

1. 편집하고 싶은 데이터에 마우스를 올리면 4 가지 버튼이 나옵니다.

첫번 째 Edit document 버튼을 클릭합니다.

![image](https://github.com/user-attachments/assets/2ca176d8-763c-46ad-a8c8-2d4f00441682)

2. UPDATE 버튼을 클릭합니다.

![image](https://github.com/user-attachments/assets/66d84a5d-85d2-436a-a5d3-5388b451683f)

3. $set 내부에 간단한 정보들을 입력하고 Update 1document 를 클릭합니다.

MongoDB 에서 업데이트 할 내용들은 `$set : {}` 에 적어줘야 합니다.

![image](https://github.com/user-attachments/assets/1ad331fb-a990-4aa6-b453-e4fbef614293)

4. find 버튼을 누르면 업데이트 된 정보를 확인할 수 있습니다.

![image](https://github.com/user-attachments/assets/cbc75338-8290-4dc9-ac30-f8d028590b3d)

## Select(find)

1. clone 버튼을 클릭하여 데이터를 복제할 수 있습니다.

![image](https://github.com/user-attachments/assets/68921868-4453-475b-bf50-860a1dbb077b)

2. 다음과 같이 입력하고 Insert 버튼을 클릭합니다.

![image](https://github.com/user-attachments/assets/f95dce10-d61f-4994-b434-aaa7b64486ed)

3. Find 혹은 Refresh 를 클릯하여 업데이트 된 데이터를 확인

![image](https://github.com/user-attachments/assets/b37fa2aa-b8b1-461f-9086-0f0cf8d28163)


```json

"name": "Martine",
"age": 33,
"phone": "010-2222-3333",
"hobby": [
	"read book",
	"soccer"
]


"name": "Smith",
"age": 30,
"phone": "010-3333-4444",
"hobby": [
	"basketball",
	"ski"
]

"name": "Bob",
"age": 32,
"phone": "010-4444-5555",
"hobby": [
	"bycicle",
	"baseball"
]

```

본격적으로 원하는 데이터를 조회해봅니다.

예를 들어 name 이 Bob 인 사람을 찾고 싶습니다.

상단의 filter `{}` 에 원하는 조건을 입력하고 find 를 클릭하면 원하는 데이터를 찾을 수 있습니다.

이 외에 다양한 조회 조건들이 있습니다. 

filter 에 조회조건 입력

![image](https://github.com/user-attachments/assets/94b6425c-25ee-44bb-a583-a690362a535c)

조회 결과

![image](https://github.com/user-attachments/assets/800e7024-87aa-4fd3-826e-277eb36a2e14)

## Delete Data

Reset 버튼을 눌러 조회조건을 초기화 합니다.

데이터를 삭제 해보겠습니다.

데이터 삭제 종류는 Hard Delete 와 Soft Delete 가 있습니다.

* Hard Delete: 물리적으로 완전히 제거하는 방법.

가장 깔끔한 방법이지만 가장 조심해야 할 방법 입니다.

* Soft Delete: 프로그램적으로 제거하는 방법.

flag 값을 추가하여 보여 줄 데이터와 감출 데이터를 구분합니다. (ex) isDelete: true

지금은 테스트 데이터라 자유롭게 추가, 삭제를 해도 상관이 없지만 

실제 사용하는 데이터를 편집할 때는 Hard Delete 를 가급적 지양해야 합니다.

데이터를 삭제하는 방법은 간단합니다.

삭제 할 데이터에 마우스를 올리고 4번 째 아이콘, 휴지통 버튼을 클릭하면 됩니다.

![image](https://github.com/user-attachments/assets/dee5d175-ee08-4683-b0fe-a06db1b2325b)

Delete click

![image](https://github.com/user-attachments/assets/6ab9a133-aa8d-4f4a-a188-0b2f98231321)







