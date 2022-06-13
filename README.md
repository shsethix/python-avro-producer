# python-avro-producer



### Setup
```

cd python-avro-producer

virtualenv ./venv

// python3 -m pip install --user virtualenv

source ./venv/bin/activate

python3 -m pip install -r requirements.txt

```

### Send Records

- Ensure kafka and schema registery is running.

### Send Records to outbound

```
python send_record.py --topic notificationsOutboundMessages --schema-subject-name com.compass.notification.events.sms.outbound.v1.NotificationsOutboundMessage --record-value  '{"userId": null, "fromPhoneNumber": null, "eventId": "23124", "partnerMessageId": "1000001", "toPhoneNumber": "+1123456789", "productId": 1, "attachments": null, "externalConversationId": null, "chatServiceSid": null, "body": null }'

```
#### Register Outbound messanger

```
curl --location --request POST 'http://localhost:8081/subjects/com.compass.notification.events.sms.outbound.v1.NotificationsOutboundMessage/versions' \
--header 'Content-Type: application/json' \
--data-raw '{
 "schema": "{\"type\": \"record\", \"namespace\": \"com.compass.notification.events.sms.outbound.v1\", \"name\": \"NotificationsOutboundMessage\", \"fields\": [{\"default\": null, \"type\": [\"null\", {\"type\": \"string\", \"avro.java.string\": \"String\"} ], \"name\": \"eventId\"}, {\"type\": {\"type\": \"string\", \"avro.java.string\": \"String\"}, \"name\": \"partnerMessageId\"}, {\"default\": null, \"type\": [\"null\", {\"type\": \"string\", \"avro.java.string\": \"String\"} ], \"name\": \"fromPhoneNumber\"}, {\"default\": null, \"type\": [\"null\", {\"type\": \"string\", \"avro.java.string\": \"String\"} ], \"name\": \"toPhoneNumber\"}, {\"default\": null, \"type\": [\"null\", {\"type\": \"string\", \"avro.java.string\": \"String\"} ], \"name\": \"body\"}, {\"default\": null, \"type\": [\"null\", {\"items\": {\"type\": \"string\", \"avro.java.string\": \"String\"}, \"type\": \"array\"} ], \"name\": \"attachments\"}, {\"default\": null, \"type\": [\"null\", {\"type\": \"string\", \"avro.java.string\": \"String\"} ], \"name\": \"externalConversationId\"}, {\"default\": null, \"type\": [\"null\", {\"type\": \"string\", \"avro.java.string\": \"String\"} ], \"name\": \"chatServiceSid\"}, {\"type\": \"int\", \"name\": \"productId\"}, {\"default\": null, \"type\": [\"null\", {\"type\": \"string\", \"avro.java.string\": \"String\"} ], \"name\": \"userId\"} ] }"
}'

```

### Verify message sent

Now, open your browser and go to http://localhost:9021, which is the address of the Confluent Control Center. Then, navigate to the topic create-user-request and go to offset 0. 



### Ref
For a tutorial on how this repository was built and how it works, go to this [article](https://medium.com/@billydharmawan/avro-producer-with-python-and-confluent-kafka-library-4a1a2ed91a24?source=friends_link&sk=b845dae5da1761d3a8c8f53d610eac33) (for Avro Producer part) and [this](https://medium.com/@billydharmawan/consume-messages-from-kafka-topic-using-python-and-avro-consumer-eda5aad64230?source=friends_link&sk=9d64b23845664a41710856270d81f36a) (for Avro Consumer part).