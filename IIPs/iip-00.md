---
iip: 0
title: IPNN base protocol
status: draft
type: required
author: Kayhan Alizadeh <kehiiiiya@gmail.com>
created: 0000-00-00 # after standard status
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

### IPNN P2P protocol

The IPNN P2P protocol is based on [libp2p protocols and specifications](https://docs.libp2p.io/concepts/fundamentals/protocols/).

#### Topics

There are 1 topics in IPNN base protocol:

```
/ipnn/topic/events/v1
```

The `events` topics is for broadcasting new events that each node gets from clients. every one **SHOULD** publish and **MUST** subscribe to this topic. All data in this topic **MUST** be an [IPNN message](#messages).

IPNN nodes can *just* save, backup and maintain some *specific* event kinds and its **OPTIONAL**.

#### Protocols

There is a stream protocol in IPNN like this:

```
/ipnn/stream/v1
```

Every node can make a stream connection with other nodes and send and receive data. they **MUST** be in [IPNN message](#messages) style.

##### Messages

The message in IPNN is defined by IPNN not libp2p.

There is 2 message types in IPNN:

###### Event

Event message will be broadcasted in event topic or sent as query message response. it **MUST** be a valid [Nostr event](https://github.com/nostr-protocol/nips/blob/master/01.md#events-and-signatures) in *json*.

Example:

```json
{
  "id": <32-bytes lowercase hex-encoded sha256 of the serialized event data>,
  "pubkey": <32-bytes lowercase hex-encoded public key of the event creator>,
  "created_at": <unix timestamp in seconds>,
  "kind": <integer between 0 and 65535>,
  "tags": [
    [<arbitrary string>...],
    ...
  ],
  "content": <arbitrary string>,
  "sig": <64-bytes lowercase hex of the signature of the sha256 hash of the serialized event data, which is the same as the "id" field>
}
```

[NIP reference](https://github.com/nostr-protocol/nips/blob/master/01.md#events-and-signatures)

###### Query

Query message **MUST** be a json message like that:

```json
{
  "ids": <a list of event ids>,
  "authors": <a list of lowercase pubkeys, the pubkey of an event must be one of these>,
  "kinds": <a list of a kind numbers>,
  "#<single-letter (a-zA-Z)>": <a list of tag values, for #e — a list of event ids, for #p — a list of event pubkeys etc>,
  "since": <an integer unix timestamp in seconds, events must be newer than this to pass>,
  "until": <an integer unix timestamp in seconds, events must be older than this to pass>,
  "limit": <maximum number of events relays SHOULD return in the initial query>
}
```

[NIP reference](https://github.com/nostr-protocol/nips/blob/master/01.md#from-client-to-relay-sending-events-and-creating-subscriptions)

Receiver node **SHOULD** send one or more Nostr event as answer (more than one event **MUST** be array of events).

##### Error

If a query answer was not successful for any reasons, receiver node **SHOULD** send an `Error` message as response.

```json
{
    "error":"ipnn_error",
    "desc" : "description" // this field is **OPTIONAL**
}
```

Errors List:

- not_found (when an event is not available in a node database)
- not_supported (when a node doesn't support answering to direct queries or doesn't support the requested event kind in its Nostr relay implementation)

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119 and RFC 8174.
