# Demonstrate Logstash as a RabbitMQ Consumer

# Tools and Libraries
## Required
* [Docker (latest)](https://www.docker.com/)
* Any Text Editor

# Building the solution
docker-compose build

# Running the solution

## Starting the containers
docker-compose up

## Starting the containers and detaching
docker-compose up -d

## Attaching to a container
docker attach {container-name}

# Testing
## EventStore
### Browse to
http://localhost:2113

### Login 
admin/changeit

Using postman POST a message to 

### Address
POST http://localhost:2113/streams/test

### Headers
Content-Type : application/json
ES-EventType : Test.Created

### Body
{"a":"1"}

## Rabbit MQ
### Browse to 
http://localhost:15672

### Login 
guest/guest

Go to the exchanges tab, click on test and the post a message to the exchange with a routing key of Test.Created and a Payload of {"a":"1"}

# Issues
Currently Logstash http output plugin is not working to POST events to EventStore.  Watching the logstash logs you will see a Failure due to a status 307.  Redirects are supposed to be followed but it fails to work.  Same POST from postman works without issue.