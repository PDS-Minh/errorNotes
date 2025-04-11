앞서 MongoDB Compass 를 사용하여 간단한 조작을 통해 데이터를 조회, 추가, 갱신, 삭제를 할 수 있습니다.

하지만 프로그래밍적으로 데이터를 입력할 때는 직접 쿼리문을 입력하여 데이터 조작을 할 수 있습니다.

이를 CRUD(Create Read Update Delete) 라고 합니다.

Link => [MongoDB manual](https://www.mongodb.com/ko-kr/docs/manual/crud/)

# Create

collection에 데이터를 만드는 방법은 두 가지 입니다

* db.collection.insertOne()

* db.collection.insertMany()

이름에서 볼 수 있듯이 insertOne은 1개의 데이터를, insertMany는 여러개의 데이터를 일괄 입력할 때 사용합니다.
insert 의 기본 구조는 다음과 같습니다.

```
db.collection.insertOne(
    <document>,
    {
      writeConcern: <document>
    }
)
```

## insertOne

우리가 추가했던 가상 인물들을 MongoDB 에 넣을 때 쿼리문으로 표현하면 다음과 같습니다.

```
db.users.insertOne({
  "name": "Martine",
  "age": 33,
  "phone": "010-2222-3333",
  "hobby": [
	"read book",
	"soccer"
  ]
})
```

## insertMany

데이터를 일괄 입력할때는 Json Array 형태로 한번에 입력할 수 있습니다.

```
db.users.insertMany([
{
  "name": "Martine",
  "age": 33,
  "phone": "010-2222-3333",
  "hobby": [
	"read book",
	"soccer"
  ]
},
{
  "name": "Smith",
  "age": 30,
  "phone": "010-3333-4444",
  "hobby": [
	"basketball",
	"ski"
  ]
},
{
  "name": "Bob",
  "age": 32,
  "phone": "010-4444-5555",
  "hobby": [
	"bycicle",
	"baseball"
  ]
}
])
```

# Read

MongoDB 에서 데이터를 조회하는 방법은 다음과 같습니다.

```
db.users.find({ // collection
  name: "Bob",  // query
  age: { $gte: 30 } 
},{ // projection
  name: 1,
  age: 1
}).limit(3) // cursor modifier
```
* query 는 데이터 작업을 하기 위한 영역 입니다.

* projection 은 데이터 중 원하는 필드만 보거나, 감출 때 사용합니다.

위와 같이 name, age 에 1 값을 할당하여 조회하면 name 과 age 만 볼 수 있습니다.

MongoDB Compass 에서도 Options 를 확장하여 다양한 쿼리 옵션들을 설정할 수 있습니다.

![image](https://github.com/user-attachments/assets/c88a2c54-85c5-4f77-acb2-c16eef88c89b)

> 💡Tip
>
> age: { $gte: 30 } 에서 $gte 는 grater then 의 의미로 age 숫자가 30 이상인 항목들을 모두 조회합니다.
> 이와 비슷한 옵션으로 $gt(초과), $lt(미만), $lte(이하) 들이 있습니다.
> 비교 쿼리 => [query-comparison](https://www.mongodb.com/ko-kr/docs/manual/reference/operator/query-comparison/)

# Update

update 방법은 3가지가 있습니다.

* db.collection.updateOne() : 1개 업데이트

* db.collection.updateMany() : 여러개 업데이트

* db.collection.replaceOne() : 이 항목은 잘 쓰이지 않아서 사용하고싶다면 반드시 공식문서를 확인하세요. 

[db.collection.replaceOne](https://www.mongodb.com/ko-kr/docs/manual/reference/method/db.collection.replaceOne/#mongodb-method-db.collection.replaceOne)

update 의 기본 구조는 다음과 같습니다.

```
db.collection.updateOne(
   <filter>,
   <update>,
   {
     upsert: <boolean>,
     writeConcern: <document>,
     collation: <document>,
     arrayFilters: [ <filterdocument1>, ... ],
     hint:  <document|string>,
     let: <document>,
     sort: <document>
   }
)
```

> 💡Tip
>
> upsert 옵션은 filter 에 일치하는 조건이 없을 경우 insert 를 합니다.


**updateOne **은 조회 된 결과 1개만 데이터를 업데이트 합니다.
```
db.users.updateOne(
  { name: "Bob" },
  { $set: { age: 40 } }
);
```

**updateMany **는 조회 조건에 일치하는 데이터들 모두 업데이트 합니다.

```
db.users.updateMany(
  { age: { $gt: 30 } },
  { $set: { age: 40 } }
);
```

# Delete

삭제작업 또한 두 가지 방법이 있습니다.

* db.collection.deleteOne()

* db.collection.deleteMany()

delete 의 기본 구조는 다음과 같습니다.

```
db.collection.deleteOne(
    <filter>,
    {
      writeConcern: <document>,
      collation: <document>,
      hint: <document|string>
    }
)
```

db.collection.deleteOne은 조회 결과와 일치하는 데이터 1개를 삭제 합니다.

```
db.users.deleteOne({
  name: "Bob"
})
```

db.collection.deleteMany 는 이름과 같이 조회 결과가 일치하는 데이터를 모두 삭제합니다.

```
db.users.deleteMany({
  age: { $gt: 30 }
})
```
