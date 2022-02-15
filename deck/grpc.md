---
marp: true
html: true
paginate: true
header: '![image width:80px](https://go.dev/images/go-logo-blue.svg)'
footer: '![image width:80px](https://go.dev/images/gophers/pilot-bust.svg)'
style: |
    section {
        font-family: Arial, Helvetica, sans-serif;
    }
    section h1 {
        color: #00A29C;
    }
    section h2 {
        color: #00A29C;
    }

    section.cl em {
    font-style: normal;
    font-weight: bold;
    color: #00ADD8
    }
    section.cl strong {
    font-style: normal;
    font-weight: bold;
    color: #CE3263
    }
---

# go

## gRPC

Pallat Anchaleechamaikorn
Go Developer

yod.pallat@gmail.com
https://github.com/pallat

https://go.dev/tour
https://github.com/uber-go/guide

---

## outline

gRPC
protobuf

---

## gRPC

https://developers.google.com/protocol-buffers/docs/gotutorial

---

## protobuf

```protobuf
syntax = "proto3";
package helloworld;

option go_package = "github.com/protocolbuffers/protobuf/examples/go/helloworldpb";

// The greeting service definition.
service Greeter {
// Sends a greeting
    rpc SayHello (HelloRequest) returns (HelloReply) {}
// Sends another greeting
    rpc SayHelloAgain (HelloRequest) returns (HelloReply) {}
}

// The request message containing the user's name.
message HelloRequest {
    string name = 1;
}

// The response message containing the greetings
message HelloReply {
    string message = 1;
}
```

---

## protoc installation

https://grpc.io/docs/protoc-installation/

```sh
$ brew install protobuf
$ protoc --version  # Ensure compiler version is 3+
```

---

## protoc-gen-go

```sh
$ go install google.golang.org/protobuf/cmd/protoc-gen-go@latest

### protoc-gen-go-grpc
$ go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
```

---

## compile proto

```sh
$ protoc -I=$SRC_DIR --go_out=$DST_DIR $SRC_DIR/addressbook.proto

### deprecated
$ protoc -I=. --go_out=plugins=grpc:. ./addressbook.proto

### currently use
$ protoc --go_out=. --go-grpc_out=. ./helloworld.proto
```

---

## example project

https://github.com/pallat/trygrpc

---

## Why load balancing gRPC is tricky?

https://majidfn.com/blog/grpc-load-balancing/?fbclid=IwAR1dJaJD1sz9IklGLFwr1WQUOCxvthNZoOy-_bxuGr3ZRn_wItpZZyFtWL0

---

## client side LB

https://github.com/hakobe/grpc-go-client-side-load-balancing-example

---

## service registry

<!-- deprecated -->
https://golangexample.com/a-grpc-load-balancer-for-go/

### available version

https://github.com/grpc/grpc/blob/master/doc/load-balancing.md

https://github.com/rafaeleyng/rafaeleyng.github.io/tree/dev/examples/grpc-load-balancing

---
