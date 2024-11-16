# API Library

Hi, my name is Chrystal Mhaye G. Rimando and this is my API Library.

This is a RESTful API which is used for managing library system. The API allows users to register, log in, and manage authors, and books.

When a user registers, their password is securely stored in the database using hashing. Once registered, a user can log in to get an access token, which is required for making requests to protected routes. Tokens have a short expiration time and are marked as "used" once a request is completed. The system also deletes expired tokens automatically.

Protected routes include actions like adding, updating, or deleting authors and books. For each of these operations, the user must provide a valid token. Once the operation is completed, the token is invalidated, and a new token is issued and returned with the response. This ensures that tokens are only used once, providing better security.

### Here are the endpoints, payloads and their functionalities:
##### USER REGISTRATION
- Registers a new user by creating an account in the system.
##### URL: POST /user/register
#####  Method: POST

### Payload
```bash
{
  "username": "your_username",
  "password": "your_password"
}
```
### Response
#### SUCCESS
```bash
{
  "status": "success",
  "token": null,
  "data": null
}
```
#### FAILURE
```bash
{
  "status": "fail",
  "token": null,
  "message": "Unauthorized Access"
}
```

##### USER Authentication
- Authenticates a user by verifying their credentials and provides an access token if successful.
#### URL: POST /user/auth
####  Method: POST

### Payload
```bash
{
  "username": "your_username",
  "password": "your_password"
}
```
### Response
#### SUCCESS
```bash
{
  "status": "success",
  "token": "your_token",
  "data": null
}
```
#### FAILURE
```bash
{
  "status": "fail",
  "token": null,
  "message": "Unauthorized Access"
}
```
## AUTHOR MANAGEMENT
- These endpoints allow managing authors within the library system.

#### Create Author
- Adds a new author to the library system.
#### URL: POST /authors
####  Method: POST

### Payload
```bash
{
  "author": "author_name",
  "token": "your_token"
}
```
### Response
```bash
{
  "status": "success",
  "token": "your_newtoken"
}
```
#### Get Authors
- Retrieves a list of all authors in the library system.
#### URL: Get /authors/get
####  Method: GET

### Payload
```bash
{
  "token": "your_token"
}
```
### Response
```bash
{
  "status": "success",
  "data": [
    {
      "authorid": "1",
      "name": "Chrystal"
      "token": "your_newtoken"
    }
  ]
}
```
#### Update Author
- Updates the information of an existing author.
#### URL: PUT /authors/update/{id}
####  Method: PUT

### Payload
```bash
{
  "name": "author_newname",
  "token": "your_token"
}
```
### Response
```bash
{
  "status": "success"
  "token": "your_newtoken"
}
```
#### Delete Author
- Deletes an author from the library system based on their ID.
#### URL: DELETE /authors/delete/{id}
####  Method: DELETE

### Payload
```bash
{
  "token": "your_token"
}

```
### Response
```bash
{
  "status": "success"
  "token": "your_newtoken"
}
```
## BOOK MANAGEMENT
- These endpoints allow managing books within the library system.

#### Add Book
- Adds a new book to the library system.
#### URL: POST /books
####  Method: POST
### Payload
```bash
{
  "title": "book_title",
  "author_id": "1",
  "token": "your_token"
}
```
### Response
```bash
{
  "status": "success"
  "token": "your_newtoken"
}
```
#### Get Books
- Retrieves a list of all books in the library system.
#### URL: GET /books
####  Method: GET
### Payload
```bash
{
  "title": "book_title",
  "author_id": "1",
  "token": "your_token"
}
```
### Response
```bash
{
  "status": "success"
  "token": "your_newtoken"
}
```
#### Update Book
- Updates the information of an existing book.
#### URL: PUT /books/{id}
####  Method: PUT
### Payload
```bash
{
  "title": "new_booktitle",
  "author_id": "1",
  "token": "your_token"
}
}

```
### Response
```bash
{
  "status": "success"
  "token": "your_newtoken"
}
```
#### Delete Book
- Deletes a book from the library system based on its ID.
#### URL: DELETE /books/{id}
####  Method: DELETE
### Payload
```bash
{
  "token": "your_token"
}
```
### Response
```bash
{
  "status": "success"
  "token": "your_newtoken"
}
```

## BOOK AUTHOR RELATIONS
- These endpoints manage the relationships between books and authors in the library.
#### Create Book-Author Relation
- Adds a new relationship between a book and an author.
#### URL: POST /books_authors
####  Method: POST
### Payload
```bash
{
  "book_id": "1",
  "author_id": "2",
  "token": "your_token"
}

```
### Response
```bash
{
  "status": "success"
  "token": "your_newtoken"
}
```
#### Get All Book-Author Relations
- Retrieves a list of all book-author relationships
#### URL: GET /books_authors/get
####  Method: GET
### Payload
```bash
{
  "token": "your_token"
}
```
### Response
```bash
{
  "status": "success",
  "token": "your_newtoken",
  "data": [
    {
      "id": "1",
      "book_id": "1",
      "author_id": "2"
    }
  ]
}
```
#### Delete Book-Author Relation
- Removes a specified book-author relationship by its ID.
#### URL: DELETE /books_authors/delete/{id}
####  Method: DELETE
### Payload
```bash
{
  "token": "your_token"
}
```
### Response
```bash
{
  "status": "success",
  "token": "your_newtoken",
}
```

## AUTHENTICATION
- All secured endpoints require an access_token in the request header. Tokens are provided upon user authentication and must be included in the Authorization header as follows:
  Authorization: Bearer {access_token}

### ERROR HANDLING
If an error occurs, the response will have the following format:
```bash
{
  "status": "fail",
  "token": null,
  "message": "Unauthorized Access"
}
```

Authentication for protected routes is done by passing the token in the request body. Tokens are validated and checked for expiry and prior usage. If valid, the request is processed, and the old token is marked as used. A new token is returned in the response for subsequent requests.
