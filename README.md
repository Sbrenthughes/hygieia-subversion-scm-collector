<!---
 Licensed to the Apache Software Foundation (ASF) under one or more
 contributor license agreements.  See the NOTICE file distributed with
 this work for additional information regarding copyright ownership.
 The ASF licenses this file to You under the Apache License, Version 2.0
 (the "License"); you may not use this file except in compliance with
 the License.  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

 Unless required by applicable law or agreed to in writing, software
 distributed under the License is distributed on an "AS IS" BASIS,
 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 See the License for the specific language governing permissions and
 limitations under the License.
-->

Hygieia Subversion SCM Collector
================================

[![Build Status](https://travis-ci.org/Hygieia/hygieia-subversion-scm-collector.svg?branch=master)](https://travis-ci.org/Hygieia/hygieia-subversion-scm-collector)
[![Coverage Status](https://coveralls.io/repos/github/Hygieia/hygieia-subversion-scm-collector/badge.svg?branch=master)](https://coveralls.io/github/Hygieia/hygieia-subversion-scm-collector?branch=master)


__Note.__ Another README is in the [gh-pages of the main HYGIEIA Repository](https://github.com/capitalone/Hygieia/blob/gh-pages/pages/hygieia/collectors/scm/subversion.md) branch. Please update it there.

---
title: Subversion Collector
tags:
keywords:
toc: true
summary:
sidebar: hygieia_sidebar
permalink: subversion.html
---
Configure the Subversion Collector to display and monitor information (related to code contribution activities) on the Hygieia Dashboard, from the Subversion repository. Hygieia uses Spring Boot to package the collector as an executable JAR file with dependencies.

### Setup Instructions

To configure the Subversion Collector, execute the following steps:

*   **Step 1: Change Directory**

Change the current working directory to the `subversion` directory of your Hygieia source code installation.

For example, in the Windows command prompt, run the following command:

```
cd C:\Users\[username]\hygieia\collectors\scm\subversion
```

*   **Step 2: Run Maven Build**

Run the maven build to package the collector into an executable jar file:

```bash
 mvn install
```

The output file `subversion-collector.jar` is generated in the `subversion\target` folder.

*   **Step 3: Set Parameters in Application Properties File**

Set the configurable parameters in the `application.properties` file to connect to the Dashboard MongoDB database instance, including properties required by the Subversion Collector.

For information about sourcing the application properties file, refer to the [Spring Boot Documentation](http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#boot-features-external-config-application-property-files).

To configure parameters for the Subversion Collector, refer to the sample [application.properties](#sample-application-properties-file) file.

*   **Step 4: Deploy the Executable File**

To deploy the `subversion-collector.jar` file, change directory to `subversion\target`, and then execute the following from the command prompt:

```bash
java -jar subversion-collector.jar --spring.config.name=subversion --spring.config.location=[path to application.properties file]
```

### Sample Application Properties File

The sample `application.properties` file lists parameter values to configure the Subversion Collector. Set the parameters based on your environment setup.

```properties
		# Database Name
		dbname=dashboarddb

		# Database HostName - default is localhost
		dbhost=localhost

		# Database Port - default is 27017
		dbport=27017

		# MongoDB replicaset
		dbreplicaset=[false if you are not using MongoDB replicaset]
		dbhostport=[host1:port1,host2:port2,host3:port3]

		# Database Username - default is blank
		dbusername=dashboarduser

		# Database Password - default is blank
		dbpassword=dbpassword

		# Logging File location
		logging.file=./logs/subversion.log

		# Collector schedule (required)
		subversion.cron=0 0/5 * * * *

		# Shared subversion username and password
		subversion.username=foo
		subversion.password=bar
		subversion.host=my.subversion.com

		# Maximum number of previous days from current date, when fetching commits
		subversion.commitThresholdDays=15
```

