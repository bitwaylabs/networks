# Bitway Node Installation And Setup

Instruction to install and configure the `bitwayd` binary

## Hardware Specifications

1. Minimum Requirements
   1. CPU: 2 cores
   2. RAM: 4 GB
   3. Storage: 200 GB
   4. Network: 1 Gbps
2. Recommended Specifications
   1. CPU: 4 cores
   2. RAM: 8 GB
   3. Storage: 500 GB
   4. Network: 1 Gbps

## Operating System
The choice of operating system for your node is entirely based on your personal preference. You can compile the `bitwayd` daemon on a wide range of modern Linux distributions and recent versions of macOS.
> The tutorial assumes that you are utilizing an Ubuntu LTS release. If you have opted for a different operating system, you will need to adjust the commands accordingly to align with your chosen OS.

## Prerequisites
Golang v1.22.0+ ([go releases and instructions](https://go.dev/dl/)).

## Build `bitwayd` from source
1. Ensure that you have the necessary version of Golang installed.
```
go version
```
The output must align with the Golang version specified in the Prerequisites section.

2. Clone the source code from the repository and navigate to the cloned directory using the `cd` command.

```
git clone -b dev https://github.com/bitwaylabs/bitway.git
cd bitway
```

 3. Compile the `bitwayd` binary.

```
make install
```
The provided command will compile the `bitwayd` binary and save it in your $GOBIN directory. If $GOBIN is included in your $PATH, you should be able to execute the `bitwayd` binary.

```
bitwayd version
2.0.0
```

If you encounter any issues related to PATH settings, please consult the provided Go releases and instructions link mentioned in the prerequisites section.
