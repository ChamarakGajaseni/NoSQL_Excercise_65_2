# 3. MongoDB
![image](https://user-images.githubusercontent.com/92835483/229438897-741547fe-efd7-4c37-a6f0-42bd281600aa.png)
![image](https://user-images.githubusercontent.com/92835483/229438943-882058b0-f923-4e20-a2aa-6b1134356471.png)
![image](https://user-images.githubusercontent.com/92835483/229438965-635acbfd-e955-4132-ad48-654b4431189b.png)

- **mongosh**: Create database
```
use students_score
```
- **mongosh**: Create collection & document
```
db.Students.insertMany([
{"name":"Ramesh","subject":"maths","marks":87},
{"name":"Ramesh","subject":"english","marks":59},
{"name":"Ramesh","subject":"science","marks":77},
{"name":"Rav","subject":"maths","marks":62},
{"name":"Rav","subject":"english","marks":83},
{"name":"Rav","subject":"science","marks":71},
{"name":"Alison","subject":"maths","marks":84},
{"name":"Alison","subject":"english","marks":82},
{"name":"Alison","subject":"science","marks":86},
{"name":"Steve","subject":"maths","marks":81},
{"name":"Steve","subject":"english","marks":89},
{"name":"Steve","subject":"science","marks":77},
{"name":"Jan","subject":"english","marks":0,"reason":"absent"}
])
```
-Find the total marks for each student across all subjects:
```
db.Students.aggregate([
  {
    $group: {
      _id: "$name",
      totalMarks: { $sum: "$marks" }
    }
  }
])
```
-Find the maximum marks scored in each subject:
```
db.Students.aggregate([
  {
    $group: {
      _id: "$subject",
      maxMarks: { $max: "$marks" }
    }
  }
])
```
-Find the minimum marks scored by each student:
```
db.Students.aggregate([
  {
    $group: {
      _id: "$name",
      minMarks: { $min: "$marks" }
    }
  }
])
```
-Find the top two subjects based on average marks:
```
db.Students.aggregate([
  {
    $group: {
      _id: "$subject",
      avgMarks: { $avg: "$marks" }
    }
  },
  {
    $sort: { avgMarks: -1 }
  },
  {
    $limit: 2
  }
])
```
