---
iip: 0
title: IPNN base protocol
status: draft
type: required
author: Kayhan Alizadeh <kehiiiiya@gmail.com>
created: 2023-07-10
---

## Abstract

IPNN is an open protocol that allows [nostr](https://nostr.com) relays to synchronize, query notes from each other, broadcast notes, and more.

## Motivation

In general nostr relays won't share notes they receive with each other, your client probably can find more relays to find data you need by metadata in notes. IPNN protocol make this relays interconnected. so, when you publish some data to your relay which have IPNN implemented, your note will be published to lot of other relays automatically, who uses those relays will get your event faster and if they IPNN nostr implementation in your publish was offline, it will query it in network and send it back to you rapidly. this interconnection make things faster, more reliable, more safe and more.

## Specification



The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119 and RFC 8174.

## [Additional Section]

