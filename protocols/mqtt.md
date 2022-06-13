# 1 - Basic Concepts


## 1.1 What is MQTT
**Message Queue Telemetry Transport**

MQTT is a lightweight publish/subscribe messaging protocol designed for M2M(Machine to Machine) telemetry in low bandwidth environments.

It was design by Andy Standfor-Clak(IBM) and Arlen Nipper in 1999 for coonnecting Oil Pipeline telemetry systems over satellite.

Although it started live as propietary protocol it was released Royalty free in 2010 and become an OASIS standard in 2014.

## 1.2 MQTT Versions

The original **MQTT** which was designed in 1999 and had been used for many years. It was designed for TCP/IP networks.

**MQTT-SN** which was specified in around 2013, and designed to work over UDP, ZigBee and other transport.

## 1.3 How MQTT Works

[Client - Publiser] --(Publish on topic vehicle/vin/remoteDoorLock)--> [Central Broker] --(Subscribed on topic vehicle/vin/remoteDoorLock)--> [client - Subscriber]

## 1.4 What Happens to Published Messages

Publish -> Distribute

*If no clients have subscribed to the topic or they aren't currently connected then the message is immediately removed from the broker.*

In general, **the broker does not store messages.**
*Note: Retained messages, persistent connections and QoS levels can result in messages being temporarily stored on the broker/server.*

## 1.5 MQTT QoS Levels

- QoS0
- QoS1 at least once
- QoS2 at most once

## 1.6 MQTT Broker or servers

*Note: The original term was **broker** but it has now been standardized as **server**. We can see both terms used.*

- Mosuitto - Open Source
- HiveMQ - Commercial

For testing: iot.eclipse.org 1883 or 8883(SSL)


## 1.6 Important Points to Notes

1. Clients do not have addresses like in email systems, and messages are not sent to clients.
2. Messages are published to a broker on a topic.
3. The job of an MQTT broker is to filter messages based on topic, and then distribute them to subscribers.
3. A client can receive these messages by subscribing to that topic on the same broker
4. There is no direct connection between a publisher and subscriber.
5. All clients can publish (broadcast) and subscribe (receive).
MQTT brokers do not normally store messages.




























