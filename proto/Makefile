
build: get gen
	protoc -I . --grpc_out=. --plugin=protoc-gen-grpc=`which grpc_cpp_plugin` helloworld.proto
    protoc -I . --cpp_out=. helloworld.proto

hello:
	echo "Hello"
