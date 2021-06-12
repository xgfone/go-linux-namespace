# Linux Namespace [![Build Status](https://api.travis-ci.com/xgfone/go-namespace.svg?branch=master)](https://travis-ci.com/github/xgfone/go-namespace) [![GoDoc](https://pkg.go.dev/badge/github.com/xgfone/go-namespace)](https://pkg.go.dev/github.com/xgfone/go-namespace) [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=flat-square)](https://raw.githubusercontent.com/xgfone/go-namespace/master/LICENSE)

The operation about linux namespace. Support `Go1.7+`.

## Installation
```shell
$ go get -u github.com/xgfone/go-namespace
```

## Example
```go
package main

import (
    "fmt"

    "github.com/xgfone/go-namespace"
)

func main() {
    ns := NewNameSpace("name")

    // Ensure that the namespace exists.
    if exist, err := ns.IsExist(); err != nil {
        fmt.Println(err)
        return
    } else if !exist {
        if err := ns.Create(); err != nil {
            fmt.Println(err)
            return
        }
    }

    // Execute the command in the namespace.
    if output, err := ns.Exec("ip", "a"); err != nil {
        fmt.Println(err)
    } else {
        fmt.Println(output)
    }

    // Delete the namespace.
    if err := ns.Delete(); err != nil {
        fmt.Println(err)
        return
    }
}
```
