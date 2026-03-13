# Kafka Local Setup Quick Reference (Homebrew + KRaft)

This README contains the basic commands needed to start Kafka locally, verify it is running, and create/test topics. Useful for quick reference during development.

---

# 1. Check if Kafka is Installed (Homebrew)

```bash
brew info kafka
```

This shows where Kafka is installed. Typical config locations:

Apple Silicon (M1/M2/M3):

```
/opt/homebrew/etc/kafka/
```

Intel Mac:

```
/usr/local/etc/kafka/
```

---

# 2. Start Kafka (Recommended Way)

Start Kafka using Homebrew services:

```bash
brew services start kafka
```

Check if service is running:

```bash
brew services list
```

---

# 3. Start Kafka Manually (Alternative)

If starting manually:

```bash
kafka-server-start /opt/homebrew/etc/kafka/server.properties
```

or

```bash
kafka-server-start /usr/local/etc/kafka/server.properties
```

---

# 4. Verify Kafka is Running

Use the Java process status command:

```bash
jps
```

Example output:

```
1234 Kafka
3810 Jps
```

If Kafka is running you will see `Kafka` in the list.

---

# 5. Alternative Check (Port Check)

Check if Kafka is listening on port 9092:

```bash
lsof -i :9092
```

Expected output includes a process listening on port `9092`.

---

# 6. Create a Topic

```bash
kafka-topics --bootstrap-server localhost:9092 --create --topic first_topic
```

---

# 7. List Topics

```bash
kafka-topics --bootstrap-server localhost:9092 --list
```

---

# 8. Produce Messages to Topic

```bash
kafka-console-producer --bootstrap-server localhost:9092 --topic first_topic
```

Then type messages:

```
hello
test message
kafka event
```

---

# 9. Consume Messages from Topic

```bash
kafka-console-consumer --bootstrap-server localhost:9092 --topic first_topic --from-beginning
```

This reads all messages from the beginning of the topic.

---

# 10. Common Error

### Error

```
Connection to node -1 (localhost:9092) could not be established
```

### Cause

Kafka broker is **not running**.

### Fix

Start Kafka:

```bash
brew services start kafka
```

---

# 11. Useful Debug Commands

Check Java processes:

```bash
jps
```

Check Kafka port:

```bash
lsof -i :9092
```

Check running brew services:

```bash
brew services list
```

---

# Quick Workflow

1. Start Kafka

```
brew services start kafka
```

2. Verify Kafka

```
jps
```

3. Create topic

```
kafka-topics --bootstrap-server localhost:9092 --create --topic first_topic
```
