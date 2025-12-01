+++
title = "About"
description = "A little bit about me and my projects."
layout = "single"
+++

## About me

Mostly self-taught and driven by curiosity and a love for software. I
particularly enjoy understanding how things work as a whole, designing and
building solutions to problems, and using resources to their full potential. I
typically opt for simple solutions over complex ones.

## My projects

### Australian Weather API

- **Status ::** First commit: 2025-05-18. 
  
  2025-11-29: In active private development. Public "it works for me" MVP release set
  for December 2025.

- **Overview ::** This project is my baby. It's a pseudo-microservice, RESTful
API written in Python, and is specifically for serving public weather data
available from the Bureau of Meteorology in Australia. Like most modern
businesses, they serve said data via FTP, which made for a fun design process
when building a sync service that always serves fresh weather data.

- **Details ::** Based on Flask; Pydantic used heavily for all service
  communications, contracts, and resource requests; PostgreSQL with hand-rolled
  shapefile ETL; hand-rolled platform services and authorization and
  authentication systems; Dockerised for cross-platform support; follows the
  [Microsoft Rest API
  Guidelines](https://github.com/microsoft/api-guidelines/blob/vNext/azure/Guidelines.md);
  well documented codebase, using Stripe's API docs as the baseline for public
  documentation standards.

- **Purpose ::** The main reason was for me to learn Python, programming, and to
  gain a better understanding of how software works in general. After completing
  the [Automate the Boring Stuff](https://automatetheboringstuff.com/) course, I
  wanted to know how to actually build a program hands on. I just learn better
  this way. As there was already a personal interest in weather, this project
  seemed like a fun fit!
  
  Secondly, this program would allow for users to self-host their own weather
  data systems. While the data is public access and other weather front-ends
  exist, none of them are open source.

### Helium browser packaging

- **Status ::** Submitted 2025-09-14. 

  Actively maintained. See
  [helium-browser-bin](https://aur.archlinux.org/packages/helium-browser-bin) on
  the AUR, or the public [GitHub
  repo](https://github.com/s6muel/helium-browser-bin) that has in depth
  documentation for users looking to understand the `PKGBUILD`.

- **Overview ::** This is my first public package for the AUR. As I get older, I
  feel a sense of obligation to give back to the people and communities that
  have been so useful to me over the years. Maintaining this package has also
  taught me a lot about the Linux system in general and is an awesome learning
  experience that I'm grateful for. 
  
  An interesting tidbit is that the standard `*-flags.conf` convention that we
  Linux users expect is a feature implemented downstream and not a feature of
  Chromium (and presumably CEF?) itself[^1].

- **Details ::** The `PKGBUILD` was originally built for the AppImage packaging,
  which eventually changed to binary packaging as a matter of user expectation
  and Arch conventions. The AppImage is maintained by Pujan Modhar on the AUR[^2].
  The process follows the Chromium and Ungoogled Chromium packaging since there
  are very little differences between these programs. That seemed a logical
  approach for me to make sure this program is stable for users.

- **Purpose ::** To give back to the Linux community. However, my experience of
  packaging, engaging with the community, and trying to make sure this is the
  best package it can be, ended up making this really bloody fun.

### Gleemacs

- **Status ::** In daily use since 2025-11-04.

- **Overview ::** My personal GNU Emacs configuration in one beautiful `org`
  file. It's for my own useage and is setup for writing and programming. It's
  highly performant, clean, and involves no evil mode. It was designed to
  harness Emacs with minimal third-party packages, and enhances the out of the
  box experience without being too opinionated.
  
- **Details ::** The great thing about `org-mode` is that you can write prose
  and code in the same document. Therefore I'd recommend reading through
  [gleemacs](/gleemacs) not only for the information, but for the fun that
  awaits!


[^1]: https://gitlab.archlinux.org/archlinux/packaging/packages/chromium/-/blob/main/PKGBUILD?ref_type=heads#L169
[^2]: https://aur.archlinux.org/packages/helium-browser-appimage
