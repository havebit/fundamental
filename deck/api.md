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

## API

Pallat Anchaleechamaikorn
Go Developer

yod.pallat@gmail.com
https://github.com/pallat

https://go.dev/tour
https://github.com/uber-go/guide

---

## outline

net/http
Fiber
Gorm.io
Dependencies Injection
JWT
Middleware
Configurations
Gracefully shutting down
Serve frontend directly

---

## Requirement

Todo List API

> **POST** _/todos_
> **GET** _/todos_
> **DELETE** _/todos/:**id**_

---

## Cross-Functional Requirement

- configuration in .env file
- gracefully shutting down
- liveness probe
- readiness probe
- JWT authenications
- rate limited
- Dockerfile
- error handling

---

## Why do we need to use Go instead of other languages

try this in javascript

```js
parseInt(0.5)
parseInt(0.05)
parseInt(0.005)
parseInt(0.0005)
parseInt(0.00005)
parseInt(0.000005)
parseInt(0.0000005)
parseInt(0.00000005)
```

---

## Tips: floating point for money

and this

```js
0.34 + 0.01
```

---

<!-- _class: cl -->

## init the project

> *mkdir* todoapi *&&* cd todoapi
> *git* init
> *go mod init* **gitlab.com/cjexpress/pallat.anc/todoapi**

---

## gorilla/mux

https://pkg.go.dev/net/http
https://github.com/gorilla/mux

---

## Web Framework Benchmark

https://www.techempower.com/benchmarks/#section=data-r19&hw=ph&test=plaintext
https://github.com/smallnest/go-web-framework-benchmark

---

## Fiber

https://docs.gofiber.io/
https://github.com/gofiber/fiber

---

### Fiber: Example

```go
package main

import "github.com/gofiber/fiber/v2"

func main() {
    app := fiber.New()

    app.Get("/", func(c *fiber.Ctx) error {
        return c.SendString("Hello, World 👋!")
    })

    app.Listen(":3000")
}
```

---

## Fiber.io

$\bigstar$ Some values returned from *fiber.Ctx are not immutable by default

### Issue

https://github.com/gofiber/fiber/issues/426

---

## database/sql

```go
import (
   "database/sql"
   _ "github.com/mattn/go-sqlite3"
)
```

---

## the Blank identifier

### (underscore)

import with need the side effects

**_ "github.com/mattn/go-sqlite3"**

---

<style scope>
section em {
    color: #00ADD8;
}
</style>

## SQL Driver init()

```go
func init() {
    sql.Register("sqlite3", &SQLiteDriver{})
}
```

**&SQLiteDriver** implement *sql.Driver*

```go
type Driver interface {
    Open(name string) (Conn, error)
}
```

---

## database/sql with sqlite

```go
func main() {
   db, err := sql.Open("sqlite3", "test.db")
   if err != nil {
       log.Fatal(err)
   }
   defer db.Close()
   
   // TODO: logic
}
```

---

## Object-Relational Mapping (ORM)

gorm.io
xorm.io
ent (entgo.io)
gorp
etc.

https://github.com/avelino/awesome-go#orm

---

## Gorm.io

```go
import (
    "gorm.io/gorm"
    "gorm.io/driver/postgres"
)

func main() {
    dsn := "host=localhost user=postgres password=mysecretpassword dbname=myapp port=5432"
    db, err := gorm.Open(postgres.Open(dsn), &gorm.Config{})
    if err != nil {
    panic("failed to connect database")
    }

    // TODO: logic
}
```

---

## Gorm Model

```go
type Model struct {
   ID        uint `gorm:"primarykey"`
   CreatedAt time.Time
   UpdatedAt time.Time
   DeletedAt DeletedAt `gorm:"index"`
}
```

---

## Composition Gorm Model, embeded field

```go
type Todo struct {
   gorm.Model
   Title string `json:"text"`
}
```

---

## The Meta information by tagging

```go
type Todo struct {
   gorm.Model
   Title string `json:"text"` // <-- tag
}
```

---

## Todo Package

- Json binding
- Insert into Table
- Return Json error
- Return OK Response

---

## Gin-Gonic

https://github.com/gin-gonic/gin

### recommended by golang.org

Tutorials
https://golang.org/doc/tutorial/

Developing a RESTful API with Go and Gin
https://golang.org/doc/tutorial/web-service-gin

---

## Gin-Gonic Example

```go
package main

import "github.com/gin-gonic/gin"

func main() {
    r := gin.Default()
    r.GET("/ping", func(c *gin.Context) {
        c.JSON(200, gin.H{
            "message": "pong",
        })
    })
    r.Run() // listen and serve on 0.0.0.0:8080 (for windows "localhost:8080")
}
```

---

## Gin Handler

```go
type HandlerFunc func(*Context)
```

usage

```go
func pingPongHandler(c *gin.Context) {
        c.JSON(200, gin.H{
            "message": "pong",
        })
}
```

---

## Gin Context

```go
type Context struct {
    Request *http.Request
    Writer  ResponseWriter

    Params Params

    // Keys is a key/value pair exclusively for the context of each request.
    Keys map[string]interface{}

    // Errors is a list of errors attached to all the handlers/middlewares who used this context.
    Errors errorMsgs

    // Accepted defines a list of manually accepted formats for content negotiation.
    Accepted []string
    // contains filtered or unexported fields
}
```

---

## Let's start with New Todo Handler

```http
POST /todos
Content-Type: application/json

{
    "text": "Daily Sync-up"
}
```

---

## JWT

jwt.io

---

<style scope>
section strong {
    color: #CE3262;
}
</style>

## Standard Claims

"iss" (Issuer)
"sub" (Subject)
"aud" (Audience)
**"exp" (Expiration Time)**
**"nbf" (Not Before)**
**"iat" (Issued At)**
"jti" (JWT ID)

---

## Protect API

**POST** /todos
**Content-Type:** application/json
**Authorization:** *Bearer* eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c

```json
{
    "text": "Daily Sync-up"
}
```

---

## Middleware

![image w:600px align:center](https://i.imgur.com/RTwlI4F.png)

---

## Gin Middleware chain

```go
c.Next()
```

beak the chain by Abort

```go
c.AbortWithStatus(http.StatusUnauthorized)
```

---

## JWT Middleare

![image](https://www.vaadata.com/blog/wp-content/uploads/2016/12/JWT_tokens_EN.png)

---

## Login

**POST** /login
**Content-Type:** application/json

```json
{
    "account": "pallat",
    "password": "drowssap"
}
```

---

## Swagger

https://github.com/swaggo/gin-swagger

---

## Gracefully shutting down

![bg h:400px right](https://marcofranssen.nl/_next/image?url=%2Fimages%2F933faf01ec92c3ab47275d096d3e8c0f2e0d87e5.png&w=3840&q=75)

---

## ListenAndServe

![image h:500px](listen_serve.png)

---

## The Kubernetes termination lifecycle

https://cloud.google.com/blog/products/containers-kubernetes/kubernetes-best-practices-terminating-with-grace

`
In practice, this means your application needs to handle the SIGTERM message and begin shutting down when it receives it. This means saving all data that needs to be saved, closing down network connections, finishing any work that is left, and other similar tasks.
`

---

## graceful example

```go
    ctx, stop := signal.NotifyContext(context.Background(), os.Interrupt)
    defer stop()

    go func() {
        if err := server.ListenAndServe(); err != nil && err != http.ErrServerClosed {
            log.Fatalf(“listen: %s\n”, err)
        }
    }()

    <-ctx.Done()
    stop()
    fmt.Println("shutting down gracefully, press Ctrl+C again to force")

    timeoutCtx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
    defer cancel()

    if err := server.Shutdown(timeoutCtx); err != nil {
        fmt.Println(err)
    }
```

---

## test shutdown

```zsh
sudo lsof -i :8080
kill -15 [PID] || kill -SIGINT [PID]
kill -SIGTERM [PID]
```

---

## Configurations

https://12factor.net/

---

## Viper

https://github.com/spf13/viper

---

## .env auto loading

https://github.com/joho/godotenv

---

## Our Config

.env

```ini
ADDR=":8081"
SIGNATURE="drowssap"
```

---

## Add external to the binary

```sh
go build -ldflags “-X main.somevar=training” -o app
```

---

## Add git commit number to the binary

```sh
go build \
  -ldflags "-X main.buildcommit=`git rev-parse --short HEAD` \
  -X main.buildtime=`date "+%Y-%m-%dT%H:%M:%S%Z:00"`" \
  -o app
```

---

## Pod Health checks

![image h:500px](https://images.contentstack.io/v3/assets/blt300387d93dabf50e/blt50458dd3b04743a2/5cb7328ab790c01122392558/pod-health-check.png)

---

## livenessProbe

```yaml
livenessProbe:
 exec:
   command:
     - cat
     - /tmp/live
```

```go
_, err := os.Create("/tmp/live")

…

defer os.Remove("/tmp/live")
```

---

## readinessProbe

/healthz

**200 OK**

---

## Rate Limit

```go
import "golang.org/x/time/rate"

limiter := rate.NewLimiter(5, 5)

if !limiter.Allow() {
    // StatusTooManyRequests              = 429 // RFC 6585, 4
}
```

---

## Load Test

```sh
go install github.com/tsenart/vegeta@latest

echo "GET http://:8081/limitz" | vegeta attack -rate=10/s -duration=1s | vegeta report
```

---

## Makefile

---

## Dockerfile

```dockerfile
FROM golang:1.17-buster AS build
WORKDIR /app
COPY go.mod ./
COPY go.sum ./
RUN go mod download
COPY . ./
ENV GOARCH=amd64
RUN go build -o /go/bin/app

## Deploy
FROM gcr.io/distroless/base-debian11
COPY --from=build /go/bin/app /app
EXPOSE 8081
USER nonroot:nonroot
CMD ["/app"]
```

---

## Docker build

```sh
docker build -t todo:test -f Dockerfile .
```

---

## Docker run

```sh
docker run -p:8081:8081 --env-file ./.env --link some-mariadb:db --name myapp todo:test
```

---

## Error Handling with Transaction Referrence

---

## Works with Frontend
