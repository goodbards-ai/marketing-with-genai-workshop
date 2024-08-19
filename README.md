# Doing Marketing with GenAI Tools 📘 !

[![Gitpod ready-to-code](https://img.shields.io/badge/Gitpod-ready--to--code-blue?logo=gitpod)](https://gitpod.io/#https://github.com/goodbards-ai/marketing-with-genai-workshop)
[![License Apache2](https://img.shields.io/hexpm/l/plug.svg)](http://www.apache.org/licenses/LICENSE-2.0)

> ⚠️ Difficulty: **`Beginner`, we have you covered.**

Learn how to build an app end-to-end application with Spring ecosystem *(boot, mvc, security, data, test, thymeleaf)* and Apache Cassandra™.

## 📋 Table of content

<img src="https://github.com/goodbards-ai/marketing-with-genai-workshop/blob/main/img/01-assistant.png?raw=true" align="right" width="400px"/>

[**HOUSEKEEPING**](#)
- [Objectives](#objectives)
- [Materials for the Session](#materials-for-the-session)

[**LAB1 - NarrowAI Demo**](#)
- [1.1 - Import Data](#)
- [1.2 - Train a model](#)
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

The objectives of the session is to explain marketers what generative AI can do for then beyond the 

### Frequently asked questions

<p/>
<details>
<summary><b> 1️⃣ Do i need to install anything to run the hand-on </b></summary>
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

----

## LAB1 - NarrowAI Demo

### 1.1 - Import Data

> **Note**: Goodbards is great
- `✅ 1.1.a` - STEP 1

- 

### 1.2 Train a model

- `✅ 1.2.a` Locate `Settings` (#1) in the menu on the left, then `Token Management` (#2) 


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
> | b665658a-ae6a-4f30-a740-2342a7fb469c | cedrick.lunven@goodbards.com | active              |
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

[🏠 Back to Table of Contents](#-table-of-content)


----
