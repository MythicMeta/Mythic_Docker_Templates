# mythic_base_go

This is the base image for the mythic_* series of images. This image is based on golang:1.20-buster.
This also includes:
* make
* protobuf-compiler
* garble
* google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest
* google.golang.org/protobuf/cmd/protoc-gen-go@latest

# mythic_base_python

This is the base image for the mythic_* series of images. This image is based on python:3.11-buster.
This package also includes:
* make
* protobuf-compiler
* PyPi packages in requirements.txt
* pip3

# mythic_{go|python}_dotnet

This image builds on `mythic_{go|python}_base` by adding the dotnet-sdk-7.0, mono-complete, and nuget.
As a convenience, this image also bundles in the System.Management.Automation.dll.
This also includes:
* gcc-mingw-w64

# mythic_{go|python}_macos

This image builds on `mythic_{go|python}_base` by adding the macOS SDK 12.1 with osxcross. 
This also includes:
* clang-15
* clang++-15
* cmake
* llvm
* gcc-mingw-w64