+++
categories = ["messaging", "java"]
date = "2016-04-17T18:51:49-05:00"
tags = ["messaging", "java", "JMS", "JMS Patterns"]
title = "Messaging Systems"

+++

# What "Messaging System" means?

The Messaging Systems exist since some years ago but they're not so popular as other kind of systems. 

A Messaging is usually use in an enterprise environment. An enterprise has many different applications working independently that have been built using different languages and platforms, if the enterprise needs to communicate them by sharing data and process in a diligent way, **How the enterprise can do this?**
                   
**Using Messaging**

Messaging allows the enterprise to share data from applications that have been built in different platforms and uses different kind of data by transforming the data in a common customized or not customized format and transferring the packed data between the applications. In a reliably, asynchronously, frequent and immediate transfer way, a Messaging System improves the enterprise communication.

Messaging makes applications loosely coupled and with an asynchronous sending, the applications do not need to be running at the same time in ordert to transfer data, so this does the enterprise more reliable. Messaging delegtes "***messagging systems***" the responsibility of transfer the data between applications, so the applications do not need to worry about how the data is transfered but they worry about what data shold be transfer.
                                 
<p align="center">
  <img src="/img/Messaging.png" alt="Messaging"/>
</p>
                               
In order to transfer the data from different applications an EMS is needed. An **EMS** (Enterprise Messaging System) is a set of published enterprise-wide standards that allows organizations to send semantically precise messages between computer systems. EMS systems promote loosely coupled architectures that allow changes in the formats of messages to have minimum impact on message subscribers. EMS systems are facilitated by the use of structured messages (such as using XML or JSON), and appropriate protocols, such as DDS, MSMQ, AMQP or SOAP with web services.

So at the end, a MOM (Message-Oriented Middleware) software solution is required to support sending and receiving messages in distributed systems. This software is specialized about communication, a MOM provides transforming, standardized protocols, communication routes (channels, pipes, etc.), a Message broker, and the APIs required to connect with.
                               
A robust MOM it is not always necessary, so far for many of the current systems that pretend to be simple but powerful, an answer to the new lightweight demands a ***Message Broker*** it is enough to cover the message communication for the enterprise.

A *Message Broker* is an intermediary program module that translates a message from the formal messaging protocol of the sender to the formal messaging protocol of the receiver. A message broker is an architectural pattern for message validation, transformation and routing.[1] It mediates communication amongst applications, minimizing the mutual awareness that applications should have of each other in order to be able to exchange messages, effectively implementing decoupling.
                                 
The purpose of a broker is to take incoming messages from applications and perform some action on them. The following are examples of actions that might be taken in by the broker:
                                 
* Route messages to one or more of many destinations
* Transform messages to an alternative representation
* Perform message aggregation, decomposing messages into multiple messages and sending them to their destination, then recomposing the responses into one message to return to the user
* Interact with an external repository to augment a message or store it
* Invoke Web services to retrieve data
* Respond to events or errors
* Provide content and topic-based message routing using the publish–subscribe pattern                        
                          

<p align="center">
  <img src="/img/MessageBroker.png" alt="Message Broker"/>
</p>
                                
These are some of the most popular Message Brokers: Apache ActiveMQ, RabbitMQ, HiveMQ, Apache Kafka.

[ActiveMQ Message Broker example code](https://goo.gl/hQenrh "MarceStarlet Github - EmbeddedBroker")

### Where a Messaging Systems should be used?
                   
As many of the systems and software solutions you can't apply the Messaging System anywhere, but there are some specific scenarios where it should be use in order to improve the communication. The Messaging Systems should be used:

* In an enterprise that necessary require a reliable communication between applications.
* In distributed systems that wants to communicate data from different endpoints.
* When have different applications that only must to be worried about what data will be transferred and don't care how it is transferred.
              
Some examples where a Messaging System is used: Apache TomEE, Eclipse, Whatsapp, etc.                                                         

 

           
