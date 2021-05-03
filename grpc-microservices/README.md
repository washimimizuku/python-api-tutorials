# grpc-microservices

A tutorial to learn and experiment with gRPC: https://realpython.com/python-microservices-grpc/

## Generate recommendations python code from protobufs

Inside folder gprc-microservices, run:

$ python -m grpc_tools.protoc -I protobufs --python_out=recommendations --grpc_python_out=recommendations protobufs/recommendations.proto

## Run grpc recommendations server

$ python recommendations/recommendations.py

## Test grpc client

>>> import grpc
>>> from recommendations_pb2_grpc import RecommendationsStub
>>> channel = grpc.insecure_channel("localhost:50051")
>>> client = RecommendationsStub(channel)
>>> request = RecommendationRequest(
...    user_id=1, category=BookCategory.SCIENCE_FICTION, max_results=3)
>>> client.Recommend(request)
