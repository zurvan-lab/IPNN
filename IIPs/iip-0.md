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

In general, nostr relays won't share notes they receive with each other. Your client may be able to find more relays to find the data you need by using the metadata in notes. IPNN protocol makes these relays interconnected. So, when you publish data to your relay with IPNN implementation, your note will be automatically published and broadcast to many other relays with IPNN implementation as well. Users of those relays will receive your event faster, and if their IPNN nodes were offline in your publish time, it will query it in the network and send it back to you quickly. This interconnection makes things faster, more reliable, more secure, and more.

## Specification



The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119 and RFC 8174.

## [Additional Section]

