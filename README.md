# Exercise. MongoDB. Basics

[https://classroom.google.com/u/0/c/NDgwNDYwMTI2OTAz/a/MzYyOTEzMDcwMTE0/details](https://classroom.google.com/u/0/c/NDgwNDYwMTI2OTAz/a/MzYyOTEzMDcwMTE0/details)

```js
// 1. Create DB with collections ///////////////////////////////////////////////
use socialDB
db.createCollection('users')
db.createCollection('posts')

// 2. Queries //////////////////////////////////////////////////////////////////
// 2.1. Insert
// - 15 new posts with at least 2 comments
db.posts.insertMany([
    {
        title: "Title 1", body: "Post body 1", username: "user1", comments: [
            { username: "user2", body: "comment body 1.1" },
            { username: "user3", body: "comment body 1.2" }]
    },
    {
        title: "Title 2", body: "Post body 2", username: "user2", comments: [
            { username: "user4", body: "comment body 2.1" },
            { username: "user5", body: "comment body 2.2" }]
    },
    {
        title: "Title 3", body: "Post body 3", username: "user3", comments: [
            { username: "user6", body: "comment body 3.1" },
            { username: "user7", body: "comment body 3.2" }]
    },
    {
        title: "Title 4", body: "Post body 4", username: "user4", comments: [
            { username: "user8", body: "comment body 4.1" },
            { username: "user9", body: "comment body 4.2" },
            { username: "user10", body: "comment body 4.3" }]
    },
    {
        title: "Title 5", body: "Post body 5", username: "user5", comments: [
            { username: "user10", body: "comment body 5.1" },
            { username: "user11", body: "comment body 5.2" },
            { username: "user12", body: "comment body 5.3" },
            { username: "user13", body: "comment body 5.4" }]
    },
    {
        title: "Title 6", body: "Post body 6", username: "user6", comments: [
            { username: "user12", body: "comment body 6.1" },
            { username: "user13", body: "comment body 6.2" }]
    },
    {
        title: "Title 7", body: "Post body 7", username: "user7", comments: [
            { username: "user14", body: "comment body 7.1" },
            { username: "user15", body: "comment body 7.2" }]
    },
    {
        title: "Title 8", body: "Post body 8", username: "user8", comments: [
            { username: "user1", body: "comment body 8.1" },
            { username: "user2", body: "comment body 8.2" }]
    },
    {
        title: "Title 9", body: "Post body 9", username: "user9", comments: [
            { username: "user3", body: "comment body 9.1" },
            { username: "user4", body: "comment body 9.2" }]
    },
    {
        title: "Title 10", body: "Post body 10", username: "user10", comments: [
            { username: "user5", body: "comment body 10.1" },
            { username: "user6", body: "comment body 10.2" }]
    },
    {
        title: "Title 11", body: "Post body 11", username: "user11", comments: [
            { username: "user7", body: "comment body 11.1" },
            { username: "user8", body: "comment body 11.2" },
            { username: "user9", body: "comment body 11.3" },
            { username: "user10", body: "comment body 11.4" }]
    },
    {
        title: "Title 12", body: "Post body 12", username: "user12", comments: [
            { username: "user9", body: "comment body 12.1" },
            { username: "user10", body: "comment body 12.2" }]
    },
    {
        title: "Title 13", body: "Post body 13", username: "user13", comments: [
            { username: "user11", body: "comment body 13.1" },
            { username: "user12", body: "comment body 13.2" }]
    },
    {
        title: "Title 14", body: "Post body 14", username: "user14", comments: [
            { username: "user13", body: "comment body 14.1" },
            { username: "user14", body: "comment body 14.2" }]
    },
    {
        title: "Title 15", body: "Post body 15", username: "user15", comments: [
            { username: "user15", body: "comment body 15.1" },
            { username: "user1", body: "comment body 15.2" }]
    },

])

// - Insert at least 10 users
db.users.insertMany([
    { username: "user1", email: "user1@mail.com", age: 8 },
    { username: "user2", email: "user2@mail.com", age: 9 },
    { username: "user3", email: "user3@mail.com", age: 10 },
    { username: "user4", email: "user4@mail.com", age: 11 },
    { username: "user5", email: "user5@mail.com", age: 12 },
    { username: "user6", email: "user6@mail.com", age: 13 },
    { username: "user7", email: "user7@mail.com", age: 14 },
    { username: "user8", email: "user8@mail.com", age: 15 },
    { username: "user9", email: "user9@mail.com", age: 16 },
    { username: "user10", email: "user10@mail.com", age: 17 },
    { username: "user11", email: "user11@mail.com", age: 18 },
    { username: "user12", email: "user12@mail.com", age: 19 },
    { username: "user13", email: "user13@mail.com", age: 20 },
    { username: "user14", email: "user14@mail.com", age: 21 },
    { username: "user15", email: "user15@mail.com", age: 22 }
])

// 2.2. Update data
// - Update posts
// - - Update all fields of a post
db.posts.updateOne({ title: "Title 7" },
    {
        $set: {
            title: "Title 7 updated",
            body: "Post body 7 updated",
            username: "user5",
            comments: [
                { username: "user3", body: "comment body 7.1 Updated" },
                { username: "user2", body: "comment body 7.2 Updated" }
            ]
        }
    })

// - - Change the body of a post
db.posts.updateOne({ title: "Title 1" },
    { $set: { body: "Post body 1 updated" } })

// - - Update comment: Change the body of a comment
// VERSION 1: Overwrite all array with the single change
db.posts.updateOne({ title: "Title 1" },
    {
        $set: {
            comments: [
                { username: "user2", body: "comment body 1.1 updated" },
                { username: "user3", body: "comment body 1.2" }
            ]
        }
    })
// VERSION 2: Update only the needed field of a specific object inside the array
db.posts.updateOne({title:"Title 1"},
    {$set: {"comments.1.body": "comment body 1.2 UPDATED inside"}})


// - Update users
// - - Update all fields of a user
db.users.updateOne({ username: "user1" },
    { $set: { username: "user1updated", email: "user1updated@mail.com", age: 7 } })

// - - Change email of two users
db.users.updateOne(
    { username: "user2" },
    { $set: { email: "user2updated@mail.com" } }
)
db.users.updateOne(
    { username: "user3" },
    { $set: { email: "user3updated@mail.com" } }
)

// - - Increase on 5 years the age of a user
db.users.updateOne({ username: "user4" }, { $inc: { age: 5 } })


// 2.3. Get data

// - All posts
db.posts.find()

// Posts from username
db.posts.find({ username: "user5" })

// Users with age > 20
db.users.find({ age: { $gt: 20 } })

// Users with age < 23
db.users.find({ age: { $lt: 23 } })

// Users with age between 20 and 30
db.users.find({ age: { $gt: 20, $lt: 30 } })

// Show users sorted by age, ascending and descending
db.users.find().sort({ age: 1 }) // ascending
db.users.find().sort({ age: -1 }) // descending

// Count total users
db.users.count()  // DEPRECATED
db.users.countDocuments()

// Get and print all post titles
db.posts.find().forEach((doc) => {
    print("Post title: " + doc.title)
})

// Get only 2 users
db.users.find().limit(2)

// Search by title 2 posts
db.posts.createIndex({ title: 'text' })  // Create a search index
db.posts.find({ $text: { $search: "Title" } }).limit(2)


// 2.4. Delete
// Delete users older than 20
db.users.deleteMany({ age: { $gt: 20 } })


// 3. Extra ////////////////////////////////////////////////////////////////////
// Get count of posts with more than two posts
db.posts.find({'comments.2':{$exists: true}}).count()

// Get last created post
db.posts.find().sort({_id:-1}).limit(1)

// Get last 5 created posts
db.posts.find().sort({_id:-1}).limit(5)

// Delete all posts with more than two comments
db.posts.deleteMany({ 'comments.2': { $exists: true } })
```