+++
title = "Using dnsproxy for encrypted DNS on Linux"
author = ["Sam Sinclair"]
date = 2025-12-19T14:39:00+11:00
tags = ["linux", "sysadmin", "DNS", "privacy", "security"]
draft = false
description = "Setting up dnsproxy on Linux to provide encrypted DNS via secure transport protocols with systemd-resolved and NetworkManager."
summary = "Configuring dnsproxy as a local endpoint on Linux with systemd-resolved and NetworkManager to use encrypted DNS resolvers like ControlD and NextDNS."
toc = true
+++

## Introduction {#introduction}

This is a quick and simple guide for using
[dnsproxy](https://github.com/AdguardTeam/dnsproxy) as a system-wide DNS
endpoint to support DNS-over-HTTPS (DoH), DNS-over-QUIC (DoQ), and DNS-over-TLS
(DoT) on Linux systems. DNS queries are handled locally by dnsproxy, accessible
at `127.0.0.1`, and forwarded to our encrypted upstream resolver of choice,
allowing for consistent usage across the system and VPNs (when configured). It's
also particularly useful when encrypted protocols aren't available (most VPN
applications), or where you want to minimise exposing your IP to logs in
paid-for services (i.e., ControlD's Legacy Resolver, or NextDNS' Linked IP).

I found this set up to be stable with providers like NextDNS and ControlD, but
it'll work just as well with public resolvers like Cloudflare, Quad9,
RethinkDNS, etc..

***[!] Important Note ::** tinkering with DNS can sometimes (almost always 99% of
  the time) result in the striking of keyboards with great vengeance and furious
  anger. I therefore developed this guide out of trial and error to save you and
  future me the trouble. If you find yourself without DNS, just work backwards
  from where you are in the guide and you'll be fine.*


## Requirements {#requirements}

+ **dnsproxy ::** install with your package manager or grab the binaries from
  [the GitHub repo](https://github.com/AdguardTeam/dnsproxy).
+ **systemd ::** we rely on `systemd-resolved`.
+ **NetworkManager ::** not _required_ but this guide is tailored for it, any
    network manager will work once configured.


## Set up {#set-up}


### Configure dnsproxy as an endpoint {#configure-dnsproxy-dot-yaml-as-an-endpoint}

+ **Config reference ::** <https://github.com/AdguardTeam/dnsproxy?tab=readme-ov-file#usage>

Modify `/etc/dnsproxy/dnsproxy.yaml` and make the following changes:

-   bootstrap
    -   This is a temporary clear-text dependency to resolve the encrypted
        resolver's hostname, so you should use a trusted provider.
    -   For ControlD: retrieve from the relevant endpoint settings.
    -   For NextDNS and others: use a trusted DNS for initial bootstrapping (e.g.
        `9.9.9.9`).
-   listen-addrs
    -   `127.0.0.1` (localhost)
    -   `::1` (optional for IPv6)
-   listen-ports
    -   Use port 5353 to avoid conflicts with other services. Especially relevant if
        you use a VPN application: they sometimes install their own resolvers and
        hog port 53 which prevents `dnsproxy` from operating.
-   upstream
    -   Format: `<PROTOCOL>://<RESOLVER_ADDRESS>`
    -   Protocols:
        -   DoH, prepend `https://`
        -   DoQ, prepend `quic://`
        -   DoT, prepend `tls://`
    -   ControlD example: `<RESOLVER_ID>.dns.controld.com`
    -   NextDNS example: `<RESOLVER_ID>.dns.nextdns.io`
-   verbose
    -   Set to `true` to enable debug level logging. 
	-   This is optional. `false` is the default so you can safely omit this if
        you don't care about logs.


Your config should look something like this:

```yaml
# This is the yaml configuration file for dnsproxy with minimal working
# configuration, all the options available can be seen with ./dnsproxy --help.
# To use it within dnsproxy specify the --config-path=/<path-to-config.yaml>
# option.  Any other command-line options specified will override the values
# from the config file.
---
bootstrap:
  - "123.123.123.123"
  - "2606:1a40::22"
listen-addrs:
  - "127.0.0.1"
  - "::1"
listen-ports:
  - 5353
max-go-routines: 0
ratelimit: 0
ratelimit-subnet-len-ipv4: 24
ratelimit-subnet-len-ipv6: 64
udp-buf-size: 0
upstream:
  - "quic://1234asdf.dns.provider.com"
timeout: '10s'
verbose: true
```


### Update `resolved.conf` {#update-resolved-dot-conf}

Open `/etc/systemd/resolved.conf` and modify the DNS entry to point to our
`dnsproxy` service. Make sure to use the port that you set as the `listen-ports`
when [configuring dnsproxy](#configure-dnsproxy-dot-yaml-as-an-endpoint).

```cfg
DNS=127.0.0.1:5353
```

Restart `systemd-resolved` to apply the changes (don't worry, your existing DNS
will still work):

```bash
$ systemctl restart systemd-resolved
```


### Start the proxy {#start-the-proxy}

Now start `dnsproxy` in the terminal. Leave it running and continue in a new
terminal window.

```bash
dnsproxy --config-path=/etc/dnsproxy/dnsproxy.yaml
```


### Configure NetworkManager {#configure-networkmanager}

Configure your network interface with NetworkManager to point to the DNS proxy
service, and restart the connection to apply the settings. If you don't know the
connection name, run `nmcli -t connection show --active` to list them.

***[!] Important ::** The proxy must be running before you restart the
  connection, otherwise you'll have no DNS resolution.*

<!--listend-->

```bash
nmcli connection modify "<CONNECTION_NAME>" ipv4.dns "127.0.0.1"
nmcli connection modify "<CONNECTION_NAME>" ipv6.dns "::1"
# This prevents DNS settings from being updated by your router/network
nmcli connection modify "<CONNECTION_NAME>" ipv4.ignore-auto-dns true
nmcli connection modify "<CONNECTION_NAME>" ipv6.ignore-auto-dns true
nmcli connection down "<CONNECTION_NAME>"
nmcli connection up "<CONNECTION_NAME>"
```


#### Reverting NetworkManager settings {#reverting-networkmanager-settings}

If you need/want to revert this configuration, run the following. This will
reset DNS settings to a DHCP configuration.

```bash
nmcli connection modify "<CONNECTION_NAME>" ipv4.dns ""
nmcli connection modify "<CONNECTION_NAME>" ipv6.dns ""
nmcli connection modify "<CONNECTION_NAME>" ipv4.ignore-auto-dns false
nmcli connection modify "<CONNECTION_NAME>" ipv6.ignore-auto-dns false
nmcli connection down "<CONNECTION_NAME>"
nmcli connection up "<CONNECTION_NAME>"
```


### Testing the proxy {#testing-the-proxy}

To test `systemd-resolved` is using dnsproxy, run:

```bash
resolvectl query example.com
```

An output similar to the below is expected; it shows that queries are
being sent _to_ `dnsproxy` over plain DNS, hence "Data is auth...: no."
`dnsproxy` then sends those plain requests to our upstream provider via
encrypted transports (Do{H,Q,T}).

To confirm DNS queries are encrypted, check your provider's status page or
[dnscheck.tools](https://dnscheck.tools/), and double check with [dnsleaktest.com](https://dnsleaktest.com/).

```bash
example.com: 123.123.123.123
             2606:1a40::22

-- Information acquired via protocol DNS in 23.2ms.
-- Data is authenticated: no; Data was acquired via local or encrypted transport: no
-- Data from: network
```

If you set verbose logging to true when [configuring
dnsproxy](#configure-dnsproxy-dot-yaml-as-an-endpoint), check the other terminal
window where `dnsproxy` is running, look for lines like the following to see if
it's  upstream is resolving correctly:

```bash
Dec 20 16:10:18 <HOSTNAME> dnsproxy[258961]: 2025/12/20 16:10:18.807274 DEBUG set upstream idx=0 addr=quic://1234asdf.dns.provider.com:853
Dec 20 16:10:19 <HOSTNAME> dnsproxy[258961]: 2025/12/20 16:10:19.777028 DEBUG sending request addr=123.123.123.123:53 proto=udp qtype=A qname=1234asdf.dns.provider.com.
Dec 20 16:10:19 <HOSTNAME> dnsproxy[258961]: 2025/12/20 16:10:19.964799 DEBUG sending request addr=quic://1234asdf.dns.provider.com:853 proto=udp qtype=AAAA qname=api.example.com.
Dec 20 16:10:20 <HOSTNAME> dnsproxy[258961]: 2025/12/20 16:10:20.267163 DEBUG response received addr=quic://1234asdf.dns.provider.com:853 proto=udp status=ok
Dec 20 16:10:20 <HOSTNAME> dnsproxy[258961]: 2025/12/20 16:10:20.267302 DEBUG exchange successfully finished prefix=dnsproxy upstream=quic://1234asdf.dns.provider.com:853 question=";api.example.com.\tIN\t AAAA" duration=489.766768ms
```


### Starting the systemd unit (enabling autostart) {#starting-the-systemd-unit--enabling-autostart}

Once happy with the setup, you can stop the `dnsproxy` terminal process and
start it with a systemd unit and enable it to make sure it's always running with
the below. 

***[!] Note ::** If you don't want to muddy up `journalctl` logs, you should
revert the verbose setting back to false, see: [configuring
dnsproxy](#configure-dnsproxy-dot-yaml-as-an-endpoint).*

```bash
$ systemctl enable dnsproxy.service
$ systemctl start dnsproxy.service
```

If your distributions packaging didn't come with a service or you installed from
source, you can use the [unit provided by Arch Linux packaging](https://gitlab.archlinux.org/archlinux/packaging/packages/dnsproxy/-/blob/main/dnsproxy.service?ref_type=heads).


## Usage {#usage}

+ **Unit Monitoring ::** Run `journalctl -u dnsproxy -f` in terminal
+ **Chromium ::** Secure DNS "On" and set to "OS Default"
+ **Firefox ::** DNS over HTTPS set to "Default Protection"
+ **VPN / Other ::** Set custom DNS to `127.0.0.1`
