# grpc-microservices

A tutorial to learn and experiment with gRPC: https://realpython.com/python-microservices-grpc/

## Install

$ pipenv shell
$ pipenv install

## Generate recommendations python code from protobufs in recommendations

$ cd recommendations
$ python -m grpc_tools.protoc -I ../protobufs --python_out=. --grpc_python_out=. ../protobufs/recommendations.proto
## Generate recommendations python code from protobufs in marketplace

$ cd marketplace
$ python -m grpc_tools.protoc -I ../protobufs --python_out=. --grpc_python_out=. ../protobufs/recommendations.proto

## Run grpc recommendations server

$ cd recommendations
$ python recommendations.py

## Test grpc client

>>> import grpc
>>> from recommendations_pb2_grpc import RecommendationsStub
>>> channel = grpc.insecure_channel("localhost:50051")
>>> client = RecommendationsStub(channel)
>>> request = RecommendationRequest(
...    user_id=1, category=BookCategory.SCIENCE_FICTION, max_results=3)
>>> client.Recommend(request)

## Run marketplace

$ cd marketplace
$ FLASK_APP=marketplace.py flask run

## Build and run Docker images

### recommendations

$ docker build . -f recommendations/Dockerfile -t recommendations
$ docker network create microservices
$ docker run -p 127.0.0.1:50051:50051/tcp --network microservices --name recommendations recommendations

### marketplace

$ docker build . -f marketplace/Dockerfile -t marketplace
$ docker run -p 127.0.0.1:5000:5000/tcp --network microservices -e RECOMMENDATIONS_HOST=recommendations marketplace

## Better yet, with docker composer

$ docker-compose up
