---
iip: 0
title: IPNN base protocol
status: draft
type: required
author: Kayhan Alizadeh <kehiiiiya@gmail.com>
created: 2023-02-12
---

## Abstract

IPNN is an open protocol that allows [Nostr](https://nostr.com) relays to synchronize, query notes from each other, broadcast notes, and more.

## Motivation

In general, Nostr relays won't share notes they receive with each other. Your client may be able to find more relays to find the data you need by using the metadata in notes. IPNN protocol makes these relays interconnected. So, when you publish data to your relay with IPNN implementation, your note will be automatically published and broadcast to many other relays with IPNN implementation as well. Users of those relays will receive your event faster, and if their IPNN nodes were offline in your publish time, it will query it in the network and send it back to you quickly. This interconnection makes things faster, more reliable, more secure, and more.

## Specification

Each IPNN node (implementation) needs to consider following this rules.

### Nostr Improvement Possibilities

At the first step, each IPNN nodes is a Nostr relay. so, IPNN nodes **MUST** have [NIP-01](https://github.com/nostr-protocol/nips/blob/master/01.md) implemented.

> NOTE: the Nostr protocol itself doesn't focused on saving and maintaining events and it's more about communication and transmission of events. but for IPNN nodes, it's **RECOMMENDED** to save and maintain events they receive from clients or other nodes. limiting the space, backup, removing old events or some specific events and more, is **OPTIONAL**.

### Network

All IPNN nodes **MUST** support `tcp` and `udp` transports. supporting `quic` is **RECOMMENDED**.

Port `37771`  for network is **RECOMMENDED**.

### IPNN P2P protocol

The IPNN P2P protocol is based on [libp2p protocols and specifications](ipns://docs.libp2p.io/concepts/fundamentals/protocols/).

#### Topics

There are 2 topics in IPNN base protocol:

```
/ipnn/topic/events/v1
```

The `events` topics is for broadcasting new events that each node gets from clients. every one **SHOULD** publish and **MUST** subscribe to this topic. All data in this topic **MUST** be an IPNN message.

```
/ipnn/topic/profiles/v1
```

The `profiles` topics is for broadcasting new profile and users a relay finds. each node **SHOULD** gossip new profiles in profiles topic. All data in this topic **MUST** be an IPNN message.

#### Protocols

There is a stream protocol in IPNN like this:

```
/ipnn/stream/v1
```

Every node can make a stream connection with other nodes and send and receive data. they **MUST** be in IPNN messages style.

##### Messages

The message in IPNN is defined by IPNN not libp2p.

There is 2 message types in IPNN:

###### Event

Event message will be broadcasted in event topic or sent as query message response. it **MUST** be a valid Nostr event in *json*.

This message is a event message when a some event is not found:

```json
{
    "error":"not_found"
}
```

###### Profile

Profile message **MUST** contain a Nostr profile details in *json*.

This message is a profile message when a profile is not found:

```json
{
    "error":"not_found"
}
```

###### Query

Query message **MUST** be a json message like that:

```json
{
    "type" : "profile" | "event",
    "id" | "public_key" : "..."
}
```

Receivier node **SHOULD** send a event message or profile message as answer.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119 and RFC 8174.
