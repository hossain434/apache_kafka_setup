#### These are the steps I followed to run kafka on Windows

1. Install Zookeeper first (zookeeper-X.X.X.tar.gz). Make sure download latest version.

2. Extract Zookeeper (and place it to C:/kafka drive) and run this command in powershell/cmd \zookeeper-3.3.6\bin> .\zkServer.cmd Now this should up a Zookeeper instance on localhost:2181

3. Download Kafka binary version (kafka_X.X.X.X.tgz). Make sure download latest version.

4. Extract Kafka, time to modify some configs. for simplicity re-name the kafka_2.10-0.10.0.1 to just kafka and place it to C:/kafka drive.

5. Inside Kafka extraction you can find .\config\server.properties. In .\config\server.properties replace log.dirs=c:/kafka/kafka-logs.Note: Make sure to create those folders in relevant paths.

6. In \zookeeper-3.3.6\conf folder, rename the file to zoo.cfg.

6. Happy news: Kafka ships with windows .bat scripts, You can find these files inside ./bin/windows folder.

7. Start powershell/cmd and run this command to start Kafka broker, C:\kafka\kafka>.\bin\windows\kafka-server-start.bat .\config\server.properties. If this is doesn't work then close Zookeeper and Kafka cmd window and reopen it again.

8. DONE!, Now you have a running Zookeeper instance and a Kafka broker.

9. Create topic:
C:\kafka\kafka\bin\windows>kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic hello_world

10. Now, ask Zookeeper to list available topics on Apache Kafka by running the following command:
C:\kafka\kafka\bin\windows>kafka-topics --list --zookeeper localhost:2181

11. Now, publish a sample messages to Apache Kafka topic called "hello_world" by using the following producer command:
C:\kafka\kafka\bin\windows>kafka-console-producer --broker-list localhost:9092 --topic hello_world

After running above command, enter some messages like "Hi how are you?" press enter, then enter another message like "Where are you?"

12. Now, use consumer command to check for messages on Apache Kafka Topic called "hello_world" by running the following command:

C:\kafka\kafka\bin\windows>kafka-console-consumer --bootstrap-server localhost:9092 --topic hello --from-beginning

You should see the following output:

Hi how are you?
Where are you?

#### Run on Maven project.
Follow the steps #1 to #8 on above.

Run Producer.java

Run Consumer.java

Run AssignSeekConsumer.java

Reference: https://medium.com/better-programming/an-introduction-to-apache-kafka-95a82260c1c3
