# Kafka messaging 📨

The project uses Apache Kafka for messaging transaction data, and Apache Spark is used to process transaction data and calculate cashback.

## Deploy ⚡

To run the project, you need to clone the repository

```bash
  git clone https://github.com/vitor-pelicer/Kafka-messaging
```

Start containers with docker

```bash
  docker compose up
```

You may consider using the docker GUI interface to make it easier to use the terminal, but in any case I am showing how to use the project with just the CLI.

open the zookeeper container terminal

```bash
  docker exec -it zookeeper bash
```

Creating input topic

```bash
  kafka-topics --create --bootstrap-server kafka:9092 --replication-factor 1 --partitions 1 --topics input
```

Creating output topic

```bash
  kafka-topics --create --bootstrap-server kafka:9092 --replication-factor 1 --partitions 1 --topics output
```

Create a producer for the input topic

```bash
  kafka-console-producer --bootstrap-server kafka:9092 --topic input
```

Create a consumer for the output topic

```bash
  kafka-console-consumer --bootstrap-server kafka:9092 --topic output
```

open the jupyter container terminal

```bash
  docker exec -it jupyter bash
```

Open jupyter interface at http://localhost:8888/

Open the notebook "stream_processer.ipynb" and run the code cells

insert a valid message into the producer console of the topic input

Examples

```bash
  {"transaction_id": "1", "customer_id": "123", "amount": 20, "transaction_timestamp": "2023-04-21T09:30:00Z", "merchant_id": "MerchantX"}
```

```bash
  {"transaction_id": "2", "customer_id": "123", "amount": 20, "transaction_timestamp": "2023-04-21T09:30:00Z", "merchant_id": "MerchantY"}
```

The processed result should appear on the consumer terminal of the output topic.
