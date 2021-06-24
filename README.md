# python-avro-producer



### Setup
```

cd python-avro-producer

virtualenv ./venv


source ./venv/bin/activate

pip install -r requirements.txt

```

### Send Records

- Ensure kafka and schema registery is running.

```

python send_record.py --topic notificationsWebhooks --schema-file webhook-event.avsc --record-value  '{ "eventId": "23123", "origin": "TWILIO" ,"parameters": { "conversationSid": "externalConversationId", "eventType": "onDeliveryUpdated", "participantSid": "externalConversationId", "messageSid": "externalMessageId", "status": "sent" } }'

```


### Verify message sent

Now, open your browser and go to http://localhost:9021, which is the address of the Confluent Control Center. Then, navigate to the topic create-user-request and go to offset 0. 



### Ref
For a tutorial on how this repository was built and how it works, go to this [article](https://medium.com/@billydharmawan/avro-producer-with-python-and-confluent-kafka-library-4a1a2ed91a24?source=friends_link&sk=b845dae5da1761d3a8c8f53d610eac33) (for Avro Producer part) and [this](https://medium.com/@billydharmawan/consume-messages-from-kafka-topic-using-python-and-avro-consumer-eda5aad64230?source=friends_link&sk=9d64b23845664a41710856270d81f36a) (for Avro Consumer part).