DB structure

``` js
// Using MongoDB schema structure as example

  

// Users Collection

{

  _id: ObjectId,

  username: String,

  email: String,

  password: String (hashed), // Never store plain passwords

  profile_picture: String (URL),

  bio: String,

  created_at: Timestamp,

  updated_at: Timestamp

}

  

// Blogs Collection

{

  _id: ObjectId,

  title: String,

  content: String,

  author_id: ObjectId (reference to Users),

  categories: [ObjectId] (array of category IDs),

  status: String (draft/published),

  read_time: Number,

  views: Number,

  created_at: Timestamp,

  updated_at: Timestamp

}

  

// Categories Collection

{

  _id: ObjectId,

  name: String,

  description: String,

  created_at: Timestamp

}

  

// Comments Collection

{

  _id: ObjectId,

  blog_id: ObjectId (reference to Blogs),

  user_id: ObjectId (reference to Users),

  content: String,

  created_at: Timestamp,

  updated_at: Timestamp

}

  

// Likes Collection

{

  _id: ObjectId,

  blog_id: ObjectId (reference to Blogs),

  user_id: ObjectId (reference to Users),

  created_at: Timestamp

}

  

// Follows Collection

{

  _id: ObjectId,

  follower_id: ObjectId (reference to Users),

  following_id: ObjectId (reference to Users),

  created_at: Timestamp

}
```


