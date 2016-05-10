# gateway

This application was generated using JHipster, you can find documentation and help at [https://jhipster.github.io](https://jhipster.github.io).

~~~
                                                   /-------------\
                                                   |   Browser   |
                                                   \------+------/
                                                          |
                                                          |
                                                          V 8080
                               /-----------------------------------------------------\
                               | Gateway                                             |
                               | +-----------+    +--------------+      +----------+ |
                               | |           |    |  Zuul Proxy  |      |          | |     +-------+
                               | | Angular   |    |              |      |  Access  +-|---->|       |
                               | | App       |    +--------------+      |  Control | |     | Users |
                               | |           |    |    Ribbon    |      |          | |     | Roles |
                               | +-----------+    +---+------+---+      +----------+ |     +-------+
                               |                      |      |                       |
                               \-+---------------------------------------------------/
                                 |                    |      |       
                                 |                    |      |                              
                                 |                    |      |                        
                                 |        +-----------/      \----------------+            
/-----------------------\        |        |                                   |
| JHipster Registry     |        |        V 8081                              V 8082
|                       |        | /-------------\     +-----+         /-------------\     +-----+
|  +-----------------+  |        | |             |     |     |         |             |     |     |
|  | Eureka Server   |  |        | |  Service 1  +---->| DB1 |         |  Service 2  +---->| DB2 |
|  +-----------------+  |        | |             |     |     |         |             |     |     |
|  | Config Server   |  |        | \--+-----+----/     +-----+         +--+------+---/     +-----+
|  +--------+--------+  |  8761  |    |     |                             |      |
|           |           |<-------+----+-----------------------------------/      |
\-----------------------/                   |                                    |
            |                               \-------------+----------------------/
            V                                             |
        +-------+                                         |
        |       |                 /------------------------------------------------\
        |  Git  |                 | ELK                   |                        | 
        |  Repo |                 |                       V 5000                   |
        +-------+                 | +---------+      +----------+      +--------+  |
                                  | | Elastic |      | Logstash |      | Kibana |  |
                                  | | Search  |<-----|          |      |        |  |
                                  | +---------+      +----------+      +--------+  |
                                  \------------------------------------------------/
~~~


## Development

Before you can build this project, you must install and configure the following dependencies on your machine:


## Building for production

To optimize the gateway client for production, run:

    ./gradlew -Pprod clean bootRepackage

To ensure everything worked, run:

    java -jar build/libs/*.war --spring.profiles.active=prod

## Continuous Integration

To setup this project in Jenkins, use the following configuration:

* Project name: `gateway`
* Source Code Management
    * Git Repository: `git@github.com:xxxx/gateway.git`
    * Branches to build: `*/master`
    * Additional Behaviours: `Wipe out repository & force clone`
* Build Triggers
    * Poll SCM / Schedule: `H/5 * * * *`
* Build
    * Invoke Gradle script / Use Gradle Wrapper / Tasks: `-Pprod clean test bootRepackage`
* Post-build Actions
    * Publish JUnit test result report / Test Report XMLs: `build/test-results/*.xml`

[JHipster]: https://jhipster.github.io/
