# "Hello World" using [Helidon](https://helidon.io)

This project implements a simple Hello World REST service using Helidon SE.

## Build and run

With JDK8+
```bash
mvn package
java -jar target/novatec-hello.jar
```

## Exercise the application

```
curl -X GET http://localhost:8080/greet
Hello World
```

## Try health and metrics

```
curl -s -X GET http://localhost:8080/health
{"outcome":"UP",...
. . .

```

## Build the Docker Image

```
docker build -t novatec-hello .
```

## Start the application with Docker

```
docker run --rm -p 8080:8080 novatec-hello:latest
```

Exercise the application as described above

## Deploy the application to Kubernetes

```
kubectl cluster-info                # Verify which cluster
kubectl get pods                    # Verify connectivity to cluster
kubectl create -f app.yaml   # Deply application
kubectl get service novatec-hello  # Get service info
```

## Native image with GraalVM

GraalVM allows you to compile your programs ahead-of-time into a native
 executable. See https://www.graalvm.org/docs/reference-manual/aot-compilation/
 for more information.

You can build a native executable in 2 different ways:
* With a local installation of GraalVM
* Using Docker

### Local build

Download Graal VM at https://www.graalvm.org/downloads, the versions
 currently supported for Helidon are `19.2` and `19.3`.

```
# Setup the environment
export GRAALVM_HOME=/path
# build the native executable
mvn package -Pnative-image
```

You can also put the Graal VM `bin` directory in your PATH, or pass
 `-DgraalVMHome=/path` to the Maven command.

See https://github.com/oracle/helidon-build-tools/tree/master/helidon-maven-plugin
 for more information.

Start the application:

```
./target/novatec-hello
```