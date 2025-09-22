## Web Server (Java)

Minimal Java socket servers implemented in three variants:
- Single-threaded server with a simple client
- Multi-threaded server with a simple client
- Thread pool-based server

### Requirements
- Java JDK 11 or newer (`javac` and `java` on PATH)
- Linux/macOS shell (commands use Bash)

### Project layout
- `singleThreaded/` — package `singleThreaded` with `Server` and `Client` on port 8090
- `multiThreaded/` — package `multiThreaded` with `Server` and `Client` on port 8010
- `threadPool/` — package `threadPool` with `Server` on port 8010

### Build
From the project root (`/home/raghu/Documents/webserver`):

```bash
mkdir -p out
javac -d out singleThreaded/*.java
javac -d out multiThreaded/*.java
javac -d out threadPool/*.java
```

This compiles all sources into the `out/` directory, preserving package structure.

### Run: Single-threaded variant
Server (port 8090):

```bash
java -cp out singleThreaded.Server
```

Client (in a separate terminal):

```bash
java -cp out singleThreaded.Client
```

Expected: client prints a single line response from the server.

### Run: Multi-threaded variant
Server (port 8010):

```bash
java -cp out multiThreaded.Server
```

Client (spawns many concurrent requests):

```bash
java -cp out multiThreaded.Client
```

Expected: multiple responses printed, one per client thread.

### Run: Thread pool variant
Server (port 8010, fixed-size pool):

```bash
java -cp out threadPool.Server
```

Note: There is no client for this variant in the repo. You can:
- Reuse `multiThreaded.Client` against port 8010, or
- Use `nc` to test: `printf 'ping\n' | nc localhost 8010`

### Clean

```bash
rm -rf out
```

### Notes
- Ensure no other process is using ports 8090 or 8010.
- Servers log basic connection info to stdout and run until terminated (Ctrl+C).
