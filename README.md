# Applause Assignment - Tester Matching
My solution to the task is a REST API developed using Django framework. 

## API schema

## Data model



## Technology

### REST API:
- Python 3
- Django 
- Django REST framework
- drf-yasg - Yet another Swagger generator
### Database:
- PostgreSQL
### Other tools:
- Docker
- Docker Compose

## Using the API
## Importing the data
Data can be imported using custom django-admin command called `populate_db`. 

You can run it the same way you would run any other django-admin command.
```shell
python manage.py populate_db
```
Script requires the database tables to be empty to avoid collisions and to avoid populating database twice by mistake.  If tables are not empty script throughs an error.
## Running the app
App requires PostgreSQL database to work. Because of that the easiest way to run it locally is to use Docker Compose. 

First open terminal in the TeststerMatch directory. 

To start the app in a development mode run this command:
```shell
docker-compose up
```
After docker containers are up. You need to run this two commands in other terminal in the same directory to setup database. You need to do only one time after you create the containers.
```shell
docker-compose exec web python manage.py migrate
```
```shell
docker-compose exec web python manage.py populate_db
```
### Windows only (probably)
Temporarly I have only access to Windows machine. However, after checking online it seems that this is Windows exclusive issue.

There's an issue running volume for the postgres container 'the normal way' on Windows. To overcome it you need to create volume and use it instead of the host volume.
```shell
docker volume create --name tester-postgresql -d local
``` 
You also need modify `docker-compose.yml`. I left comments about this inside the file. 

### Running tests
After starting Docker Compose and making migration. You can tests inside Docker container using command bellow.
```shell
docker-compose exec web python manage.py test
```