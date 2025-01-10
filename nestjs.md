# Nest js

#### Relation And Populate

##### In node js

staff_id:{
type:mongoose.Schema.TYpes.ObjectId,
ref:"Staff"
}

().populate("staff_id)

#### Path and Math

staff_id:[{
type:mongoose.Schema.TYpes.ObjectId,
ref:"Staff"
}}

.populate({
path:"staf_id",
match:{
name:"Sachin",
email:"sachin@gmail.com"
}
})

--> use like

```js
.populate({
path:"staf_id",
match:{
email:{
$regex:
}
}
})

{
$eq:""
}


{
$ne:""
}
```
#### Sorting & Limit

```js
.populate({
path:"staf_id",
select:"-_id name",
options:{
    sort:{ name:"-1"}
    limit:2
}
})
```

#### Nested Pupulation

auth -> post -> comments

find({naem:"sachin}).populate({
    path:"Post",
    populate:{
        path:"comments
         populate:{
        path:"comments
       }
    }
})

