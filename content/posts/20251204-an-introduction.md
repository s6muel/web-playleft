---
title: "What's powering my website"
date: 2025-12-04
description: "A brief overview of the internals running this website."
summary: "A brief overview of the internals running this website."
tags: ["hosting"]
toc: true
---
## "The first one"

This was just a [place holder post](/posts/the-first-one/) when I first
published the previous version of the website. Like many who envision things for
their domain, I had intended to write a post about hosting this website as an
example for others looking to self host. Obviously, that never happened!

So, while this revision will not be a guide, I will provide you a brief overview
of the software and services powering my website.

## Self-hosting

When I say self-hosting, I mean everything is done by oneself. That means
starting with a vanilla *<insert-your-favourite-server-here>* ISO and finishing
with a publicly available website. If you're reading this and that sounds
intimidating, to be honest, it's really not.

## Requirements

-   Fast (no one likes to wait, unless that's you: please take a ticket)
-   Simple (no one wants to fuck about endlessly, it's just a website)
-   Reliable (no one wants to fuck about endlessly, it's just a website)

## Software

### Front-end

I write all of the content in GNU Emacs' `org-mode` which is exported to
markdown, and then built with Hugo and my custom theme. It's super light weight,
readable (aesthetically; otherwise all content is world-class and nobel worthy),
and accessible.

### Back-end

These beautifully simple HTML files are lovingly served to you with good old
`nginx` (not configured the Apache way!), and your traffic is secured with
*military grade encryption with over 9000 bits of entropy* by Let's Encrypt. I'm
using an Australian based provider for hosting, but the server is based in
Singapore hoping location will help improve international routing. DNS is
provided by the Cloudflare free plan.

### Server

A humble 1vCPU/1GB RAM VPS running vanilla Debian stable (image sourced from
Debian.org).

### Security

Admin user and disk encryption passwords are seven word diceware phrases for
ease of access and reasonable levels of strength. Typical SSH hardening like
restricting root login, key-only access, and so on so forth. `Fail2Ban` and
`recidive` configured to IP ban repeat miscreants (see: script kiddies).

The last point was more out of my own interest in configuring these tools
correctly with incremental ban times. While they work as they should, the setup
doesn't stop the traffic. Not that it matters to the server or performance, but
it was a useful learning experience nonetheless.

## Hardware

-   Leopold FC660
-   Nespresso Mini
-   WD-40
