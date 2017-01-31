# Monggo DB - Query

Mempelajari dasar-dasar query yang dibutuhkan untuk menciptakan database di MongoDB.


## 1. Membuat database 'Academic'

```
use academic
```

## result

```
switched to db academic
```

## 2. Menampilkan semua collection dan data dalam database

```
show collection
```

## result (karena belum ada collection, jadi tampilan kosong )

```

```

## 3. Membuat atau mengaktifkan database

```
use academic
```

## result
```
 switched to db academic
```


## 4. Membuat Collection "departments"
```
 db.createCollection("departments")
 ```

## result
```
{ "ok" : 1 }
```


## 5. Membuat Collection "students"
```
 db.createCollection("students")
 ```

## result
```
{ "ok" : 1 }
```


## 6. Melihat Collection "students"
```
db.students.find()
```

## result (karena belum ada data, jadi tampilan kosong)
```
```

## 7. Masukan 5 data dalam collection "departments"
```
 db.departments.insertMany([
  {
    code  : "SI001",
    name  : "System Informasi & Akuntasi",
    Major : "Teknologi Komputer"
  },
  {
    code  : "SI002",
    name  : "System Informasi & Matematika",
    Major : "Teknologi Komputer"
  },
  {
    code  : "IT001",
    name  : "Teknik informatika",
    Major : "Teknologi Komputer"
  },
  {
    code  : "MT001",
    name  : "Multimedia Teknologi",
    Major : "Teknologi Komputer"
  }
 ])
```
## result
```
 {
	"acknowledged" : true,
	"insertedIds" : [
		ObjectId("58900d995e588439d57a99b5"),
		ObjectId("58900d995e588439d57a99b6"),
		ObjectId("58900d995e588439d57a99b7"),
		ObjectId("58900d995e588439d57a99b8")
	]
}
```

## 8. Masukan 3 data dalam Collection "students" beserta references ke "departments"
```
 db.students.insertMany([
  {
    studentId:"1401082057",
   name:"Willy",
   address:"Gang kelinci no 15,blok P2",
   department : {
                   $ref : "departments",
                   $id  : ObjectId("58900d995e588439d57a99b5"),
                   $db  : "academic"
                }
  },
  {
    studentId:"1401082058",
   name:"Iqbal",
   address:"Bandung, Taman Qblol no 10,blok P2",
   department : {
                   $ref : "departments",
                   $id  : ObjectId("58900d995e588439d57a99b6"),
                   $db  : "academic"
                }
  },
  {
    studentId:"1401082057",
   name:"mandra",
   address:"Gang badak no 15,blok P2",
   department : {
                   $ref : "departments",
                   $id  : ObjectId("58900d995e588439d57a99b6"),
                   $db  : "academic"
                }
  }
  ])
```
## result
```
{
    "acknowledged" : true,
    "insertedIds" : [
        ObjectId("589017227c7cadb6dad71454"),
        ObjectId("589017227c7cadb6dad71455"),
        ObjectId("589017227c7cadb6dad71456")
    ]
}
```

## 9. Melihat isi Collection "students"
```
 db.students.find()
 ```

## result

```
{ "_id" : ObjectId("589017227c7cadb6dad71454"), "studentId" : "1401082057", "name" : "Willy", "address" : "Gang kelinci no 15,blok P2", "department" : DBRef("departments", ObjectId("58900d995e588439d57a99b5"), "academic") }
{ "_id" : ObjectId("589017227c7cadb6dad71455"), "studentId" : "1401082058", "name" : "Iqbal", "address" : "Bandung, Taman Qblol no 10,blok P2", "department" : DBRef("departments", ObjectId("58900d995e588439d57a99b6"), "academic") }
{ "_id" : ObjectId("589017227c7cadb6dad71456"), "studentId" : "1401082057", "name" : "mandra", "address" : "Gang badak no 15,blok P2", "department" : DBRef("departments", ObjectId("58900d995e588439d57a99b6"), "academic") }"
```

## 10. Menampilkan key "name" dan "address" dalam collection "students"

```
db.students.find({},{name:true, address:true})
```

## result

```
/* 1 */
{
    "_id" : ObjectId("589017227c7cadb6dad71454"),
    "name" : "Willy",
    "address" : "Gang kelinci no 15,blok P2"
}

/* 2 */
{
    "_id" : ObjectId("589017227c7cadb6dad71455"),
    "name" : "Iqbal",
    "address" : "Bandung, Taman Qblol no 10,blok P2"
}

/* 3 */
{
    "_id" : ObjectId("589017227c7cadb6dad71456"),
    "name" : "mandra",
    "address" : "Gang badak no 15,blok P2"
}
```
## 11. Menampilkan key "studentId", "name","address",dari data student yang mempunyai "studentId" tertentu
```
db.students.find({studentId:"1401082058"})
```
## result
```
/* 1 */
{
    "_id" : ObjectId("589017227c7cadb6dad71455"),
    "studentId" : "1401082058",
    "name" : "Iqbal",
    "address" : "Bandung, Taman Qblol no 10,blok P2",
    "department" : {
        "$ref" : "departments",
        "$id" : ObjectId("58900d995e588439d57a99b6"),
        "$db" : "academic"
    }
}
```

## 12. Menampilkan key "StudentId" secara urut berdasarkan "name" dengan sort() secara ascending maupun descending

### Sort Ascending
```
db.students.find().sort({name:1})
```
### Sort Descending
```
db.students.find().sort({name:-1})
```

## result

### Descending
```
/* 1 */
{
    "_id" : ObjectId("589017227c7cadb6dad71456"),
    "studentId" : "1401082057",
    "name" : "mandra",
    "address" : "Gang badak no 15,blok P2",
    "department" : {
        "$ref" : "departments",
        "$id" : ObjectId("58900d995e588439d57a99b6"),
        "$db" : "academic"
    }
}

/* 2 */
{
    "_id" : ObjectId("589017227c7cadb6dad71454"),
    "studentId" : "1401082057",
    "name" : "Willy",
    "address" : "Gang kelinci no 15,blok P2",
    "department" : {
        "$ref" : "departments",
        "$id" : ObjectId("58900d995e588439d57a99b5"),
        "$db" : "academic"
    }
}

/* 3 */
{
    "_id" : ObjectId("589017227c7cadb6dad71455"),
    "studentId" : "1401082058",
    "name" : "Iqbal",
    "address" : "Bandung, Taman Qblol no 10,blok P2",
    "department" : {
        "$ref" : "departments",
        "$id" : ObjectId("58900d995e588439d57a99b6"),
        "$db" : "academic"
    }
}
```

## 13. Menampilkan "departments" secara urut berdasarkan "name" dengan sort() secara ascending maupun descending

### Sort Ascending
```
db.departments.find().sort({name:1})
```
### Sort Descending
```
db.departments.find().sort({name:-1})
```

## result
```
{ "_id" : ObjectId("58900d995e588439d57a99b8"), "code" : "MT001", "name" : "Multimedia Teknologi", "Major" : "Teknologi Komputer" }
{ "_id" : ObjectId("58900d995e588439d57a99b5"), "code" : "SI001", "name" : "System Informasi & Akuntasi", "Major" : "Teknologi Komputer" }
{ "_id" : ObjectId("58900d995e588439d57a99b6"), "code" : "SI002", "name" : "System Informasi & Matematika", "Major" : "Teknologi Komputer" }
{ "_id" : ObjectId("58900d995e588439d57a99b7"), "code" : "IT001", "name" : "Teknik informatika", "Major" : "Teknologi Komputer" }
```

## 14 Mencari data "students" dengan "name"
```
db.students.find({name:"Iqbal"})
```

## result

```
{ "_id" : ObjectId("589017227c7cadb6dad71455"), "studentId" : "1401082058", "name" : "Iqbal", "address" : "Bandung, Taman Qblol no 10,blok P2", "department" : DBRef("departments", ObjectId("58900d995e588439d57a99b6"), "academic") }
```
