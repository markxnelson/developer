# Get started - Oracle AI Database on Oracle Cloud Infrastructure (OCI)

## Introduction

Set up a mTLS connection for Oracle Autonomous AI Database and OKafka.

Estimated Time: 15 minutes

### Objectives

* Download your Oracle Autonomous AI Database Wallet
* Configure the Database Wallet for OKafka
* Configure your OKafka environment to connect to Oracle Autonomous AI Database

### Prerequisites

This lab assumes you have:

* 

## Task 1: Download the Oracle Autonomous AI Database Wallet

## Task 2: Configure The Wallet For OKafka

In the downloaded wallet, configure the database password, and keystore/truststore passwords:

`ojdbc.properties`:
```properties
<copy>
user = okafkauser
password = <your database user password
# Connection property while using Oracle wallets.
oracle.net.wallet_location=(SOURCE=(METHOD=FILE)(METHOD_DATA=(DIRECTORY=${TNS_ADMIN})))
# Set the correct password for both trustStorePassword and keyStorePassword.
# It's the password you specified when downloading the wallet from OCI Console or the Service Console.
javax.net.ssl.trustStore=${TNS_ADMIN}/truststore.jks
javax.net.ssl.trustStorePassword=<your keystore/truststore password>
javax.net.ssl.keyStore=${TNS_ADMIN}/keystore.jks
javax.net.ssl.keyStorePassword=<your keystore/truststore password>
</copy>
```

Make sure you have these environment variables set anywhere you run the OKafka sample app, as they are used for database connection to your Autonomous Database instance.

## Task 3: Clone The Lab Code

run the following command to checkout the lab code from GitHub:

```bash
<copy>
git clone --filter=blob:none --no-checkout https://github.com/oracle/microservices-datadriven.git
cd microservices-datadriven
git sparse-checkout init --cone
git sparse-checkout set code-teq/okafka-lab
git checkout main
</copy>
```

## Task 4: Set Environment Variables For OKafka

The sample application uses specific environment variables to configure the OKafka database connection.

Set the following environment variables using your database TNS alias and the path where you downloaded your database wallet:

```bash
<copy>
export TNS_ADMIN=<Database TNS Alias>
export WALLET_DIR=<Path to downloaded wallet>
export SECURITY_PROTOCOL="SSL"
</copy>
```

You may also view the lab code here: [OKafka Lab](https://github.com/oracle/microservices-datadriven/tree/main/code-teq/okafka-lab)

You may now **proceed to the next lab**.

## Acknowledgements

* **Author** - Anders Swanson, Developer Evangelist, November 2025
* **Contributors** - Anders Swanson
* **Last Updated By** - Anders Swanson, November 2025
