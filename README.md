This is a project i completed as a part of the LetsGetRusty Bootcamp.  It makes use of docker images, postgres, and variouse pre existing rust crates.  
The goal was to create a functional API for a question forum like StackOverflow using the Rust programming language.  its capabilities include: 

Creating, Reading, Updating, and Deleting(CRUD) records stored in a Postgres database running on a Docker image.  


Instructions to start up postgres database. 
  1. [Install Docker](https://www.docker.com/)
  2. Install the [Postgres image](https://hub.docker.com/_/postgres) by running `docker pull postgres` in your terminal
  3. Start a Postgres instance by running:
    docker run --name stack-overflow-db -e POSTGRES_PASSWORD=postgrespw -p 55008:5432 -d postgres

Instructions to initialize the database.
  1. Run command: cargo install sqlx-cli
  2. Run command: sqlx migrate run (This will apply changes defined in the "migrations" file to the database)

this program was tested using curl requests to the API listening on port 8000. 
Here are some examples in linux and windows format

Windows: 

Create Question
Copy code:
curl --location "http://localhost:8000/question" ^
--header "Content-Type: application/json" ^
--data "{\"title\": \"Newly Created Question\", \"description\": \"My Description\"}"

Get Questions
Copy code:
curl --location "http://localhost:8000/questions"

Delete Question
Copy code:
curl --location --request DELETE "http://localhost:8000/question" ^
--header "Content-Type: application/json" ^
--data "{ \"question_uuid\": \"[UUID of a created question]\" }"

Create Answer
Copy code:
curl --location "http://localhost:8000/answer" ^
--header "Content-Type: application/json" ^
--data "{ \"question_uuid\": \"fe7331e9-4726-4559-ba2c-f472f490f525\", \"content\": \"test question\" }"

Get Answers
Copy code:
curl --location --request GET "http://localhost:8000/answers" ^
--header "Content-Type: application/json" ^
--data "{ \"question_uuid\": \"fe7331e9-4726-4559-ba2c-f472f490f525\" }"

Delete Answer
Copy code:
curl --location --request DELETE "http://localhost:8000/answer" ^
--header "Content-Type: application/json" ^
--data "{ \"answer_uuid\": \"708b02d7-ccef-4b7a-8fcd-e0b7481a38b9\" }"



Linux: 

Create question
Copy code:
curl --location 'localhost:8000/question' \
--header 'Content-Type: application/json' \
--data '{
    "title": "Newly Created Question",
    "description": "My Description"
}'

Get questions
Copy code:
curl --location 'localhost:8000/questions'

Delete question
Copy code:
curl --location --request DELETE 'localhost:8000/question' \
--header 'Content-Type: application/json' \
--data '{ 
    "question_uuid": "[UUID of a created question]"
}'

Create answer
Copy code:
curl --location 'localhost:8000/answer' \
--header 'Content-Type: application/json' \
--data '{ 
    "question_uuid": "[UUID of a created question]",
    "content": "test question"
}'

Get answers
Copy code:
curl --location --request GET 'localhost:8000/answers' \
--header 'Content-Type: application/json' \
--data '{
    "question_uuid": "[UUID of a created question]"
}'

Delete answer
Copy code:
curl --location --request DELETE 'localhost:8000/answer' \
--header 'Content-Type: application/json' \
--data '{ 
    "answer_uuid": "[UUID of a created answer]"
}'
