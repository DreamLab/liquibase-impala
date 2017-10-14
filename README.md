# About liquibase-impala

Liquibase-impala is a [Liquibase](http://www.liquibase.org/) [extension](https://liquibase.jira.com/wiki/spaces/CONTRIB/overview), which adds support for Impala and Hive.

# Notes on compatibility

As of version 1.1.x the plugin was tested and should work with the following versions of external dependencies:

| Dependency          | Versions                     |
| :-----------------: | :--------------------------: |
| Liquibase           | 3.5.2, 3.5.3                 |
| Impala JDBC driver  | Cloudera Impala JDBC 2.5.32  |
| Hive JDBC driver    | Cloudera Impala Hive 2.5.18  |

**Other canfigurations are likely to work too** so you are encouraged to test with your versions. Let us know when you do!

# How to install

Download jdbc driver and dependencies from http://www.cloudera.com/downloads/connectors/impala/jdbc/2-5-32.html

Unpack and put dependencies to local maven repository with the commands provided below

mvn install:install-file -Dfile=ql.jar -DgroupId=com.cloudera.impala.jdbc -DartifactId=ql -Dversion=2.5.32 -Dpackaging=jar

mvn install:install-file -Dfile=hive_metastore.jar -DgroupId=com.cloudera.impala.jdbc -DartifactId=hive_metastore -Dversion=2.5.32 -Dpackaging=jar

mvn install:install-file -Dfile=hive_service.jar -DgroupId=com.cloudera.impala.jdbc -DartifactId=hive_service -Dversion=2.5.32 -Dpackaging=jar

mvn install:install-file -Dfile=ImpalaJDBC41.jar -DgroupId=com.cloudera.impala.jdbc -DartifactId=ImpalaJDBC41 -Dversion=2.5.32 -Dpackaging=jar

mvn install:install-file -Dfile=TCLIServiceClient.jar -DgroupId=com.cloudera.impala.jdbc -DartifactId=TCLIServiceClient -Dversion=2.5.32 -Dpackaging=jar

mvn install:install-file -Dfile=HiveJDBC41.jar -DgroupId=com.cloudera.hive.jdbc -DartifactId=ImpalaJDBC41 -Dversion=2.5.32 -Dpackaging=jar

# How to use

Test the plugin:

1. cd examples/

2. modify liquibase.properties according to yours impala endpoint

3. put the artifact liquibase-imapala.jar under the liquibase/lib directory

4. submit the job with the command ./liquibase --logLevel=DEBUG update

5. if you want to disable locking, submit the job on that manner JAVA_OPTS="${JAVA_OPTS} -Dliquibase.lock=false" ./liquibase --logLevel=DEBUG update

# How to test locally

Test the plugin:

1. cd examples/

2. modify liquibase.properties according to yours impala endpoint

3. put the artifact liquibase-imapala.jar under the liquibase/lib directory

4. submit the job with the command ./liquibase --logLevel=DEBUG update

5. if you want to disable locking, submit the job on that manner JAVA_OPTS="${JAVA_OPTS} -Dliquibase.lock=false" ./liquibase --logLevel=DEBUG update

6. script run.sh perform basic integration testing for Impala and Hive, which includes:
    - update execution
    - tag execution
    - rollback execution
    script can be submitted with the command ./run.sh <both|hive|impala> PATH_TO_LIQUIBASE_HOME
