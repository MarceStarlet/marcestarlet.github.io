+++
title = "MQTT - Concepts & Usage" 
tags = ["mqtt", "IoT", "protocols", "communication"] 
categories = ["development","IoT", "messaging"] 
date = "2016-04-20" 
+++

## MQTT - Concepts & Usage

The last part of this serie of posts about MQTT will cover some concepts about the protocol that essentialy will show us the boundaries of the protocol and how it handles the connections between clients and the broker.

### Connection
             
Let's start by defining the **MQTT Connection**. The connection initiates when a client sends a *CONNECT* message to the broker, then the broker responds with a *CONNACK* and a status code.

<p align="center">
  <img src="/img/Connection.png" alt="MQTT Connection"/>
</p>
               
Once the connections is established the broker will keep the connection until the client send a disconnect command or it losses the connection.
            
The **CONNECT** message include some information relative to an implementer of a MQTT library than the users that will use the library, here I'll present to you the basic information relevant for the users.

* **clientId**                                          
  The *clientId* is an identifier for each MQTT Client, this means that should be unique for each client connected to the broker indicating that it must keep the state for that client. Since MQTT version 3.1.1, it is possible to connect without a clientId so the broker won't keep the state.
  If you use clientId you should set cleanSession to true, otherwise the connection will be refused.
* **cleanSession**                                       
  The *cleanSession* flag indicates to the broker whether the client wants to establish a persistent session or not. If cleanSession is set to false, it means that the broker will stores all the subscriptions of the client as well as all the messages that do not arrived to the client as long as the QoS has been defined as 1 o 2. If cleanSession is set to true, the broker won't store anything for the client, non the subscriptions neither the missed messages.
* **username/password** (optional)                                   
  The *username* and *password* are used for authentication and authorization. It is recommended to encrypt the password. 
* **keepAlive**                                 
  The *keepAlive* is a time interval, the clients commits to by sending regular PING Request messages to the broker. The broker response with PING Response and this mechanism will allow both sides to determine if the other one is still alive and reachable.

When the broker obtains the CONNECT it responds with a **CONNACK** message that only contains two data entries.

* **sessionPresent**                                    
  This flag indicates to the client wheter the broker has a persistent session or not. If the client in a previous connection set the cleanSession to false then this flag is true, otherwise is false.
* **returnCode**                                                     
  This flags lets the client know if the connection attemp was successfull or not, and if not, it indicates what the issue is.

### Publish
The publish action allows a client to send messages to a topic destination in different modes, but always with a payload, and due MQTT is a data agnostic, you can set to the payload the *data* you want for the case you need. The publish message have some attributes, listed bellow the most important:

* **Topic Name**, the name of the topic destination to publish in the broker
* **QoS**, the "Quality of Service" in which you want to send a message. It is used to define the 
  guarantee of a message. The possible values are 0, 1 or 2. See more about the QoS in the next section.
* **Retain Flag**, this flag instructs the broker to retain the *last* message sent for those new subscribers in order to receive the retained message in a new conenction to the broker. This could be usefull if you have a notification for new subscribers.
* **Payload**, is the content of the message. As commented before MQTT is data agnostic so you can send any kind of message (image, binary, text).
* **Packed ID**, is a unique identifier between the client and brokre that identifies the message during the message flow.
* **Dup Flag**, indicates that a message is duplicate because the last message sent was not acknowledged, so the message will be resent. This flag is taking in account when QoS 1 or 2.

Each publisher is responsible of the send of the message to the broker, once the broker receives the message it is now responsible to publish the message to the subscribers.

<p align="center">
  <img src="/img/Publish.png" alt="Publish"/>
</p>

Here the code of a MQTT Client - Publisher using the Paho API

	try {
		// set default memory persistence in case QoS is 1 or 2
		MemoryPersistence persistence = new MemoryPersistence();
		// create new MQTT Client using URI, CLientID and persistence
		MqttClient samplePublisher = new MqttClient(getUri(), getClientId(), persistence);
		// create MQTT Options to set the connection attributes
		MqttConnectOptions options = new MqttConnectOptions();
		// default cleanSession is set to true to indicate the broker to don't keep session
		// change to false if you want the broke keep a session
		options.setCleanSession(true);
		logger.info("Connecting to: {}", getUri());
		// establish a connection 
		// a CONNECT is sent and the broker should respond with a CONNACK
		samplePublisher.connect(options);
		
		// create new MQTT message
		MqttMessage message = new MqttMessage();
		// the payload is the content of a message 
		message.setPayload(getPayload().getBytes());
		logger.info("Publishing message {} to {} topic", getPayload(), getTopic());
		// publish the message to the Topic indicated
		samplePublisher.publish(getTopic(), message);
		logger.info("Message sent, disconnecting client");
		// disconnect
		samplePublisher.disconnect();
		
	} catch (MqttException e) {
		// handle exception
		logger.error("reason ", e.getReasonCode());
		logger.error("msg ", e.getMessage());
		logger.error("loc ", e.getLocalizedMessage());
		logger.error("cause ", e.getCause());
		logger.error("excep ", e);
		logger.error("trace", (Object[])e.getStackTrace());
	}
