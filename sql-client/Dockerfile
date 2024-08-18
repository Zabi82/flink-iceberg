###############################################################################
#  Licensed to the Apache Software Foundation (ASF) under one
#  or more contributor license agreements.  See the NOTICE file
#  distributed with this work for additional information
#  regarding copyright ownership.  The ASF licenses this file
#  to you under the Apache License, Version 2.0 (the
#  "License"); you may not use this file except in compliance
#  with the License.  You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
#  Unless required by applicable law or agreed to in writing, software
#  distributed under the License is distributed on an "AS IS" BASIS,
#  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#  See the License for the specific language governing permissions and
# limitations under the License.
###############################################################################

###############################################################################
# Build Click Count Job
###############################################################################

FROM maven:3.8.2-jdk-11-slim AS builder

###############################################################################
# Build SQL Playground Image
###############################################################################

FROM flink:1.18-scala_2.12-java11

# Copy sql-client script
COPY bin/* /opt/sql-client/
#copy a patch fix in sql-client.sh related to classpath 
COPY patch/* /opt/flink/bin/
RUN chmod 755 /opt/flink/bin/sql-client.sh
RUN mkdir -p /opt/sql-client/lib

# Download connector libraries
RUN wget -P /opt/sql-client/lib/ https://repo.maven.apache.org/maven2/org/apache/flink/flink-sql-connector-kafka/3.0.0-1.17/flink-sql-connector-kafka-3.0.0-1.17.jar;    
RUN wget -P /opt/sql-client/lib/ https://repo.maven.apache.org/maven2/org/apache/flink/flink-sql-avro-confluent-registry/1.18.0/flink-sql-avro-confluent-registry-1.18.0.jar;
RUN wget -P /opt/sql-client/lib/ https://repo.maven.apache.org/maven2/org/apache/flink/flink-connector-jdbc_2.11/1.11.0/flink-connector-jdbc_2.11-1.11.0.jar;
RUN wget -P /opt/sql-client/lib/ https://repo.maven.apache.org/maven2/mysql/mysql-connector-java/8.0.19/mysql-connector-java-8.0.19.jar;
RUN wget -P /opt/sql-client/lib/ https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk-bundle/1.12.648/aws-java-sdk-bundle-1.12.648.jar;
RUN wget -P /opt/sql-client/lib/ https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-aws/3.3.4/hadoop-aws-3.3.4.jar;
RUN wget -P /opt/sql-client/lib/ https://repo1.maven.org/maven2/software/amazon/awssdk/bundle/2.20.74/bundle-2.20.74.jar;
RUN wget -P /opt/sql-client/lib/ https://repo1.maven.org/maven2/org/apache/flink/flink-hadoop-fs/1.18.1/flink-hadoop-fs-1.18.1.jar;
RUN wget -P /opt/sql-client/lib/ https://repo1.maven.org/maven2/org/apache/commons/commons-configuration2/2.1.1/commons-configuration2-2.1.1.jar;
RUN wget -P /opt/sql-client/lib/ https://repo1.maven.org/maven2/commons-logging/commons-logging/1.1.3/commons-logging-1.1.3.jar;
RUN wget -P /opt/sql-client/lib/ https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-auth/3.3.4/hadoop-auth-3.3.4.jar;
RUN wget -P /opt/sql-client/lib/ https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-common/3.3.4/hadoop-common-3.3.4.jar;
RUN wget -P /opt/sql-client/lib/ https://repo1.maven.org/maven2/org/apache/hadoop/thirdparty/hadoop-shaded-guava/1.1.1/hadoop-shaded-guava-1.1.1.jar;
RUN wget -P /opt/sql-client/lib/ https://repo1.maven.org/maven2/org/codehaus/woodstox/stax2-api/4.2.1/stax2-api-4.2.1.jar;
RUN wget -P /opt/sql-client/lib/ https://repo1.maven.org/maven2/com/fasterxml/woodstox/woodstox-core/5.3.0/woodstox-core-5.3.0.jar;
RUN wget -P /opt/sql-client/lib/ https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-hdfs-client/3.3.4/hadoop-hdfs-client-3.3.4.jar;
RUN wget -P /opt/sql-client/lib/ https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-mapreduce-client-core/3.3.4/hadoop-mapreduce-client-core-3.3.4.jar;
RUN wget -P /opt/sql-client/lib/ https://repo1.maven.org/maven2/org/apache/iceberg/iceberg-flink-runtime-1.18/1.5.0/iceberg-flink-runtime-1.18-1.5.0.jar;

    
RUN wget -P /opt/flink/lib/ https://repo.maven.apache.org/maven2/org/apache/flink/flink-sql-connector-kafka/3.0.0-1.17/flink-sql-connector-kafka-3.0.0-1.17.jar;
RUN wget -P /opt/flink/lib/ https://repo1.maven.org/maven2/org/apache/iceberg/iceberg-flink-runtime-1.18/1.5.0/iceberg-flink-runtime-1.18-1.5.0.jar;
RUN wget -P /opt/flink/lib/ https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk-bundle/1.12.648/aws-java-sdk-bundle-1.12.648.jar;
RUN wget -P /opt/flink/lib/ https://repo.maven.apache.org/maven2/org/apache/flink/flink-sql-avro-confluent-registry/1.18.0/flink-sql-avro-confluent-registry-1.18.0.jar;
RUN wget -P /opt/flink/lib/ https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-aws/3.3.4/hadoop-aws-3.3.4.jar;
RUN wget -P /opt/flink/lib/ https://repo1.maven.org/maven2/software/amazon/awssdk/bundle/2.20.74/bundle-2.20.74.jar;

# Copy configuration
COPY conf/* /opt/flink/conf/

WORKDIR /opt/sql-client
ENV SQL_CLIENT_HOME /opt/sql-client

COPY docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]
