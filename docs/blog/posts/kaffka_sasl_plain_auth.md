# How to Enable SASL/PLAIN Authentication in Apache Kafka

This document outlines the steps required to enable SASL/PLAIN authentication in Apache Kafka, a popular distributed event streaming platform. SASL/PLAIN uses a simple username and password mechanism for authentication, which is suitable for environments where SSL/TLS is used to encrypt connections.

**Prerequisites:**

- Apache Kafka installed and running
- Basic knowledge of Kafka configuration and administration
- Access to the Kafka and Zookeeper configuration files 

### Step 1: Configure Kafka for SASL/PLAIN

1. **Edit Kafka’s `server.properties` file** to enable SASL/PLAIN. Add or modify the following properties:

    You will find this file in your Kafka directory:

    `/home/ubuntu/kafka/config/server.properties`

    ```properties
    # Enable SASL_PLAINTEXT or SASL_SSL if encryption is needed
    listeners=SASL_PLAINTEXT://localhost:9092
    # Specify the SASL mechanism
    sasl.mechanism.inter.broker.protocol=PLAIN
    sasl.enabled.mechanisms=PLAIN
    # Specify JAAS configuration file
    security.inter.broker.protocol=SASL_PLAINTEXT
    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \
    username="admin" \
    password="admin-secret" \
    user_admin="admin-secret" \
    user_kafka="kafka-secret";
    ```

    - Replace `localhost` with the IP or endpoint where Kafka is hosted.
    - Replace `admin-secret` and `kafka-secret` with your actual passwords.
    - If you're using SASL_SSL for encrypted communication, make sure to also configure the SSL settings.

2. **Create or update the JAAS configuration file** if you prefer not to include credentials directly in `server.properties`. Kafka will use this file to authenticate users.

    Create a file named `kafka_server_jaas.conf` with the following content:

    ```properties
    KafkaServer {
      org.apache.kafka.common.security.plain.PlainLoginModule required
      username="admin"
      password="admin-secret"
      user_admin="admin-secret"
      user_kafka="kafka-secret";
    };
    ```

    Then, point to this file by setting the `KAFKA_OPTS` environment variable:

    ```bash
    export KAFKA_OPTS="-Djava.security.auth.login.config=/path/to/kafka_server_jaas.conf"
    ```

### Step 3: Configure Kafka Clients

Ensure your Kafka clients are configured to use SASL/PLAIN authentication:

1. **For producer and consumer clients**, include the following properties in their configuration:

    You will find consumer and producer config files at: `/home/ubuntu/kafka/config/`

    Add the following lines to `consumer.properties` and `producer.properties`:

    ```properties
    security.protocol=SASL_PLAINTEXT
    sasl.mechanism=PLAIN
    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required \
    username="kafka" \
    password="kafka-secret";
    ```

    - Adjust the `security.protocol` as necessary if using encryption (e.g., `SASL_SSL`).

### Step 4: Restart Kafka and Zookeeper

After configuring SASL/PLAIN authentication, restart your Kafka and Zookeeper instances to apply the changes.

Run Zookeeper:

    bin/zookeeper-server-start.sh config/zookeeper.properties

Run Kafka server:

    bin/kafka-server-start.sh config/server.properties

Run the Producer:

    bin/kafka-console-producer.sh --bootstrap-server {host.ip}:9092 --topic testes --producer.config /home/ubuntu/kafka/config/producer.properties

Run the Consumer:

    bin/kafka-console-consumer.sh --bootstrap-server {host.ip}:9092 --topic testes --consumer.config /home/ubuntu/kafka/config/consumer.properties
    
### Step 5: Testing

Test your setup by producing and consuming messages with a client configured to use SASL/PLAIN authentication. If the client can produce and consume messages without errors, SASL/PLAIN authentication is working correctly.

### Troubleshooting

- **Authentication errors**: Check the Kafka and Zookeeper log files for authentication errors. Ensure that usernames and passwords match between the JAAS configuration files and client configurations.
- **Connection issues**: Verify that the correct ports are open and accessible between Kafka clients and the Kafka cluster.
- **Configuration mistakes**: Double-check all configuration files for typos or incorrect settings.

### Conclusion

Enabling SASL/PLAIN authentication in Apache Kafka adds a layer of security by requiring clients to authenticate using usernames and passwords. This guide has walked you through configuring SASL/PLAIN for both Kafka brokers and clients, as well as optional Zookeeper configuration if needed. Remember, SASL/PLAIN should be used in conjunction with SSL/TLS to ensure that credentials are not transmitted in clear text over the network.