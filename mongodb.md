
```json
db.mydata.insertOne( 
        { 
course: "BDA", 
details: { 
duration: "six months", 
Trainer: "Tushar Kute" 
}, 
Batch: [{ size: "small", qty: 10 }, { size: "Medium", qty: 30 }], 
category: "Data Science" 
}
)

```

insert data in document

```json
db.student.insert({'roll':2,'name':'Pramod','marks':90.31})
db.student.insert({'roll':3,'name':'Priya','marks':73.22})
db.student.insert({'roll':4,'name':'Amar','class':'SY'})
db.student.insert({'roll':5,'name':'Akash','class':'TY','marks':90.31})
```

```json
pgdbda@dbda-HP-406-G1-MT> db.student.find({roll:{$eq:3}})
[
  {
    _id: ObjectId("64537446bd841bd486e8e4f5"),
    roll: 3,
    name: 'Priya',
    marks: 73.22
  }
]

```

not equal to conidtional operator

```json
pgdbda@dbda-HP-406-G1-MT> db.student.find({name:{$ne:'Priya'}}).pretty()
[
  {
    _id: ObjectId("64536db3bd841bd486e8e4ee"),
    roll: 1,
    name: 'dobby',
    marks: 43.23
  },
  {
    _id: ObjectId("64537446bd841bd486e8e4f4"),
    roll: 2,
    name: 'Pramod',
    marks: 90.31
  },
  {
    _id: ObjectId("64537446bd841bd486e8e4f6"),
    roll: 4,
    name: 'Amar',
    class: 'SY'
  },
  {
    _id: ObjectId("64537446bd841bd486e8e4f7"),
    roll: 5,
    name: 'Akash',
    class: 'TY',
    marks: 90.31
  }
]

```

conidtional operator

```json
pgdbda@dbda-HP-406-G1-MT> db.student.find({class:'TY',marks:{$gt:50}})
[
  {
    _id: ObjectId("64537446bd841bd486e8e4f7"),
    roll: 5,
    name: 'Akash',
    class: 'TY',
    marks: 90.31
  }
]

```
OR condition

```json

pgdbda@dbda-HP-406-G1-MT> db.student.find({$or:[{class:'TY'},{marks:{$gt:50}}]})
[
  {
    _id: ObjectId("64537446bd841bd486e8e4f4"),
    roll: 2,
    name: 'Pramod',
    marks: 90.31
  },
  {
    _id: ObjectId("64537446bd841bd486e8e4f5"),
    roll: 3,
    name: 'Priya',
    marks: 73.22
  },
  {
    _id: ObjectId("64537446bd841bd486e8e4f7"),
    roll: 5,
    name: 'Akash',
    class: 'TY',
    marks: 90.31
  }
]

```

create a variable with documents and call it on a insert query

```json
var Allcourses=
[
    {
        course:"java",
        details: {Duration:"six months",Trainer:"Tushar Kute"},
        Batch:[{size:"Medium",qty:25}],
        category:"Programming Language"
        
        
    },
    {
        course:"Python",
        details:{Duration:"three months",Trainer:"Rashmi Thorave"},
        Batch:[{size:"Small",qty:10},{size:"Large",qty:30}],
        category:"Programming Language"
    }
];

input:
db.mydata.insert(Allcourses)

output:
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("64537c92bd841bd486e8e4f8"),
    '1': ObjectId("64537c92bd841bd486e8e4f9")
  }
}

```
update query

```json
db.student.update({roll:3},{$set:{marks:70.23}})
db.student.update({roll:3},{$set:{marks:70.23,age:20}})

```
update multiple command values

```json
db.student.update({},{$set:{college:'cdac'}},{multi:true})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 5,
  modifiedCount: 4,
  upsertedCount: 0
}

```

```json
db.student.save({ '_id': ObjectId("64537446bd841bd486e8e4f7"),roll:4,name:'Anita',marks:57.23,age:23,class:'TY'})

```
Lab Assignment from detailed syllabus pdf:

creating a document restaurant

```json
pgdbda@dbda-HP-406-G1-MT> db.restaurant.find({cuisine:{$ne:'American'},long:{$lt:65.754168},score:{$gt:70}})
[
  {
    _id: ObjectId("64539315895ceb11d22053b9"),
    name: 'First',
    cuisine: 'Indian',
    score: 87.12,
    grade: 'B',
    long: 56.78,
    lat: 89.23,
    city: 'New York'
  },
  {
    _id: ObjectId("64539474895ceb11d22053ba"),
    name: 'First',
    cuisine: 'Indian',
    score: 87.12,
    grade: 'B',
    long: 59.78,
    lat: 89.23,
    city: 'New York'
  },
  {
    _id: ObjectId("64539474895ceb11d22053bd"),
    name: 'Fourth',
    cuisine: 'Mexican',
    score: 82.89,
    grade: 'A',
    long: 50.78,
    lat: 89.23,
    city: 'Texas'
  }
]

db.restaurant.insert({name:'First', cuisine:'Indian', score:87.12, grade:'B', long:59.78, lat:89.23, city:'New York' })
db.restaur _id: ObjectId("64539315895ceb11d22053b9")ant.insert({name:'Second', cuisine:'American', score:47.12, grade:'c', long:86.78, lat:89.23, city:'washington dc' })
db.restaurant.insert({name:'Third', cuisine:'American', score:91.66, grade:'A', long:96.78, lat:89.23, city:'Brooklyn' })
db.restaurant.insert({name:'Fourth', cuisine:'Mexican', score:82.89, grade:'A', long:50.78, lat:89.23, city:'Texas' })
db.restaurant.insert({name:'Fifth', cuisine:'Indian', score:77.94, grade:'B', long:6.78, lat:89.23, city:'Los Angeles' })

```

Q write a query to find the restaurants who achieved a score more than 90 using restaurants collection.
Answer:

```json
pgdbda@dbda-HP-406-G1-MT> db.restaurant.find({score:{$gt:90}})
[
  {
    _id: ObjectId("64539474895ceb11d22053bc"),
    name: 'Third',
    cuisine: 'American',
    score: 91.66,
    grade: 'A',
    long: 96.78,
    lat: 89.23,
    city: 'Brooklyn'
  }pgdbda@dbda-HP-406-G1-MT> db.restaurant.find({score:{$gt:90}})
[
  {
    _id: ObjectId("64539474895ceb11d22053bc"),
    name: 'Third',
    cuisine: 'American',
    score: 91.66,
    grade: 'A',
    long: 96.78,
    lat: 89.23,
    city: 'Brooklyn'
  }
]
]

```
Q. to find the restaurants which do not prepare any cuisine of American and achieved a score more than 70 and located int the longitude less than 65.754168 using restaurants collections
Answer:'

```json
pgdbda@dbda-HP-406-G1-MT> db.restaurant.find({cuisine:{$ne:'American'},long:{$lt:65.754168},score:{$gt:70}})
[
  {
    _id: ObjectId("64539315895ceb11d22053b9"),
    name: 'First',
    cuisine: 'Indian',
    score: 87.12,
    grade: 'B',
    long: 56.78,
    lat: 89.23,
    city: 'New York'
  },
  {
    _id: ObjectId("64539474895ceb11d22053ba"),
    name: 'First',
    cuisine: 'Indian',
    score: 87.12,
    grade: 'B',
    long: 59.78,
    lat: 89.23,
    city: 'New York'
  },
  {
    _id: ObjectId("64539474895ceb11d22053bd"),
    name: 'Fourth',
    cuisine: 'Mexican',
    score: 82.89,
    grade: 'A',
    long: 50.78,
    lat: 89.23,
    city: 'Texas'
  }
]

```
Q. to find the restaurants which do not prepare any cuisine of American and achieved a grade point A not belongs to the borough Brooklyn. The document must be displayed according to the cuisine in desc order?

Document name and fields

Restaurants
 * name
 * cuisine
 * score
 * grade
 * long
 * lat
 * city


```json

db.cricketer.insert({name:'ajay', matches:58, runs:3129,  catches:32, })
db.cricketer.insert({name:'vijay', matches:32, runs:4205,  catches:11,})
db.cricketer.insert({name:'ram', matches:230, runs:6390, catches:105, })
db.cricketer.insert({name:'ahmed', matches:192, runs:5502, wickets:13, catches:111, stumpings:11})
db.cricketer.insert({name:'akshay', matches:101, runs:699, wickets:89, catches:71, })
db.cricketer.insert({name:'prem', matches:57, runs:1054, wickets:69, catches:55, })

```

Q1. find information of all the bowlers?

```json

pgdbda@dbda-HP-406-G1-MT> db.cricketer.find({"wickets":{$exists:true}});
[
  {
    _id: ObjectId("64539c5b895ceb11d22053c3"),
    name: 'ahmed',
    matches: 192,
    runs: 5502,
    wickets: 13,
    catches: 111,
    stumpings: 11
  },
  {
    _id: ObjectId("64539c5b895ceb11d22053c4"),
    name: 'akshay',
    matches: 101,
    runs: 699,
    wickets: 89,
    catches: 71
  },
  {
    _id: ObjectId("64539c5b895ceb11d22053c5"),
    name: 'prem',
    matches: 57,
    runs: 1054,
    wickets: 69,
    catches: 55
  }
]

```

Q2. Print the information about the wicketkeepers only.

```json

pgdbda@dbda-HP-406-G1-MT> db.cricketer.find({"stumpings":{$exists:true}})
[
  {
    _id: ObjectId("64539c5b895ceb11d22053c3"),
    name: 'ahmed',
    matches: 192,
    runs: 5502,
    wickets: 13,
    catches: 111,
    stumpings: 11
  }
]

```
Q3. find the information about the player who score more than 4000 runs

```json
pgdbda@dbda-HP-406-G1-MT> db.cricketer.find({"runs":{$gt:4000}})
[
  {
    _id: ObjectId("64539c5b895ceb11d22053c1"),
    name: 'vijay',
    matches: 32,
    runs: 4205,
    catches: 11
  },
  {
    _id: ObjectId("64539c5b895ceb11d22053c2"),
    name: 'ram',
    matches: 230,
    runs: 6390,
    catches: 105
  },
  {
    _id: ObjectId("64539c5b895ceb11d22053c3"),
    name: 'ahmed',
    matches: 192,
    runs: 5502,
    wickets: 13,
    catches: 111,
    stumpings: 11
  }
]

```
q4. Delete the wickets for the player who has stumpings

```json

db.cricketer.update({stumpings:{$exists:true}},{$unset:{stumpings:""}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

```
Q5. update the matches and wickets of player 'prem' to 61 and 71

```json

pgdbda@dbda-HP-406-G1-MT> db.cricketer.update({name:"prem"},{$set:{matches:61,wickets:71}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

```
Q6. print the information of player who have take more than 50 wickets.

```json

db.cricketer.find({wickets:{$gt:50}})
[
  {
    _id: ObjectId("64539c5b895ceb11d22053c4"),
    name: 'akshay',
    matches: 101,
    runs: 699,
    wickets: 89,
    catches: 71
  },
  {
    _id: ObjectId("64539c5b895ceb11d22053c5"),
    name: 'prem',
    matches: 61,
    runs: 1054,
    wickets: 71,
    catches: 55
  }
]

```

