# FastAPI User Management API

This is a simple User Management API built using FastAPI and SQLAlchemy. It provides basic CRUD operations for User objects, including creating, updating, deleting, and retrieving user details.

## Dependencies

- FastAPI
- SQLAlchemy
- Pydantic
- jose
- passlib
- typing
- HTTPException

## User Model

User model has the following attributes:

- `id`: integer, primary key
- `email`: string, unique
- `hashed_password`: string
- `name`: string
- `idade`: integer

## Endpoints

1. `POST /users/`: Create a new user
2. `PUT /users/{user_id}`: Update a user
3. `DELETE /users/{user_id}`: Delete a user
4. `GET /users/{user_id}`: Get details of a user

## Parameters

- `user`: A UserIn model instance containing `email`, `password`, `name`, `idade`.
- `user_id`: An integer representing the User ID.
- `db`: An instance of SQLAlchemy Session.
- `token`: A string representing the bearer token for authentication.

## Examples of Use

### Create a new user 
**Request:** 
```bash 
curl -X POST "http://localhost:8000/users/" -H "accept: application/json" -H "Content-Type: application/json" -d "{\"email\":\"johndoe@example.com\",\"password\":\"password123\",\"name\":\"John Doe\",\"idade\":30}"
```
**Response:**
```json
{
  "email": "johndoe@example.com",
  "name": "John Doe",
  "idade": 30
}
```

### Update a user
**Request:** 
```bash 
curl -X PUT "http://localhost:8000/users/1" -H "accept: application/json" -H "Content-Type: application/json" -d "{\"email\":\"johndoe@example.com\",\"password\":\"password123\",\"name\":\"John Doe\",\"idade\":31}"
```
**Response:**
```json
{
  "email": "johndoe@example.com",
  "name": "John Doe",
  "idade": 31
}
```

## Important Notes

- Ensure that the SECRET_KEY and the ALGORITHM for JWT Authentication are kept secret and safe.
- Passwords are hashed using the bcrypt hashing algorithm.
- Email is unique for every user.
- Duplicate email would cause HTTP 400 error.
- Non-existent user_id would cause HTTP 404 error.
- The database connection string needs to be updated according to your database settings. Currently, it is set to 'mysql+pymysql://user:password@localhost/dbname'.
- The ACCESS_TOKEN_EXPIRE_MINUTES is currently set to 30 minutes. You can change this according to your requirements.
