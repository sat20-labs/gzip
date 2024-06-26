# GZIP gin's middleware

[![Run Tests](https://github.com/sat20-labs/gzip/actions/workflows/go.yml/badge.svg)](https://github.com/sat20-labs/gzip/actions/workflows/go.yml)
[![codecov](https://codecov.io/gh/gin-contrib/gzip/branch/master/graph/badge.svg)](https://codecov.io/gh/gin-contrib/gzip)
[![Go Report Card](https://goreportcard.com/badge/github.com/sat20-labs/gzip)](https://goreportcard.com/report/github.com/sat20-labs/gzip)
[![GoDoc](https://godoc.org/github.com/sat20-labs/gzip?status.svg)](https://godoc.org/github.com/sat20-labs/gzip)
[![Join the chat at https://gitter.im/gin-gonic/gin](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/gin-gonic/gin)

Gin middleware to enable `GZIP` support.

## Usage

Download and install it:

```sh
go get github.com/sat20-labs/gzip
```

Import it in your code:

```go
import "github.com/sat20-labs/gzip"
```

Canonical example:

```go
package main

import (
  "fmt"
  "net/http"
  "time"

  "github.com/sat20-labs/gzip"
  "github.com/gin-gonic/gin"
)

func main() {
  r := gin.Default()
  r.Use(gzip.Gzip(gzip.DefaultCompression))
  r.GET("/ping", func(c *gin.Context) {
    c.String(http.StatusOK, "pong "+fmt.Sprint(time.Now().Unix()))
  })

  // Listen and Server in 0.0.0.0:8080
  if err := r.Run(":8080"); err != nil {
    log.Fatal(err)
  }
}
```

Customized Excluded Extensions

```go
package main

import (
  "fmt"
  "net/http"
  "time"

  "github.com/sat20-labs/gzip"
  "github.com/gin-gonic/gin"
)

func main() {
  r := gin.Default()
  r.Use(gzip.Gzip(gzip.DefaultCompression, gzip.WithExcludedExtensions([]string{".pdf", ".mp4"})))
  r.GET("/ping", func(c *gin.Context) {
    c.String(http.StatusOK, "pong "+fmt.Sprint(time.Now().Unix()))
  })

  // Listen and Server in 0.0.0.0:8080
  if err := r.Run(":8080"); err != nil {
    log.Fatal(err)
  }
}
```

Customized Excluded Paths

```go
package main

import (
  "fmt"
  "net/http"
  "time"

  "github.com/sat20-labs/gzip"
  "github.com/gin-gonic/gin"
)

func main() {
  r := gin.Default()
  r.Use(gzip.Gzip(gzip.DefaultCompression, gzip.WithExcludedPaths([]string{"/api/"})))
  r.GET("/ping", func(c *gin.Context) {
    c.String(http.StatusOK, "pong "+fmt.Sprint(time.Now().Unix()))
  })

  // Listen and Server in 0.0.0.0:8080
  if err := r.Run(":8080"); err != nil {
    log.Fatal(err)
  }
}
```

Customized Excluded Paths

```go
package main

import (
  "fmt"
  "net/http"
  "time"

  "github.com/sat20-labs/gzip"
  "github.com/gin-gonic/gin"
)

func main() {
  r := gin.Default()
  r.Use(gzip.Gzip(gzip.DefaultCompression, gzip.WithExcludedPathsRegexs([]string{".*"})))
  r.GET("/ping", func(c *gin.Context) {
    c.String(http.StatusOK, "pong "+fmt.Sprint(time.Now().Unix()))
  })

  // Listen and Server in 0.0.0.0:8080
  if err := r.Run(":8080"); err != nil {
    log.Fatal(err)
  }
}
```
