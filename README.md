# Doing Marketing with GenAI Tools 📘 !

[![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/goodbards-ai/marketing-with-genai-workshop)
[![License Apache2](https://img.shields.io/hexpm/l/plug.svg)](http://www.apache.org/licenses/LICENSE-2.0)

> ⚠️ Difficulty: **`Beginner`, we have you covered.**

Learn how to build an app end-to-end application with Spring ecosystem *(boot, mvc, security, data, test, thymeleaf)* and Apache Cassandra™.

## 📋 Table of content

<img src="https://github.com/goodbards-ai/marketing-with-genai-workshop/blob/main/img/01-assistant.png?raw=true" align="right" width="400px"/>

**HOUSEKEEPING**
- [Objectives](#objectives)
- [Acknowledgements](#acknowledgements)
- [Frequently asked questions](#frequently-asked-questions)
- [Materials for the Session](#materials-for-the-session)

[**LAB1 - NarrowAI Demo**](#)
- [1.1 - Import Data](#)
- [1.2 - Train a modle](#)
- [1.3 - Run a model](#)

[**LAB2 - Generative AI Landscape**](#2-application-implementation)
- [2.1 - Connect to Goodbards](#)
- [2.2 - Interact with GPT](#)
- [2.3 - Interact with Gemini](#)
- [2.4 - Image Generation with Dall-e](#)
- [2.5 - Retrieval Augmented Generation](#)

[**LAB3 - Run a Marketing campaign**](#)
- [3.1 - Prompt Templating](#)
- [3.2 - Content Generation](#)
- [3.3 - Content Publication](#)
- [2.4 - Campaign Tracking](#)
- [2.5 - Tactics and Scheduling](#)

[**Homeworks**](#homeworks)

## HouseKeeping

### Objectives

* Discover how to use the following technologies: 
  * **Spring Data:** the Object Mapping layer of Spring
  * **Spring Data Cassandra:** what traps to avoid
  * **Spring Security:** how to handle authentication with OAuth2
  * **Spring MVC:** how to expose REST API and controllers
  * **Spring Webflux:** how to use the new `WebClient`
  * **Thymeleaf:** how to build a user interface with Spring
  * **Spring Test:** How to run tests
  * **Astra DB** (a Database-as-a-service built on Apache Cassandra)
* Han fun with an interactive session

### Acknowledgements

This application has been built based on the work of [**Java Brains**](https://www.youtube.com/channel/UCYt1sfh5464XaDBH0oH_o7Q), a famous youtuber *(500k+ subscribers)*. On his channel you can find the full [*Code with me Series*](https://www.youtube.com/watch?v=LxVGFBRpEFM), 16 episodes for building this application step-by-step. The link to each episode is provided at the end of this readme.

### Frequently asked questions

<p/>
<details>
<summary><b> 1️⃣ Can I run this workshop on my computer?</b></summary>
<hr>
<p>There is nothing preventing you from running the workshop on your own machine, If you do so, you will need the following
<ol>
<li><b>git</b> installed on your local system
<li><b>JDK 8+</b> installed on your local system
<li><b>Maven 3.6+</b> installed on your local system
</ol>
</p>
In this readme, we try to provide instructions for local development as well - but keep in mind that the main focus is development on Gitpod, hence <strong>We can't guarantee live support</strong> about local development in order to keep on track with the schedule. However, we will do our best to give you the info you need to succeed.
</details>
<p/>
<details>
<summary><b> 2️⃣ What other prerequisites are required?</b></summary>
<hr>
<ul>
<li>You will need an enough *real estate* on screen, we will ask you to open a few windows and it does not file mobiles (tablets should be OK)
<li>You will need a GitHub account eventually a google account for the Google Authentication (optional)
<li>You will need an Astra account: don't worry, we'll work through that in the following
<li>As Intermediate level we expect you to know what java and Spring are. 
</ul>
</p>
</details>
<p/>
<details>
<summary><b> 3️⃣ Do I need to pay for anything for this workshop?</b></summary>
<hr>
<b>No.</b> All tools and services we provide here are FREE. FREE not only during the session but also after.
</details>
<p/>
<details>
<summary><b> 4️⃣ Will I get a certificate if I attend this workshop?</b></summary>
<hr>
Attending the session is not enough. You need to complete the homeworks detailed below and you will get a nice badge that you can share on linkedin or anywhere else *(open api badge)*
</details>
<p/>

> [🏠 Back to Table of Contents](#-table-of-content)

### Materials for the Session

It doesn't matter if you join our workshop live or you prefer to work at your own pace,
we have you covered. In this repository, you'll find everything you need for this workshop:

- [Slide deck](/slides/slides.pdf)
- [Discord chat](https://dtsx.io/discord)
- [Questions and Answers](https://community.datastax.com/)
- [Twitch backup](https://www.twitch.tv/datastaxdevs)

----

## 1. Database Initialization

### 1.1 - Create an Astra Account

> **Note**: **Datastax Astra** is a cloud-native, fully managed database-as-a-service (DBaaS) based on Apache Cassandra. It provides a scalable, performant and highly available database solution without the operational overhead of managing Cassandra clusters. Astra supports both SQL and NoSQL APIs, and includes features like backup and restore, monitoring and alerting, and access control. It enables developers to focus on application development while the database infrastructure is managed by Datastax.

- `✅ 1.1.a` - Access [https://astra.datastax.com](https://astra.datastax.com) and register with `Google` or `Github` account

![](https://github.com/DataStax-Academy/cassandra-for-data-engineers/blob/main/images/setup-astra-1.png?raw=true)

### 1.2 - Create an Astra Token

- `✅ 1.2.a` Locate `Settings` (#1) in the menu on the left, then `Token Management` (#2) 

- `✅ 1.2.b`Select the role `Organization Administrator` before clicking `[Generate Token]`

![](https://github.com/DataStax-Academy/cassandra-for-data-engineers/blob/main/images/setup-astra-2.png?raw=true)

- `✅ 1.2.c` - Copy your token in the clipboard. With this token we will now create what is needed for the training.

![](https://github.com/DataStax-Academy/cassandra-for-data-engineers/blob/main/images/setup-astra-3.png?raw=true)

### 1.3 - Open your Environment

> **Note**: **Gitpod** is a cloud-based integrated development environment (IDE) that allows developers to build, test and run applications directly in their web browser. It provides preconfigured dev environments for GitHub projects, so developers can start coding immediately without setting up local environment. Gitpod saves time and streamlines the development process.

> `✅ 1.3.a` ↗️ _Right Click and select open as a new Tab..._
>
> [![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/datastaxdevs/workshop-betterreads)

### 1.4 - Setup Astra CLI

> **Note**:  The **Astra CLI** is a command-line interface (CLI) tool for managing Apache Cassandra databases hosted on Datastax Astra. It allows developers to perform tasks like creating and managing databases, executing Cassandra queries, and managing security and access control. The Astra CLI simplifies database management and provides an alternative to the Astra web interface, enabling automation and integration with other tools and workflows.

- `✅ 1.4.a` **Locate the terminal called `setup` and check that the CLI is available**

```
astra --version
```

> 🖥️ `output`
>
> ```
> $ astra --version
> 0.2.1
> ```

- `✅ 1.4.b` **Trigger the setup command**

```
astra setup
```

> 🖥️ `output`
>
> ```
>     _____            __                  
>    /  _  \   _______/  |_____________    
>   /  /_\  \ /  ___/\   __\_  __ \__  \  
>  /    |    \\___ \  |  |  |  | \// __ \_ 
>  \____|__  /____  > |__|  |__|  (____  /
>          \/     \/                   \/ 
>            Version: 0.2.1
> 
>  -----------------------
>  ---      SETUP      ---
>  -----------------------
> 
> $ Enter an Astra token:
> ```

- `✅ 1.4.c` **Provide your token as asked (starting witg AstraCS:..)**

> 🖥️ `output`
>
> ```
> [OK]    Configuration has been saved.
> [OK]    Enter 'astra help' to list available commands.
> ```

- `✅ 1.4.d` **List your existing Users.**

```bash
astra user list
```

> 🖥️ `output`
>
> ```
> +--------------------------------------+-----------------------------+---------------------+
> | User Id                              | User Email                  | Status              |
> +--------------------------------------+-----------------------------+---------------------+
> | b665658a-ae6a-4f30-a740-2342a7fb469c | cedrick.lunven@datastax.com | active              |
> +--------------------------------------+-----------------------------+---------------------+
> ```

### 1.5 - Create database

- `✅ 1.5.a` **Create database `workshops` with keyspace `better_reads`**

```bash
astra db create workshops -k better_reads --if-not-exist
```

> 🖥️ `Output`
>
> ```
> [ INFO ] - Database 'workshops' already exist. Connecting to database.
> [ INFO ] - Database 'workshops' has status 'MAINTENANCE' waiting to be 'ACTIVE' ...
>[ INFO ] - Database 'workshops' has status 'ACTIVE' (took 7983 millis)
> ```

| Chunk         | Description     |
|--------------|-----------|
| `db create` | Operation executed `create` in group `db`  |
| `workshops` | Name of the database, our argument |
|`-k better_reads` | Name of the keyspace, a db can contains multiple keyspaces |
| `--if-not-exist` | Flag for itempotency creating only what if needed |

> **Note**: If the database already exist but has not been used for while the status will be `HIBERNATED`. The previous command will resume the db an create the new keyspace but it can take about a minute to execute.
>
> ```
> [OK]    Resuming Database 'com.dtsx.astra.sdk.db.domain.Database@406005b3' ...
> [INFO]  Database 'workshops' has status 'RESUMING' waiting to be 'ACTIVE' ...
> [INFO]  Database 'workshops' has status 'ACTIVE' (took 41466 millis)
> [INFO]  Keyspace  'workshops' already exists. Connecting to keyspace.
> [OK]    Database 'workshops' is ready.
> ```

- `✅ 1.5.b` **Check the status of database `workshops`**

```bash
astra db status workshops
```

> 🖥️ `output`
>
> ```
> [ INFO ] - Database 'workshops' has status 'ACTIVE'
> ```

- `✅ 1.5.c` **Get the informations for your database including the keyspace list**

```bash
astra db get workshops
```

> 🖥️ `output`
>
> ```
> +------------------------+-----------------------------------------+
> | Attribute              | Value                                   |
> +------------------------+-----------------------------------------+
> | Name                   | workshops                               |
> | id                     | 906ef2f2-07d0-472c-add6-fe719cf61d02    |
> | Status                 | ACTIVE                                  |
> | Default Cloud Provider | GCP                                     |
> | Default Region         | us-east1                                |
> | Default Keyspace       | better_reads                            |
> | Creation Time          | 2023-02-20T12:06:21Z                    |
> |                        |                                         |
> | Keyspaces              | [0] better_reads                        |
> |                        |                                         |
> | Regions                | [0] us-east1                            |
> +------------------------+-----------------------------------------+
> ```

[🏠 Back to Table of Contents](#-table-of-content)

### 1.6 - Create Schema

- `✅ 1.6.a` **Check tables list leveraging `cqlsh`**

```bash
astra db cqlsh workshops -k better_reads -e "describe tables;"
```

> 🖥️ `output`
>
> ```
> [INFO]  Downloading Cqlshell, please wait...
> [INFO]  Installing  archive, please wait...
> [INFO]  Secure connect bundles have been downloaded.
> [INFO]  Cqlsh is starting, please wait for connection establishment...
> 
> <empty>
> ```


- `✅ 1.6.b` **Create tables**

```bash
astra db cqlsh workshops \
   -k better_reads \
   -f /workspace/workshop-betterreads/dataset/schema-ddl.cql
```

> 🖥️ `output`
>
> ```
> [INFO] Secure connect bundles have been downloaded.
> [INFO] Cqlsh is starting, please wait for connection establishment...
> ```

- `✅ 1.6.c` **List tables**

```bash
astra db cqlsh workshops -k better_reads -e "describe tables;"
```

> 🖥️ `output`
>
> ```
> [INFO] Secure connect bundles have been downloaded.
> [INFO] Cqlsh is starting, please wait for connection establishment...
>
> author_by_id  book_by_id  book_by_user_and_bookid  books_by_user
> ```

[🏠 Back to Table of Contents](#-table-of-content)

### 1.7 - Load Data

- `✅ 1.7.a` **Show content of the CSV File**

```
head -n 10 /workspace/workshop-betterreads/dataset/book_by_id_0.csv 
```

> 🖥️ `output`
>
> ```
> id,author_id,author_names,book_description,book_name,cover_ids,published_date
> OL10000049W,"[\"OL3964979A\"]","[]",,"Le crime organise/quatre films exemplaires","[\"3140091\"]",2009-12-11
> OL10000394W,"[\"OL3965434A\"]","[]",,"Portraits of Illusions","[\"3140733\"]",2009-12-11
> OL10000415W,"[\"OL3965461A\"]","[]",,"Le Berceau du monde","[\"3140790\"]",2009-12-11
> OL10000427W,"[\"OL3965478A\"]","[]",,"La fracture identitaire","[]",2009-12-11
> OL10000471W,"[\"OL3965508A\"]","[]",,"Jamiroquaï de A à Z","[\"3140910\"]",2009-12-11
> OL10001081W,"[\"OL3966201A\"]","[]",,"Contes soufis, tome 1","[\"3142335\"]",2009-12-11
> OL10001150W,"[\"OL3966289A\"]","[]",,"Le prix de la terre","[\"3142514\"]",2009-12-11
> OL10001271W,"[\"OL3966392A\"]","[]",,"Balzac","[\"3142712\"]",2009-12-11
> OL10001538W,"[\"OL3966709A\"]","[]",,"D'affectueuses révérences","[]",2009-12-11
> ```

- `✅ 1.7.b` **Check how many rows. It should have more than 250k**

```
wc -l /workspace/workshop-betterreads/dataset/book_by_id_0.csv
```

> 🖥️ `output`
>
> ```
> 250437 ./dataset/book_by_id_0.csv
> ```

- `✅ 1.7.c` **Populate table `book_by_id` from the csv `book_by_id_0`**

```
astra db load workshops \
     -k better_reads \
     -t book_by_id \
     -maxErrors -1 \
     -url /workspace/workshop-betterreads/dataset/book_by_id_0.csv
```

- The batch is running and should be able to see the throughput at ~3k records per second.

> 🖥️ `output`
>
> ```
> [INFO]  Downloading Dsbulk, please wait...
> [INFO]  Installing  archive, please wait...
> [INFO] Secure connect bundles have been downloaded.
> [INFO] RUNNING: dsbulk load -u token -p xxxxb -b /yyy1.zip -k better_reads -t book_by_id -logDir ./logs --log.verbosity normal --schema.allowMissingFields true -maxConcurrentQueries AUTO -delim , -url ./dataset/book_by_id_0.csv -header true -encoding UTF-8 -skipRecords 0 -maxErrors -1
> [INFO] DSBulk is starting please wait ...
> Username and password provided but auth provider not specified, inferring PlainTextAuthProvider
> A cloud secure connect bundle was provided: ignoring all explicit contact points.
> A cloud secure connect bundle was provided and selected operation performs writes: changing default consistency level to LOCAL_QUORUM.
> ...
>  total | failed | rows/s |  p50ms |  p99ms | p999ms | batches
> 18,944 |      0 |  1,706 | 107.08 | 134.22 | 182.45 |    1.00
> ...
> ```

- The operation should take about 1 minute to complete. The file can have some errors like invalid title with special characters. IT IS NOT A PROBLEM the dataset is not perfect we will have some failed rows.

> 🖥️ `output`
>
> ```
>  total | failed | rows/s | p50ms | p99ms | p999ms | batches
> 250,000 |    183 |  3,684 | 21.44 | 56.10 |  66.32 |    1.00
> Operation LOAD_20220214-185449-001328 completed with 183 > errors in 1 minute and 7 seconds.
> ```

- `✅ 1.7.d` **Populate table `book_by_id` from the csv `book_by_id_1`**

```
astra db load workshops \
     -k better_reads \
     -t book_by_id \
     -maxErrors -1 \
     -url /workspace/workshop-betterreads/dataset/book_by_id_1.csv
```

> 🖥️ `output`
>
> ```
>  total | failed | rows/s |  p50ms |  p99ms | p999ms | batches
> 250,000 |    138 |  1,787 | 106.92 | 136.31 | 398.46 |    1.00
> Operation LOAD_20230220-153154-071483 completed with 138 errors in 2 minutes and 19 seconds.
> ```

- `✅ 1.7.e` **Count Records in the table `book_by_id`**

```
astra db count workshops \
     -k better_reads \
     -t book_by_id
```

> 🖥️ `output`
>
> ```
> Picked up JAVA_TOOL_OPTIONS:  -Xmx2576m
>  total | failed | rows/s |  p50ms |    p99ms |   p999ms
> 499,679 |      0 | 57,806 | 210.15 | 6,207.57 | 6,207.57
> ```

[🏠 Back to Table of Contents](#-table-of-content)

## 2. Application Implementation

### 2.1 - Configuration

- `✅ 2.1.a` **Generate `.env` file**

```
cd /workspace/workshop-betterreads/better-reads-webapp
astra db create-dotenv workshops -k better_reads
cat .env
```

> 🖥️ `output`
>
> _Values have been omitted in this guide for security reason_
> ```
> ASTRA_DB_APPLICATION_TOKEN=...
> ASTRA_DB_GRAPHQL_URL=...
> ASTRA_DB_GRAPHQL_URL_ADMIN=...
> ASTRA_DB_GRAPHQL_URL_PLAYGROUND=...
> ASTRA_DB_GRAPHQL_URL_SCHEMA=...
> ASTRA_DB_ID=...
> ASTRA_DB_KEYSPACE="better_reads"
> ASTRA_DB_REGION="us-east1"
> ASTRA_DB_REST_URL=...
> ASTRA_DB_REST_URL_SWAGGER=...
> ASTRA_DB_SECURE_BUNDLE_PATH=...
> ASTRA_DB_SECURE_BUNDLE_URL=...
> ASTRA_ORG_ID=...
> ASTRA_ORG_NAME=...
> ASTRA_ORG_TOKEN=...
> ```

- `✅ 2.1.b` **Load `.env` as environment variables**

```
set -a
source .env
set +a
env | grep ASTRA_DB_
```

> 🖥️ `output`
>
> _Values have been omitted in this guide for security reason_
> ```
> ASTRA_DB_APPLICATION_TOKEN=...
> ASTRA_DB_GRAPHQL_URL=...
> ASTRA_DB_GRAPHQL_URL_ADMIN=...
> ASTRA_DB_GRAPHQL_URL_PLAYGROUND=...
> ASTRA_DB_GRAPHQL_URL_SCHEMA=...
> ASTRA_DB_ID=...
> ASTRA_DB_KEYSPACE="better_reads"
> ASTRA_DB_REGION="us-east1"
> ASTRA_DB_REST_URL=...
> ASTRA_DB_REST_URL_SWAGGER=...
> ASTRA_DB_SECURE_BUNDLE_PATH=...
> ASTRA_DB_SECURE_BUNDLE_URL=...
> ```


- `✅ 2.1.c` **Open configuration file**

- Open project configuration 

```
gp open /workspace/workshop-betterreads/better-reads-webapp/pom.xml
```

- Locate the declaration of the `spring-boot-starter`

```xml
<dependency>
  <groupId>com.datastax.astra</groupId>
  <artifactId>astra-spring-boot-starter</artifactId>
  <version>${astra-sdk.version}</version>
</dependency>
```

- `✅ 2.1.d` **Study `application.yaml` file**

```
gp open /workspace/workshop-betterreads/better-reads-webapp/src/main/resources/application.yml
```

- Notice how the variables are used

```yaml
astra:
  api:
    application-token: ${ASTRA_ORG_TOKEN}
    database-id: ${ASTRA_DB_ID}
    database-region: ${ASTRA_DB_REGION}
```

- We could have let Spring Data generate the tables for us based on the entities but it is a bad practice

```yaml
spring:
  application:
    name: betterreads
  data:
    cassandra:
      schema-action: create-if-not-exists
```

### 2.2 - Start Application and first use

- `✅ 2.2.a` **Known the URL of the application**

- It would be handy to know the URL of the application

```
gp url 8080
```

- `✅ 2.2.b` **Start the Application**

```
cd /workspace/workshop-betterreads/better-reads-webapp
mvn spring-boot:run
```

> 🖥️ `output`
>
> ```
> BetterReads with Spring Boot, String Data, Spring NVC, Spring security
> An application by JabaBrains.
> The application will start at http://localhost:8080
> 13:37:20.276 INFO  com.datastax.astra.sdk.AstraClient              : Setup of AstraClient from application.yml
> 13:37:20.280 INFO  com.datastax.astra.sdk.config.AstraClientConfig : Initializing [AstraClient]
> 13:37:20.459 INFO  com.datastax.astra.sdk.AstraClient              : + API(s) Devops     [ENABLED]
> 13:37:20.459 INFO  com.datastax.astra.sdk.AstraClient              : + Db: id > [3ed83de7-d97f-4fb6-bf9f-82e9f7eafa23] and region [eu-west-1]
> 13:37:20.460 INFO  com.datastax.astra.sdk.AstraClient              : + Downloading bundles in: [/home/gitpod/.astra]
> 13:37:21.124 INFO  com.datastax.astra.sdk.databases.DatabaseClient : + SecureBundle found : scb_3ed83de7-d97f-4fb6-bf9f-82e9f7eafa23_eu-west-1.zip
> 13:37:21.124 INFO  com.datastax.astra.sdk.databases.DatabaseClient : + SecureBundle found : scb_3ed83de7-d97f-4fb6-bf9f-82e9f7eafa23_eu-central-1.zip
> 13:37:23.041 INFO  com.datastax.astra.sdk.AstraClient              : [AstraClient] has been initialized.
> ```

A new tab should have opened in your browser. You can also open a new terminal and enter the command.

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/new_terminal.png?raw=true)


```
gp preview $(gp url 8080)
```

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/app1.png?raw=true)

- `✅ 2.2.c`- **Show Book details**

In the search item look for `Glimpses of ancient Sowams` you can search to whatever you want it will request open library ut during this workshop you only imported a subset of books, let us pick one you imported.

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/app2.png?raw=true)

Select the first item, if you select the second you will hit the page book not found as this book is not in the DB.

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/app3.png?raw=true)

This is only what we can do at this point. To mark the book as read we will need to authenticate with `Google` or `Github`.

[🏠 Back to Table of Contents](#-table-of-content)

### 2.3 - Setup Authentication for Google

- `✅ 2.3.a` - Connect to [Google Cloud Platform](https://console.cloud.google.com)

- `✅ 2.3.b` - Create a new project if needed, on the screens i put `BetterReadsDemoApps` and click `[CREATE]]`

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/gcp1.png?raw=true)

- `✅ 2.3.c` - Select `Api and Services` on the project home page

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/gcp_welcome.png?raw=true)

- `✅ 2.3.c` - Select `[ENABLE APIS AND SERVICES]` in menu

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/gcp2.png?raw=true)

- `✅ 2.3.d` - Search for `Gmail Apis` and add them to your project.

**Look For API**

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/gmail_2.png?raw=true)

**Select API**

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/gcp3.png?raw=true)

**Output**

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/gmail_3.png?raw=true)

- `✅ 2.3.e` - Search for `Google Analytics Apis` and add them to your project.

**Look For API**

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/googleanalytics_1.png?raw=true)

**Select API**

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/gcp4.png?raw=true)

**Output**

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/googleanalytics_2.png?raw=true)

- `✅ 2.3.f` - Check `External` (or internal as you prefer to limit scope). Then select `CREATE`

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/gcp6.png?raw=true)

- `✅ 2.3.g` - Select `[OAuth consent screen]` in the menu on the left. Provide your application name, a support email and the application logo. Go to the bottom of the page and also provide an email. You can then `[Save and continue]`.

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/gcpoauth1.png?raw=true)


- `✅ 2.3.h` - On menu in the left select *Credentials* and use the button on top `[CREATE CREDENTIALS]`/ OAuth ClientID.

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/gcp7.png?raw=true)

- `✅ 2.3.i` - Select `Web Application` and provide it a name

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/gcp8.png?raw=true)

- `✅ 2.3.j` - For `Authorized JavaScript origins` use the output of :

```
gp url 8080
```

- `✅ 2.3.k` - For `Authorized redirect URIs` use the output  and then `[Create]`

```
echo $(gp url 8080)/login/oauth2/code/google | sed -r  "s/https/http/"
```

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/gcp9.png?raw=true)


- `✅ 2.3.l` - A new page will open with your `clientId` and `client Secret`. Make sure you copy them locally you will need to setup your application with it.

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/gcp10.png?raw=true)

```
You are now doomed we will now mine cryptos with your google account.

Just kidding ^_^
``` 

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/gcp11.png?raw=true)

- `✅ 2.3.m` - Open file `src/main/resources/application.yml` in your project

```
gp open /workspace/workshop-betterreads/better-reads-webapp/src/main/resources/application.yml
```

- `✅ 2.3.n` - Changes keys `client-id` and `client-secret` with your values for the provider `Google`.

```yaml
  security:
    oauth2:
      client:
        registration:
          google:
            client-id: change
            client-secret: change
```

### 2.4 - Setup Authentication for Github

As each attendee has a different URL in gitpod, you will have to create your own github `OAuth Apps - Let's do this together. For github settings we will have to enter a callback URL. To know which one enter use the following command

```
clear
echo $(gp url 8080)/login/oauth2/code/github | sed -r  "s/https/http/" 
```

- `✅ 2.4.a` - Login to your github account and go to `Organizations`

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/githubapps1.png?raw=true)

- `✅ 2.4.b` - There scroll down to locate the last item of the menu `Developer Settings` *(hopefully you have not as many organizations as me)*, There pick `OAuth Apps` (we are using OAuth)

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/githubapps2.png?raw=true)

- `✅ 2.4.c` - Click button `[New OAuth Apps]` on the page

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/githubapps3.png?raw=true)

- `✅ 2.4.d` - You will be asked to login again for security reasons, then fill the form to register a new Github App. Thre Register your application

|Name| Value|
|---|---|
| `Application name`| The application name shown to user |
| `Homepage URL`| Can be anything, just the app (gp url 8080) |
| `Authorization Callback URL`| Call back url the one listed above `${homepage}/login/oauth2/code/github` |

- `✅ 2.4.e` - Click `[Register Application]`

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/githubapps4.png?raw=true)

- `✅ 2.4.f` - The application is created. You got your clientId. You will have to generate a clientSecret now. Once you get both save them on a text file in your machine we will need them later

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/githubapps5.png?raw=true)

- `✅ 2.4.h` - When everything is set you can upload am image for your application and save the change with `[Update Application]`.

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/githubapps6.png?raw=true)
 
- `✅ 2.4.i` - Open file `src/main/resources/application.yml` in your project

```
gp open /workspace/workshop-betterreads/better-reads-webapp/src/main/resources/application.yml
```

- `✅ 2.4.j` - Changes keys `client-id` and `client-secret` with your values for the provider `Github`.

```yaml
  security:
    oauth2:
      client:
        registration:
          github:
            client-id: change
            client-secret: change
```

[🏠 Back to Table of Contents](#-table-of-content)

### 2.5 - Authenticate with Oauth2

- `✅ 2.5.a` - After setting up the connection you can now start the application again :

```
cd /workspace/workshop-betterreads/better-reads-webapp
mvn spring-boot:run
```

#### `✅ 2.5.b` - Authenticate with Github

- On homepage click on `Authenticate with Github`

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/githubapps7.png?raw=true)

- Eventually you get the SSO screen for you organization

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/githubapps8.png?raw=true)

- Then you authorize the application again

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/githubapps9.png?raw=true)

```
HAHAHA EVIL LAUGH 

YOU ARE DOOMED AGAIN WE ALSO HAVE YOUR GITHUB ACCOUNT NOW
WE WILL FEED OUR TROLLS AND CODEX.AI WITH IT.
```

- More seriously, Your are in !

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/githubapps10.png?raw=true)

#### `✅ 2.5.c` Authenticate with Github

- Use the button `[Login via Google]`

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/google1.png?raw=true)

- Validate with the familiar Google Screen

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/google2.png?raw=true)

- You are in !

![new_terminal](https://github.com/datastaxdevs/workshop-betterreads/blob/master/img/google3.png?raw=true)

[🏠 Back to Table of Contents](#-table-of-content)

## Homeworks

<img src="img/badge.png?raw=true" width="200" align="right" />

Don't forget to complete your assignment and get your verified skill badge! Finish and submit your homework!

1. Complete the practice steps as described below until you have your own app running in Gitpod. (up to step 11)
2. Answer the technical questions in the form (We promise, it is NOT difficult if you follow the workshop).
3. Take a screenshot of you authenticated in the app with a few books
4. Submit your homework [here](https://dtsx.io/homework-betterreads)

5. *(totally optional)* Watch the full course on Javabrains.io

- [01 - Introduction to the series](https://www.youtube.com/watch?v=LxVGFBRpEFM)
- [02 - About the app](https://www.youtube.com/watch?v=HAiCwq4jfn8)
- [03 - System Design](https://www.youtube.com/watch?v=SnQXdvFkq4U)
- [04 - Cassandra Schema](https://www.youtube.com/watch?v=106jIBE9XSc)
- [05 - Setting up hosted](https://www.youtube.com/watch?v=waLSHx-VN08)
- [06 - Creating the Data Loader](https://www.youtube.com/watch?v=d28t_QySyzs)
- [07 - Connecting Spring Boot app to DataStax Astra](https://www.youtube.com/watch?v=7I37-awpaGg)
- [08 - Using Repository pattern with Spring Data](https://www.youtube.com/watch?v=uezZIPK8kPk)
- [09 - Saving all the authors in the world to Cassandra](https://www.youtube.com/watch?v=24NrLl8EhDM)
- [10 - Setting up books by ID ](https://www.youtube.com/watch?v=Fm-XrOTgOto)
- [11 - Starting with Spring boot and security](https://www.youtube.com/watch?v=nwyf_4aSkqM)
- [12 - Implementing the Book view flow](https://www.youtube.com/watch?v=-IuafzgS3fU)
- [13 - Building book search feature](https://www.youtube.com/watch?v=6K0im9vcoCk)
- [14 - Tracking user interactions with books](https://www.youtube.com/watch?v=NEZGCpN1J6M)
- [15 - Building the My Books feature](https://www.youtube.com/watch?v=ZIGImCqRr1I)
- [16 - Wrapping Up](https://www.youtube.com/watch?v=hJLtsn2aSr4)

----
