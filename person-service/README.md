# Getting GitOps. 
## The source code of the example service

This folder contains the Java sources of the Quarkus example. If you want to deploy it on OpenShift, please make sure to first install a PostgreSQL server, either via Crunchy Data Operator or by instantiating the template `postgresql-persistent`. 

```bash
$ oc new-app postgresql-persistent \
	-p POSTGRESQL_USER=wanja \
	-p POSTGRESQL_PASSWORD=wanja \
	-p POSTGRESQL_DATABASE=wanjadb \
	-p DATABASE_SERVICE_NAME=wanjaserver
```

The complete setup and structure of this example is being discussed in chapter 1 of the book. Please have a look there. 

How to change port in Quarkus:
1. Change Quarkus HTTP port:
- Overide the default 8080 port, set the `quarkus.http.port` property in your application properties file (`src/main/resources/application.properties`)
```quarkus.http.port=8082```
- If you only using `YAML` application configuration (`src/main/resources/application.yaml`)
```yaml
quarkus:
  http:
    port: 8082
```
2. Change HTTP server port at runtime:
- You can also override the build time preconfigured server port at runtime by providung the `quarkus.http.port` property in your runtime System properties.
```bash
java -Dquarkus.http.port=8082 target/quarkus-app/quarkus-run.jar
```
- Or if you are packaging your application in Native mode:
```bash
./target/artifac-1.0.0-SNAPSHOT-runner -Dquarkus.http.port=8082
```

