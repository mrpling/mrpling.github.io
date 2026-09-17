---
layout: default
title: "Domains can now say they're for sale - RFC 10023"
date: 2026-09-17
---

# Domains can now say they're for sale - RFC 10023

A registered domain is not necessarily an unavailable domain. This sounds obvious, but until recently there has been no standard way for the owner of a domain to say, through the DNS itself, that the domain is available to buy.

RFC 10023 changes that. Published in July 2026, RFC 10023 defines a simple `_for-sale` DNS record that a domain owner can publish to indicate that a registered domain is for sale.

For example, for `example.com`:

```text
_for-sale.example.com TXT "v=FORSALE1;"
```

That is enough to signal that the domain is being offered for sale.

Additional TXT records can provide more information, including:

```text
v=FORSALE1;ftxt=This domain is for sale
v=FORSALE1;furi=https://example.com/sale
v=FORSALE1;furi=mailto:seller@example.com
v=FORSALE1;fval=EUR2500
```

## Why this is interesting

Until now finding out whether a registered domain is actually for sale has meant checking marketplaces, visiting the domain, searching for a broker or trying to contact the owner.

RFC 10023 moves part of that information into the domain itself. 

The domain seller can point buyers towards their own landing page, an email address, a broker, a marketplace or another service entirely.

That does not make marketplaces unnecessary. But it does separate two things which have traditionally been closely tied together:

**discovering that a domain is for sale**

and

**choosing how the transaction takes place**

That distinction could become important if the convention gains broad adoption.

## Available or for sale?

This also changes how I think about domain availability in rdap.ai.

Traditionally a domain lookup gives a fairly simple answer:

```text
Available
Registered
```

But from the point of view of someone looking for a domain to acquire, there is another useful state:

```text
Available
Registered
ForSale
```

An available domain can be registered immediately.

A domain marked with RFC 10023 is already registered, but its owner has explicitly signalled that it may be acquired.

rdap.ai now checks for this signal when looking at registered domains and can show the information supplied by the owner, including asking price, text and contact links where present.

Prices are indicative only and there's no automatic following of links (that's up to you). You can also turn on/off ForSale checking in the Settings area of the app.

When rdap.ai receives a valid ForSale signal a small green box appears in the results which reveals the ForSale details when clicked. The domain 'example.nl' shows how this works.

![ForSale in action](/assets/images/forsale-screenshot.png)

## A small protocol with interesting consequences

One reason RFC 10023 is interesting is how little infrastructure is required to use it.

A domain owner who can edit DNS can publish the record today. They do not need their registry, registrar or marketplace to adopt a new protocol first.

Registrars could eventually make this even easier by exposing something like:

```text
For sale: Yes

Price: 2500 EUR
Sales page: ...
```

and then managing the DNS records automatically.

Similarly, domain search tools, registrars, marketplaces and automated agents can independently decide to recognise the signal.

## Privacy and rdap.ai

I did not particularly want every `_for-sale` lookup from rdap.ai being sent to a public DNS resolver operated by Google, Cloudflare or another third party.

So rdap.ai uses its own recursive DNS resolver for these checks.

The lookup path is deliberately simple:

```text
rdap.ai
   ↓
RFC 10023 lookup service
   ↓
local recursive resolver
   ↓
DNS
```

The resolver performs normal recursive DNS resolution rather than forwarding searches to a public DNS provider.

The lookup service itself is deliberately narrow: it exists to retrieve `_for-sale` records, not to operate as a general-purpose public DNS proxy.

## Still early

[RFC 10023](https://www.rfc-editor.org/info/rfc10023/) is new, so support is naturally limited at the moment.

Marco Davids of SIDN labs, the registry for `.nl`, was involved in developing and deploying the approach, and there are now tools beginning to consume the records.

The interesting thing is how quickly the idea spreads beyond those early implementations. The barrier to adoption is very low: for many domain owners publishing this signal is simply a DNS change.

If that happens at scale, "registered" may become a less useful description on its own.

The more useful question could become:

**Can this domain be acquired?**
