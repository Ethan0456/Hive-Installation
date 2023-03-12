# Hive-Installation

**Step 1:**  Download **Hive tar.**

`Command: wget [https://dlcdn.apache.org/hive/hive-4.0.0-alpha-2/apache-hive-4.0.0-alpha-2-bin.tar.gz](https://dlcdn.apache.org/hive/hive-4.0.0-alpha-2/apache-hive-4.0.0-alpha-2-bin.tar.gz)`
![Untitled](https://user-images.githubusercontent.com/88190547/224557968-4398fb15-5060-4b21-8c1c-589cfe9bf197.png)

**Step 2:**  Extract the tar file.

`Command: tar -xzf apache-hive-4.0.0-alpha-2-bin.tar.gz`

**Step 3:** Edit the **“.bashrc”** file to update the environment variables for user.
`Command:  sudo nvim .bashrc`

Add the following at the end of the file:

![Untitled 1](https://user-images.githubusercontent.com/88190547/224558044-1f9366cd-249e-4461-a55d-ef3a8d342ea7.png)

Run the below command to make changes work in same terminal.

`Command: source .bashrc`

**Step 4:**  Create Hive directories within HDFS. The directory ‘warehouse’ is the location to store the table or data related to hive.

`Command:`

`hdfs dfs -mkdir -p /user/hive/warehouse
 hdfs dfs -mkdir /tmp`

**Step 5:** Set read/write permissions for table.

In this command, we are giving write permission to the group:

`Command:`

`hdfs dfs -chmod g+w /user/hive/warehouse
hdfs dfs -chmod g+w /tmp`

**Step 6:**  Set Hadoop path in [hive-env.sh](http://hive-env.sh/)

`Command: cd apache-hive-4.0.0-alpha-2-bin/`

`Command: gedit conf/hive-env.sh`
![Untitled 2](https://user-images.githubusercontent.com/88190547/224558083-5a655aea-ef39-46ff-8619-aba9d9526bb3.png)

**Step 7:** Edit hive-site.xml

**`Command:** gedit conf/hive-site.xml`

add below lines

```
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<?xml-stylesheet type="text/xsl" href="configuration.xsl"?><!--
Licensed to the Apache Software Foundation (ASF) under one or more
contributor license agreements. See the NOTICE file distributed with
this work for additional information regarding copyright ownership.
The ASF licenses this file to You under the Apache License, Version 2.0
(the "License"); you may not use this file except in compliance with
the License. You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
-->
<configuration>
<property>
<name>javax.jdo.option.ConnectionURL</name>
<value>jdbc:derby:;databaseName=/home/hadoop/hive/apache-hive-4.0.0-alpha-2-bin/metastore_db;create=true</value>
<description>
JDBC connect string for a JDBC metastore.
To use SSL to encrypt/authenticate the connection, provide database-specific SSL flag in the connection URL.
For example, jdbc:postgresql://myhost/db?ssl=true for postgres database.
</description>
</property>
<property>
<name>hive.metastore.warehouse.dir</name>
<value>/user/hive/warehouse</value>
<description>location of default database for the warehouse</description>
</property>
<property>
<name>hive.metastore.uris</name>
<value/>
<description>Thrift URI for the remote metastore. Used by metastore client to connect to remote metastore.</description>
</property>
<property>
<name>javax.jdo.option.ConnectionDriverName</name>
<value>org.apache.derby.jdbc.EmbeddedDriver</value>
<description>Driver class name for a JDBC metastore</description>
</property>
<property>
<name>javax.jdo.PersistenceManagerFactoryClass</name>
<value>org.datanucleus.api.jdo.JDOPersistenceManagerFactory</value>
<description>class implementing the jdo persistence</description>
</property>
</configuration>
```

**Step 8:** By default, Hive uses Derby database. Initialize Derby database.

`Command: bin/schematool -initSchema -dbType derby`
![Untitled 3](https://user-images.githubusercontent.com/88190547/224558114-bd19d0af-c792-4296-b7b6-287c4bc8c353.png)

**Step 9:** Launch Hive.

**`Command:** hive`

![Untitled 4](https://user-images.githubusercontent.com/88190547/224558140-599fac74-a91f-4c4d-9fae-9423a4404aaf.png)
