# ApiLibrary

Hi, my name is Chrystal Mhaye G. Rimando and this is my API Library.

This is a RESTful API which is used for managing library system. The API allows users to register, log in, and manage authors, and books.

When a user registers, their password is securely stored in the database using hashing. Once registered, a user can log in to get an access token, which is required for making requests to protected routes. Tokens have a short expiration time and are marked as "used" once a request is completed. The system also deletes expired tokens automatically.

Protected routes include actions like adding, updating, or deleting authors and books. For each of these operations, the user must provide a valid token. Once the operation is completed, the token is invalidated, and a new token is issued and returned with the response. This ensures that tokens are only used once, providing better security.

Here are the endpoints and their functionalities:

User Management:
Register a User (POST /user/register): Allows a new user to register by providing a username and password.
Authenticate User (POST /user/auth): Logs in a user and provides an access token if the credentials are correct.

Authors Management:
Create an Author (POST /authors): Adds a new author to the database.
Get All Authors (GET /authors/get): Fetches a list of all authors.
Update Author (PUT /authors/update/{id}): Updates the details of a specific author by ID.
Delete Author (DELETE /authors/delete/{id}): Deletes an author by their ID.

Books Management:
Create a Book (POST /books): Adds a new book to the database, linked to an author.
Get All Books (GET /books/get): Retrieves a list of all books.
Update Book (PUT /books/update/{id}): Updates a specific book's details by ID.
Delete Book (DELETE /books/delete/{id}): Deletes a book by its ID.
Get Books by Author (POST /books/get_by_author): Fetches all books written by a specific author.

Book-Author Relationships:
Create a Relationship (POST /books_authors): Links a book to an author.
Get All Relationships (GET /books_authors/get): Retrieves all book-author relationships.
Delete Relationship (DELETE /books_authors/delete/{id}): Removes a specific book-author relationship by ID.

Authentication for protected routes is done by passing the token in the request body. Tokens are validated and checked for expiry and prior usage. If valid, the request is processed, and the old token is marked as used. A new token is returned in the response for subsequent requests.
