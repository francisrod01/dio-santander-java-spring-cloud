# dio-santander-java-product-catalog

Building a project with microservices architecture using Spring Cloud

Author: [Francis Rodrigues](https://github.com/francisrod01)

> Aprenda na prática como funciona uma arquitetura de software baseada em microsserviços, 
> os seus benefícios e desafios. by: [@Oswaldo Neto](https://github.com/oswaldoneto)

## Preparing the Development environment

Workspace uses:

- Docker 19.3.15
- Docker compose 1.29.2
- Java OpenJDK 16
- Gradle
- Spring Boot 2.5.2

### Install Docker Compose

You can run Compose on macOS, Windows, and 64-bit Linux.

https://docs.docker.com/compose/install/


Command on linux:

```bash
~$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

### Compose V2 beta

Compose V2 and the new `docker compose` command

https://docs.docker.com/compose/cli-command/


## Running the application

#### Product-catalog application

Let's start by running the Spring application using your favourite IDE.


```bash
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v2.5.2)

2021-07-15 16:23:05.227  INFO 6615 --- [           main] o.d.e.p.ProductCatalogApplication        : Starting ProductCatalogApplication using Java 16.0.1 on debian with PID 6615 (/home/paneladm/projects/dio-santander-java-spring-cloud/product-catalog/build/classes/java/main started by paneladm in /home/paneladm/projects/dio-santander-java-spring-cloud/product-catalog)
2021-07-15 16:23:05.231  INFO 6615 --- [           main] o.d.e.p.ProductCatalogApplication        : No active profile set, falling back to default profiles: default
2021-07-15 16:23:08.963  INFO 6615 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Bootstrapping Spring Data Elasticsearch repositories in DEFAULT mode.
2021-07-15 16:23:09.168  INFO 6615 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Finished Spring Data repository scanning in 198 ms. Found 1 Elasticsearch repository interfaces.
2021-07-15 16:23:10.638  INFO 6615 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Bootstrapping Spring Data Reactive Elasticsearch repositories in DEFAULT mode.
2021-07-15 16:23:10.664  INFO 6615 --- [           main] .s.d.r.c.RepositoryConfigurationDelegate : Finished Spring Data repository scanning in 25 ms. Found 0 Reactive Elasticsearch repository interfaces.
2021-07-15 16:23:12.270  INFO 6615 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2021-07-15 16:23:12.314  INFO 6615 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2021-07-15 16:23:12.314  INFO 6615 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.48]
2021-07-15 16:23:12.646  INFO 6615 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2021-07-15 16:23:12.647  INFO 6615 --- [           main] w.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 7049 ms
2021-07-15 16:23:15.982  INFO 6615 --- [           main] o.s.d.elasticsearch.support.VersionInfo  : Version Spring Data Elasticsearch: 4.2.2
2021-07-15 16:23:16.007  INFO 6615 --- [           main] o.s.d.elasticsearch.support.VersionInfo  : Version Elasticsearch Client in build: 7.12.1
2021-07-15 16:23:16.007  INFO 6615 --- [           main] o.s.d.elasticsearch.support.VersionInfo  : Version Elasticsearch Client used: 7.12.1
2021-07-15 16:23:16.008  INFO 6615 --- [           main] o.s.d.elasticsearch.support.VersionInfo  : Version Elasticsearch cluster: 6.6.2
2021-07-15 16:23:16.008  WARN 6615 --- [           main] o.s.d.elasticsearch.support.VersionInfo  : Version mismatch in between Elasticsearch Client and Cluster: 7.12.1 - 6.6.2
2021-07-15 16:23:16.847  INFO 6615 --- [           main] o.s.b.a.e.web.EndpointLinksResolver      : Exposing 1 endpoint(s) beneath base path '/actuator'
2021-07-15 16:23:16.909  INFO 6615 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2021-07-15 16:23:16.926  INFO 6615 --- [           main] o.d.e.p.ProductCatalogApplication        : Started ProductCatalogApplication in 15.659 seconds (JVM running for 20.712)
2021-07-15 16:23:47.529  INFO 6615 --- [nio-8080-exec-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring DispatcherServlet 'dispatcherServlet'
2021-07-15 16:23:47.529  INFO 6615 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Initializing Servlet 'dispatcherServlet'
2021-07-15 16:23:47.531  INFO 6615 --- [nio-8080-exec-1] o.s.web.servlet.DispatcherServlet        : Completed initialization in 2 ms
```

Two lines that interest us:

- Tomcat started on port(s): 8080
- Exposing 1 endpoint(s) beneath base path '/actuator'

After started, we should be able to reach the following url:

```bash
~$  curl http://localhost:8080/actuator | json_pp
```

and see the endpoints returned:


```bash
% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                               Dload  Upload   Total   Spent    Left  Speed
100   243    0   243    0     0  13453      0 --:--:-- --:--:-- --:--:-- 14294
{
   "_links" : {
      "self" : {
         "templated" : false,
         "href" : "http://localhost:8080/actuator"
      },
      "health" : {
         "href" : "http://localhost:8080/actuator/health",
         "templated" : false
      },
      "health-path" : {
         "href" : "http://localhost:8080/actuator/health/{*path}",
         "templated" : true
      }
   }
}
```

#### Running Elasticsearch and redis

Inside the `docker-services` folder we have a file the can start two important services for our application:

```yml
version: '2'

services:

    elasticsearch:
        container_name: 'elasticsearch'
        image: elasticsearch:6.6.2
        ports:
            - 9200:9200
            - 9300:9300
        environment:
            - discovery.type=single-node

    redis:
        container_name: "redis"
        image: redis:3.0.1
        ports:
            - 6379:6379
```

You can start them by running `docker-compose up -d` inside the folder, so it will run the file automatically.

More about how to use [Docker compose][1]

To check the services health, go to `http://localhost:8080/actuator/health` and see the output:

```json
{ "status" : "UP" }
```

[1]: https://docs.docker.com/compose/install/
