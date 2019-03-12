How to run golang helloworld sample code
-----------------------------------------

* Preparation
```
# double check go version to make sure it have to at least 1.6
$ go version

# install grpc
$ go get -u google.golang.org/grpc

# install Protocol Buffers v3
$ go get -u github.com/golang/protobuf/protoc-gen-go

# make it `protoc-gen-go` compiler plug-in must be in $PATH
$ export PATH=$PATH:$GOPATH/bin
```

* Build ( If it builded already such as this repo, then we can skip build )
```
$ cd helloworld
$ protoc -I helloworld/ protos/helloworld.proto --go_out=plugins=grpc:helloword
```

* Run helloworld golang server 
```
$ go run greeter_server/main.go
2019/03/12 12:31:22 Received: golang client request
```

* Run helloworld golang client 
```
$ go run greeter_client/main.go
2019/03/12 12:31:22 Greeting: Hello golang client request
```

How to run python helloworld sample code
-----------------------------------------

* Preparation
```
# make sure yo have pip version 9.0.1 or higher.
$ python -m pip install --upgrade pip

# install grpc
$ python -m pip install grpcio
or
$ sudo python -m pip install grpcio

# install grpc tools
$ python -m pip install grpcio-tools
or
$ sudo python -m pip install grpcio-tools
```

* Build ( If it builded already such as this repo, then we can skip build )
```
$ cd helloworld/python
$ python -m grpc_tools.protoc -I../protos --python_out=. --grpc_python_out=. ../protos/helloworld.proto

# you will have two python files which is generated automatically by grpc_tools.protoc
-rw-r--r--  1 jwang  staff   3.8K Mar 12 13:15 helloworld_pb2.py
-rw-r--r--  1 jwang  staff   1.3K Mar 12 13:15 helloworld_pb2_grpc.py

# when you run server or client code it will genereate pyc automatically
-rw-r--r--   1 jwang  staff   3.8K Mar 12 13:15 helloworld_pb2.py
-rw-r--r--   1 jwang  staff   1.3K Mar 12 13:15 helloworld_pb2_grpc.py
-rw-r--r--   1 jwang  staff   3.4K Mar 12 13:16 helloworld_pb2.pyc
-rw-r--r--   1 jwang  staff   2.4K Mar 12 13:16 helloworld_pb2_grpc.pyc
```

* Run helloworld python server 
```
$ python greeter_server.py
2019-03-12 13:02:55 python client request
2019-03-12 13:03:02 golang client request
2019-03-12 13:03:09 node.js client request
```

* Run helloworld python client 
```
$ python greeter_client.py
Greeter client received: Hello, python client request!
```

How to run node.js helloworld sample code
-----------------------------------------

* Preparation
```
# make sure you upgrade brew
$ brew update

# Install npm - https://www.npmjs.com/get-npm
$ brew install node
or 
$ brew upgrade node

# double check
$ node -v
and 
$ npm -v
```

* Build
```
# Before your start you node.js need to install (build) first
$ cd helloword/node/dynamic_codegen
$ npm install
npm WARN grpc-examples@0.1.0 No repository field.
npm WARN grpc-examples@0.1.0 No license field.

audited 155 packages in 1.275s
found 0 vulnerabilities
```
 
* Run helloworld node.js server 
```
$ node greeter_server.js
(node:91646) DeprecationWarning: grpc.load: Use the @grpc/proto-loader module with grpc.loadPackageDefinition instead
2019-03-12 21:46:40 node.js client request
2019-03-12 21:46:47 python client request
2019-03-12 21:46:58 golang client request
```

* Run helloworld node.js client 
```
$ node greeter_client.js 
(node:84962) DeprecationWarning: grpc.load: Use the @grpc/proto-loader module with grpc.loadPackageDefinition instead
Greeting: Hello node.js client request
```