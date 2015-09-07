

## Benchmarks

Server type: Echo server.

Conditions:

CONN_COUNT = 3000 concurrent connections 
DURATION = 30s.

Running the echo server and the client on localhost.

The haskell client creates CONN_COUNT lightweight threads that each open
socket connections send data, receive the echoed data and close the socket.
They check the current time after each request and stop if DURATION have passed. 

Measuring the number of requests completed by the server.

The benchmark is not great. I am unsure if the request strategy is legit. i should measure latency average and standard deviation.

Here are some preliminary numbers.

#### rust coio

the server completed 261102
 3000 30  38.21s user 29.62s system 210% cpu 32.226 total

#### golang

the server completed 297555
 3000 30  39.70s user 32.89s system 214% cpu 33.897 total

#### haskell conduit

the server completed 192420
 3000 30  38.06s user 21.22s system 153% cpu 38.668 total

#### nodejs

the server completed 195653
 3000 30  33.23s user 23.44s system 165% cpu 34.171 total

#### ruby eventmachine

the server completed 294525
 3000 30  40.14s user 32.41s system 198% cpu 36.633 total

#### clojure aleph (netty)

the server completed 202087
 3000 30  30.22s user 22.82s system 171% cpu 30.992 total

#### elixir

crashes with strange errors under heavy load. I am currently running it
with

```bash
elixirc server.ex
elixir -e Echo.Server.main
```

I am not familiar with elixir/erlang now so i am not sure this is the right way to run a beam file.