# REST Api best practices
Read this:
https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/

## Accept and Respond with JSON

Make sure the REST API responds with JSON (set `Content-Type` response header to `application/json`) 
The exception is when  we are sending and receiving files 

## Use nounds instead of verbs for endpoints paths

HTTP request already have verbs:
- GET retrieves resources. 
- POST submits new data to the server. 
- PUT updates existing data. 
- DELETE removes data. 

Examples:
GET `/articles` to get news articles
POST `/articles` to add a new article


