# Datomic REST

A base image for running the Datomic REST service shipped with Datomic Pro
Starter Edition.

This Dockerfile defines the necessary automation steps for downloading and
running Datomic REST, while deferring all privileged, user-specific
configuration to a derived image via ONBUILD instructions. The image is heavily
based on [https://hub.docker.com/r/pointslope/datomic-console/](https://hub.docker.com/r/pointslope/datomic-console/).

## How

Create a directory containing a file called `.credentials` containing your
Datomic user and download key:

```
user@comp.com:key
```

In the same directory, create the following `Dockerfile`:

```
FROM cjohansen/datomic-rest:0.9.5544
CMD ["dev", "datomic:dev://transactor-host:4334"]
```

Adjust the transactor location as needed.

Build the image and run a container from the result:

```sh
docker build -t my-datomic-rest:0.9.5544 .
docker run -d -p 8001:8001 --network mynw --name datomic-rest my-datomic-rest:0.9.5544
```
