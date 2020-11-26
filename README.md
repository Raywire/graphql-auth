# *GraphQL Authentication built with ApolloServer and SequelizeORM*

## **Mutation for registering a user**
```
mutation {
  registerUser(username: "johndoe", email: "johndoe@gmail.com", password: "wizzyekpot" ){
    token
  }
}
```

We should get something like this:

```json
{
  "data": {
    "registerUser": {
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiZW1haWwiOiJzaW1peXV3aXJlQGdtYWlsLmNvbSIsImlhdCI6MTYwNjM3NjkzMSwiZXhwIjoxNjA2NDYzMzMxfQ.mJyxkUlDevOaS2Wy-GKlZrQPOVjOnippPwtXTDTfToI"
    }
  }
}
```

## **Mutation for login**

Let’s now log in with the user details we just created:
```
mutation {
  login(email:"johndoe@gmail.com" password:"123456"){
    token
  }
}
```

We should get something like this:
```json
{
  "data": {
    "login": {
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiZW1haWwiOiJzaW1peXV3aXJlQGdtYWlsLmNvbSIsImlhdCI6MTYwNjM3NjkzMSwiZXhwIjoxNjA2NDYzMzMxfQ.mJyxkUlDevOaS2Wy-GKlZrQPOVjOnippPwtXTDTfToI"
    }
  }
}
```
## **Query for a single user**

For us to query a single user, we need to pass the user token as authorization header. Go to the HTTP Headers tab.
…and paste this:
```json
{
  "Authorization": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiZW1haWwiOiJzaW1peXV3aXJlQGdtYWlsLmNvbSIsImlhdCI6MTYwNjM3NjkzMSwiZXhwIjoxNjA2NDYzMzMxfQ.mJyxkUlDevOaS2Wy-GKlZrQPOVjOnippPwtXTDTfToI"
}
```

Here’s the query:
```
query myself{
  me {
    id
    email
    username
  }
}
```
And we should get something like this:
```json
{
  "data": {
    "me": {
      "id": 1,
      "email": "johndoe@gmail.com",
      "username": "johndoe"
    }
  }
}
```
## **Get a user by ID**
```
query singleUser{
  user(id:1){
    id
    email
    username
  }
}
```
## **The query to get all users**
```
{
  allUsers{
    id
    username
    email
  }
}
```