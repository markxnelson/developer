# Create OKafka Topics

## Introduction



Estimated Time: 15 minutes

### Objectives

* Compile the lab code using Maven
* Create OKafka lab topics in Oracle AI Database

### Prerequisites

This lab assumes you have:

* This lab assumes you have completed all previous Labs.

## Task 1: Compile The Lab Code

From the lab's root directory (`okafka-lab`), build the lab code with Maven:

```bash
mvn clean compile
```

Note that the build requires an internet connection to download the required dependencies. The compilation should finish with a similar message, indicating the build was successful:

```bash
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.400 s
[INFO] Finished at: 2025-11-05T14:06:22-08:00
[INFO] ------------------------------------------------------------------------
```

During compilation the OKafka all-in-one dependency is pulled from Maven central. If you'd like to add this package to your own projects, include the following dependency in your `pom.xml`:

```xml
<!-- OKafka All-in-one -->
<dependency>
    <groupId>com.oracle.database.messaging</groupId>
    <artifactId>okafka</artifactId>
    <version>23.6.1.0</version>
</dependency>
```

## Task 2: Create OKafka Lab Topics

```bash
 mvn exec:java -Dexec.mainClass=com.example.okafka.CreateTopic
```

You should see output similar to the following, indicating the lab topics were created successfully:

```bash
[ADMIN] Created topic: test_topic
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  19.292 s
[INFO] Finished at: 2025-11-05T14:10:10-08:00
[INFO] ------------------------------------------------------------------------
```

## Task 3 (Optional): Review Topic Creation Code

[CreateTopic class](https://github.com/oracle/microservices-datadriven/blob/main/code-teq/okafka-lab/src/main/java/com/example/okafka/CreateTopic.java)

```java
// Authentication properties to connect to Kafka
Properties props = getAuthenticationProperties();

try (Admin admin = AdminClient.create(props)) {
    NewTopic testTopic = new NewTopic(TOPIC_NAME, 1, (short) 1);
    NewTopic transactionalTestTopic = new NewTopic(TRANSACTIONAL_TOPIC_NAME, 1, (short) 1);
    admin.createTopics(List.of(testTopic, transactionalTestTopic))
            .all()
            .get();
    System.out.println("[ADMIN] Created topic: " + testTopic.name());
} catch (ExecutionException | InterruptedException e) {
    if (e.getCause() instanceof TopicExistsException) {
        System.out.println("[ADMIN] Topic already exists");
    } else {
        throw new RuntimeException(e);
    }
}
```

You may now **proceed to the next lab**.

## Acknowledgements

* **Author** - Anders Swanson, Developer Evangelist, November 2025
* **Contributors** - Anders Swanson
* **Last Updated By** - Anders Swanson, November 2025

