# ApiLibrary

Hi, my name is Chrystal Mhaye G. Rimando and this is my API Library.

This is a RESTful API which is used for managing library system. The API allows users to register, log in, and manage authors, and books.

When a user registers, their password is securely stored in the database using hashing. Once registered, a user can log in to get an access token, which is required for making requests to protected routes. Tokens have a short expiration time and are marked as "used" once a request is completed. The system also deletes expired tokens automatically.

Protected routes include actions like adding, updating, or deleting authors and books. For each of these operations, the user must provide a valid token. Once the operation is completed, the token is invalidated, and a new token is issued and returned with the response. This ensures that tokens are only used once, providing better security.

Here are the endpoints, payloads and their functionalities:

User Management
Register a User

Endpoint: POST /user/register
Payload:
json
Copy code
{
  "username": "string",
  "password": "string"
}
Description: Registers a new user with a username and password.

Authenticate User

Endpoint: POST /user/auth
Payload:
json
Copy code
{
  "username": "string",
  "password": "string"
}
Description: Logs in a user and returns an access token upon successful authentication.

Authors Management
Create an Author

Endpoint: POST /authors
Payload:
json
Copy code
{
  "token": "string",
  "name": "string",
  "bio": "string"
}
Description: Adds a new author to the database.

Get All Authors

Endpoint: GET /authors/get
Payload:
json
Copy code
{
  "token": "string"
}
Description: Fetches a list of all authors.

Update Author

Endpoint: PUT /authors/update/{id}
Payload:
json
Copy code
{
  "token": "string",
  "name": "string",
  "bio": "string"
}
Description: Updates the details of a specific author by ID.

Delete Author

Endpoint: DELETE /authors/delete/{id}
Payload:
json
Copy code
{
  "token": "string"
}
Description: Deletes an author by their ID.

Books Management
Create a Book

Endpoint: POST /books
Payload:
json
Copy code
{
  "token": "string",
  "title": "string",
  "description": "string",
  "author_id": "integer"
}
Description: Adds a new book to the database, linked to an author.

Get All Books

Endpoint: GET /books/get
Payload:
json
Copy code
{
  "token": "string"
}
Description: Retrieves a list of all books.

Update Book

Endpoint: PUT /books/update/{id}
Payload:
json
Copy code
{
  "token": "string",
  "title": "string",
  "description": "string"
}
Description: Updates a specific book's details by ID.

Delete Book

Endpoint: DELETE /books/delete/{id}
Payload:
json
Copy code
{
  "token": "string"
}
Description: Deletes a book by its ID.

Get Books by Author

Endpoint: POST /books/get_by_author
Payload:
json
Copy code
{
  "token": "string",
  "author_id": "integer"
}
Description: Fetches all books written by a specific author.

Book-Author Relationships
Create a Relationship

Endpoint: POST /books_authors
Payload:
json
Copy code
{
  "token": "string",
  "book_id": "integer",
  "author_id": "integer"
}
Description: Links a book to an author.

Get All Relationships

Endpoint: GET /books_authors/get
Payload:
json
Copy code
{
  "token": "string"
}
Description: Retrieves all book-author relationships.

Delete Relationship

Endpoint: DELETE /books_authors/delete/{id}
Payload:
json
Copy code
{
  "token": "string"
}
Description: Removes a specific book-author relationship by ID.

Authentication for protected routes is done by passing the token in the request body. Tokens are validated and checked for expiry and prior usage. If valid, the request is processed, and the old token is marked as used. A new token is returned in the response for subsequent requests.
