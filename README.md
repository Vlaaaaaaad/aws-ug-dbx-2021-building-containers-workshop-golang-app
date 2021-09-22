# Go web app

Proof-of-Concept (PoC) application that returns a name. It is indented to be called by another application that composes a "_Greeting name!_" output.

For example for "_Hello world!_" this app would be the one providing the "_world_".

![Architecture diagram](./assets/poc-hello-world.png)

## Commands

Dependencies are defined in `go.mod` and `go.sum`. To install the dependencies:

```console
go mod download && go mod verify
```

To build the application and output an executable named `example`:

```console
go build -o example .
```

To run the application:

```console
./example
```

To run a container with the application:

```console
docker run --interactive --tty --rm \
  --publish 5003:5003 \
  YOUR_IMAGE_ID_HERE
```

Endpoints exposed by the application:

```console
# curl -v http://localhost:5003
  *   Trying ::1...
  * TCP_NODELAY set
  * Connected to localhost (::1) port 5003 (#0)
  > GET / HTTP/1.1
  > Host: localhost:5003
  > User-Agent: curl/7.64.1
  > Accept: */*
  >
  < HTTP/1.1 200 OK
  < Access-Control-Allow-Headers: Accept, Accept-Language, Content-Type, X-Version, X-Reply-Service
  < Access-Control-Allow-Methods: GET, OPTIONS
  < Access-Control-Allow-Origin: *
  < Content-Type: application/json
  < X-Reply-Service: namer-service
  < X-Version: dev
  < Date: Thu, 1 Apr 1000 10:10:09 GMT
  < Content-Length: 17
  <
  {"name":"world"}

# curl -v http://localhost:5003/status/alive
  *   Trying ::1...
  * TCP_NODELAY set
  * Connected to localhost (::1) port 5003 (#0)
  > GET /status/alive HTTP/1.1
  > Host: localhost:5003
  > User-Agent: curl/7.64.1
  > Accept: */*
  >
  < HTTP/1.1 200 OK
  < Access-Control-Allow-Headers: Accept, Accept-Language, Content-Type, X-Version, X-Reply-Service
  < Access-Control-Allow-Methods: GET, OPTIONS
  < Access-Control-Allow-Origin: *
  < Content-Type: application/json
  < X-Reply-Service: namer-service
  < X-Version: dev
  < Date: Thu, 1 Apr 1000 10:10:10 GMT
  < Content-Length: 38
  <

  {"status":"Namer service is alive"}

# curl -v http://localhost:5003/status/heathy
  *   Trying ::1...
  * TCP_NODELAY set
  * Connected to localhost (::1) port 5003 (#0)
  > GET /status/healthy HTTP/1.1
  > Host: localhost:5003
  > User-Agent: curl/7.64.1
  > Accept: */*
  >
  < HTTP/1.1 200 OK
  < Access-Control-Allow-Headers: Accept, Accept-Language, Content-Type, X-Version, X-Reply-Service
  < Access-Control-Allow-Methods: GET, OPTIONS
  < Access-Control-Allow-Origin: *
  < Content-Type: application/json
  < X-Reply-Service: namer-service
  < X-Version: dev
  < Date: Thu, 1 Apr 1000 10:10:11 GMT
  < Content-Length: 40
  <

  {"status":"Namer service is healthy"}
```
