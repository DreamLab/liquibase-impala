# About liquibase-impala

Liquibase-impala is a [Liquibase](http://www.liquibase.org/) [extension](https://liquibase.jira.com/wiki/spaces/CONTRIB/overview), which adds support for Impala and Hive.

# Notes on compatibility

As of version 1.1.x the plugin was tested and should work with the following versions of external dependencies:

| Dependency          | Versions                     |
| :-----------------: | :--------------------------: |
| Liquibase           | 3.5.2, 3.5.3                 |
| Impala JDBC driver  | Cloudera Impala JDBC 2.5.32  |
| Hive JDBC driver    | Cloudera Impala Hive 2.5.18  |

**Other configurations are likely to work too** so you are encouraged to test with your versions. Let us know when you do!

# How to install

As of version 1.1.x liquibase-impala depends on proprietary Cloudera connectors for Impala and Hive. These are not present in any public Maven repositories.
Therefore, to build and install the plugin, you must do the following:

1. Download Impala JDBC driver and its dependencies from http://www.cloudera.com/downloads/connectors/impala/jdbc/2-5-32.html
2. Download Hive JDBC driver from http://www.cloudera.com/downloads/connectors/hive/jdbc/2-5-18.html
3. Unpack and install the following dependencies in your local Maven repository, using standard Maven command: 
```mvn install:install-file -Dfile=${file} -DgroupId=${groupId} -DartifactId=${artifactId} -Dversion=${version} -Dpackaging=jar```
| file                     | groupId                   | artifactId             | version |
| ------------------------ | ------------------------- | ---------------------- | ------- |
| ql.jar                   | com.cloudera.impala.jdbc  | ql                     | 2.5.32  |
| hive_metastore.jar       | com.cloudera.impala.jdbc  | hive_metastore         | 2.5.32  |
| hive_service.jar         | com.cloudera.impala.jdbc  | hive_metastore         | 2.5.32  |
| ImpalaJDBC41.jar         | com.cloudera.impala.jdbc  | ImpalaJDBC41.jar       | 2.5.32  |
| TCLIServiceClient.jar    | com.cloudera.impala.jdbc  | TCLIServiceClient.jar  | 2.5.32  |
| HiveJDBC41.jar           | com.cloudera.hive.jdbc    | HiveJDBC41.jar         | 2.5.18  |
4. _(optional, but recommended)_ Deploy the above artifacts to an internal, private Maven repository such as [Nexus](https://www.sonatype.com/nexus-repository-sonatype)
or [Artifactory](https://www.jfrog.com/artifactory/), for subsequent use.
5. Build liquibase-impala by executing ```mvn clean package```. This will create a _liquibase-impala.jar_ fat-jar in the _target/_ directory.
6. _(optional, but recommended)_ Deploy liquibase-impala to your internal, private Maven repository.

# How to use

Test the plugin:

1. cd examples/
2. modify liquibase.properties according to yours impala endpoint
3. put the artifact liquibase-impala.jar under the liquibase/lib directory
4. submit the job with the command ./liquibase --logLevel=DEBUG update
5. if you want to disable locking, submit the job on that manner JAVA_OPTS="${JAVA_OPTS} -Dliquibase.lock=false" ./liquibase --logLevel=DEBUG update

# How to test locally

Script ```examples/run.sh``` performs basic integration testing of Impala and Hive, which includes:
* update execution
* tag execution
* rollback execution
The script can be executed with the command ./run.sh <both|hive|impala> PATH_TO_LIQUIBASE_HOME
