# Chaincode Development Environment
The following is a list of dependencies and recommended tools to develop chaincode.

## Go

- [Go download page](https://golang.org/dl)
- [Go installation instructions](https://golang.org/doc/install)
- [Go documentation and tutorials](https://golang.org/doc/)

Currently, Go is the only supported language for writing chaincode. The Go installation installs a set of Go CLI tools which are very useful when writing chaincode. For example, the `go build` command allows you to check that your chaincode actually compiles before you attempt to deploy it to a network.

### Instructions

Follow the installation instructions linked above. You can verify that Go is installed properly by running the following commands. Of course, the output of `go version` may change depending on your operating system.

```
$ go version
go version go1.7.5 windows/amd64

$ echo $GOPATH
C:\gopath
```

The `GOPATH` does not need to match the one above. It only matters that you have this variable set to a valid directory on your filesystem. The installation instructions linked above will take you through the setup of this environment variable. Why is this variable important? When you run `go build` to test that your chaincode compiles, Go is going to look in the `$GOPATH/src` directory for the non-standard dependencies that you list in the `import` block of your chaincode.

## Hyperledger fabric

- [v0.5-developer-preview Hyperledger fabric](https://github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview)
- [v0.6-preview Hyperledger fabric](https://gerrit.hyperledger.org/r/gitweb?p=fabric.git;a=shortlog;h=refs/heads/v0.6)
- [master branch of the Hyperledger fabric](https://gerrit.hyperledger.org/r/gitweb?p=fabric.git;a=summary)

Any piece of chaincode that you write will need to import the chaincode shim from Hyperledger fabric in order to be able to read and write data to/from the ledger. In order to compile chaincode locally, which you will be doing a lot, you will need to have the fabric code present in your `GOPATH`.

### Instructions

Three different releases of the fabric are linked above. The release you choose needs to match the Hyperledger network you are deploying your chaincode onto. You will need to make sure that the fabric release you choose is stored under `$GOPATH/src/hyperledger/fabric`.

The instructions below should take you through the process of properly installing the v0.5 release on your `GOPATH`.

```

# Create the parent directories on your GOPATH
mkdir -p $GOPATH/src/github.com/hyperledger
cd $GOPATH/src/github.com/hyperledger

# Clone the appropriate release codebase into $GOPATH/src/github.com/hyperledger/fabric
# Note that the v0.5 release is a branch of the repository.  It is defined below after the -b argument
git clone -b v0.5-developer-preview https://github.com/hyperledger-archives/fabric.git
```

If you are installing the v0.6 release, use this for your `git clone` command:

```
# The v0.6 release exists as a branch inside the Gerrit fabric repository
git clone -b v0.6 http://gerrit.hyperledger.org/r/fabric
```

If the fabric is not installed properly on your `GOPATH`, you will see errors like the one below when building your chaincode:
```
$ go build .
chaincode_example02.go:27:2: cannot find package "github.com/hyperledger/fabric/core/chaincode/shim" in any of:
        C:\Go\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOROOT)
        C:\gopath\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOPATH)
```


## Node.js

- [Download links](https://nodejs.org/en/download/)

Node.js is NOT necessary to develop chaincode, but most of our demos are built on Node.js, so it might be handy to go ahead and install it now. Also, you'll need it when you start using the fabric SDK.

### Instructions

Download the latest Node.js LTS installation package and make sure the following commands work on your machine:

```
$ node -v
v6.10.1

$ npm -v
3.10.10
```
