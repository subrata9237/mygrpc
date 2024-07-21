cmake_minimum_required(VERSION 3.10)
project(mygrpc)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -g")

find_package(Protobuf REQUIRED)
find_package(gRPC REQUIRED)
find_package(Threads REQUIRED)

add_executable(server src/server.cpp proto/helloworld.pb.cc proto/helloworld.grpc.pb.cc)
target_link_libraries(server gRPC::grpc++ protobuf::libprotobuf)

add_executable(client src/client.cpp proto/helloworld.pb.cc proto/helloworld.grpc.pb.cc)
target_link_libraries(client gRPC::grpc++ protobuf::libprotobuf)
