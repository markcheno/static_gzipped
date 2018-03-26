# static middleware

[![Build Status](https://travis-ci.org/glebtv/static_gzipped.svg)](https://travis-ci.org/glebtv/static_gzipped)
[![codecov](https://codecov.io/gh/glebtv/static_gzipped/branch/master/graph/badge.svg)](https://codecov.io/gh/glebtv/static_gzipped)
[![Go Report Card](https://goreportcard.com/badge/github.com/glebtv/static_gzipped)](https://goreportcard.com/report/github.com/glebtv/static_gzipped)
[![GoDoc](https://godoc.org/github.com/glebtv/static_gzipped?status.svg)](https://godoc.org/github.com/glebtv/static_gzipped)

Static-Gzipped middleware for [gin](https://github.com/gin-gonic/gin)

Automatically serves pre-gzipped files with [gzipped.FileServer](https://github.com/lpar/gzipped)

Like gzip_static from nginx, but for gin / go.

### WARNING

This is incompatible with [gzip middleware](https://github.com/gin-contrib/gzip) because it will double-compress already gzipped files.
Can be used with groups: https://github.com/gin-gonic/gin/issues/1125

## Usage

### Start using it

Download and install it:

```sh
$ go get github.com/glebtv/static_gzipped
```

Import it in your code:

```go
import "github.com/glebtv/static_gzipped"
```

### Canonical example:

See the [example](example)

[embedmd]:# (example/simple/example.go go)
```go
package main

import (
  "github.com/glebtv/static_gzipped"
	"github.com/gin-gonic/gin"
)

func main() {
	r := gin.Default()

	// if Allow DirectoryIndex
	//r.Use(static_gzipped.Serve("/", static_gzipped.LocalFile("/tmp", true)))
	// set prefix
	//r.Use(static_gzipped.Serve("/static", static_gzipped.LocalFile("/tmp", true)))

	r.Use(static_gzipped.Serve("/", static_gzipped.LocalFile("/tmp", false)))
	r.GET("/ping", func(c *gin.Context) {
		c.String(200, "test")
	})
	// Listen and Server in 0.0.0.0:8080
	r.Run(":8080")
}
```
