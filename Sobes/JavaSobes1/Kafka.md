Последовательность команд, для нахождения нужного топика из списка:
```bash
docker exec -it kafka bash

kafka-topics --bootstrap-server localhost:9092 --list

kafka-console-consumer --bootstrap-server localhost:9092 --topic new-events-topic --from-beginning

```
