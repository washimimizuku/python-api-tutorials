# grpc-microservices

A tutorial to learn and experiment with gRPC: https://realpython.com/python-microservices-grpc/

## Generate python code from protobufs

Inside folder gprc-microservices, run:

$ python -m grpc_tools.protoc -I protobufs --python_out=recommendations --grpc_python_out=recommendations protobufs/recommendations.proto
