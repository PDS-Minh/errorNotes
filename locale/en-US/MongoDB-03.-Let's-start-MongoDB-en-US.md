Let's start using MongoDB.

# Configuring MongoDB

By default, there is Database, and there is a collection under which the data will be stored.

If you compare it to RDBMS, collection is a concept like table.

# Create Database & Collection

Create a new Database.

1. create database click

![image](https://github.com/user-attachments/assets/121143e8-6b7d-4548-8a6d-46fabbb369ff)

2. Set Database & collection name

Recommendations for naming a database are as follows.

* Alphabet(A-Z, a-z), number(0-9), underscore(_)

* It is generally recommended to use lowercase letters.

I set the database name to "mydatabase".

The recommendations for naming a collection are as follows.

* Alphabet(A-Z, a-z), number(0-9), underscore(_), comma(.)

* Generally, lowercase and underscore (_) or camelCase are recommended.

I set the collection name to "users".

3. Create Database click

![image](https://github.com/user-attachments/assets/6eb811af-7b1b-40e6-8388-71dd06a2b535)

New Database and collection have been created.

If you want to add another collection, you are free to add it.

![image](https://github.com/user-attachments/assets/d33d7f6b-671d-4903-90f0-d189c7292f13)

# Edit Data

Let's put the data into the Collection.

For convenient functions, you can press the Import Data button to input data in a batch of CSV or JSON data, or you can write and input a query statement yourself.

## Insert Document(add data)

Press the ADD DATA button and click Insert Document.

![image](https://github.com/user-attachments/assets/f5d57a05-ce97-4b51-a27e-de7c896a14a2)

Each data must have its own ID value.

MongoDB generates an ObjectID named _id by default.

Click the Insert button.

![image](https://github.com/user-attachments/assets/7cd38d7c-5636-41d7-ada4-f9d8725bc5c0)

generates a new data.

![image](https://github.com/user-attachments/assets/14787226-cbc7-4372-a2e5-535a89f5f93f)

## Update Data

I put the data I want to put in here.

Data can be entered by JSON rules.

1. When you mouse over the data you want to edit, you get four buttons.

Click the first Edit document button.

![image](https://github.com/user-attachments/assets/2ca176d8-763c-46ad-a8c8-2d4f00441682)

2. Click the UPDATE button.

![image](https://github.com/user-attachments/assets/66d84a5d-85d2-436a-a5d3-5388b451683f)

3. Enter simple information inside $set and click Update 1 document.

The contents to be updated in MongoDB should be written in `$set:{}`.

![image](https://github.com/user-attachments/assets/1ad331fb-a990-4aa6-b453-e4fbef614293)

4. You can click the find button to see the updated information.

![image](https://github.com/user-attachments/assets/cbc75338-8290-4dc9-ac30-f8d028590b3d)


1. You can replicate the data by clicking the clone button.

![image](https://github.com/user-attachments/assets/68921868-4453-475b-bf50-860a1dbb077b)

2. Type the following and click the Insert button.

![image](https://github.com/user-attachments/assets/f95dce10-d61f-4994-b434-aaa7b64486ed)

3. Click Find or Refresh to see updated data.

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

## Select(find)

Let's check the data you want in earnest.

For example, I want to find someone whose name is Bob.

You can find the desired data by entering the desired condition in the filter `{}` at the top and clicking find.

In addition, there are various inquiry conditions.

1. Enter the query in filter.

![image](https://github.com/user-attachments/assets/94b6425c-25ee-44bb-a583-a690362a535c)

2. Find result

![image](https://github.com/user-attachments/assets/800e7024-87aa-4fd3-826e-277eb36a2e14)

## Delete Data

Press the Reset button to initialize the query condition.

I'll try to delete the data.

There are two types of data deletion: Hard Delete and Soft Delete.

* Hard Delete: How to physically remove it completely.

It's the cleanest way, but it's the one to be most careful.

* Soft Delete: How to remove it programmatically.

Add a flag value to distinguish between the data you want to show and the hidden data. (ex) isDelete: true

It's test data, so it doesn't matter if you add or delete it freely

When editing actual data, avoid Hard Delete as much as possible.

The way to delete data is simple.

Simply mouse over the data you want to delete and click the 4th icon, Trash button.

![image](https://github.com/user-attachments/assets/dee5d175-ee08-4683-b0fe-a06db1b2325b)

Delete click

![image](https://github.com/user-attachments/assets/6ab9a133-aa8d-4f4a-a188-0b2f98231321)







