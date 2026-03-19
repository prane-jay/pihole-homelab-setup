## Pi-hole Homelab Setup
This project demonstrates my first homelab setup, built with the goal of developing hands-on networking skills.

It is a network-wide advertisement and malicious domain blocking setup using Pi-hole software on Raspberry Pi 3, with Unbound configuration as a local recursive DNS resolver for the purpose of a more private, secure alternative to the ISP given resolver. 

---

## Project Overview
This project utilizes a Raspberry Pi 3 to block ads, trackers and malicious domains. Pi-hole sits on the local network and intercepts DNS queries from every connected device. Domains that are flagged in the blocklists (a collection of unwanted domains) are sinkholed before they reach the connected device. Unbound sits behind Pi-hole and recursively resolves all remaining queries, removing the reliance on ISP or third party DNS providers such as Google and Cloudflare. 

---

## Hardware Used
- Raspberry Pi 3 (Model B+)
- MicroSD card (16GB) 
- Ethernet cable

---

## Features
- Network-wide DNS filtering for advertisements, trackers, and malicious domains for all devices on network
- Additional blocklists for specific threats beyond default
- Utilizing Unbound as a local recursive resolver. This eliminates the need for upstream DNS providers, as queries are resolved directly from root servers.
- Live dashboard for monitoring network DNS traffic

---

## Installation Notes

Raspberry Pi OS Lite (32 bit) was flashed to a microSD card using the official Raspberry Pi Imager. SSH service was enabled with password authentication for headless access. 

INSERT IMAGE

Inserted the microSD into the Raspberry Pi 3, then went into my ISP DHCP settings to reserve a static IP address so that it never changes on the network

INSERT IMAGE 2

Used the username and password set in the imager to SSH into the Raspberry Pi to install Pi-hole using the official installation documentation: [https://docs.pi-hole.net/main/basic-install/](url)

INSERT IMAGE 3

Logged into Pi-hole admin dashboard and added additional blocklists with a publicly available collection: [https://firebog.net/](url)

INSERT IMAGE 4

---

## Unbound

By default, Pi-hole will forward unblocked DNS queries to an upstream provider such as Cloudflare. Third party DNS resolvers log your queries, using Unbound eliminates. It resolves queries recursively, meaning it will connect to DNS root servers and walk the chain itself rather than asking another party to do it. Unbound runs locally, Pi-hole will forward requests to 127.0.0.1 on port 5335 as its upstream resolver. 

This was configured using the official documentation: [https://docs.pi-hole.net/guides/dns/unbound/](url)

INSERT IMAGE 

---

## What I learned

- Linux administration: editing config files, managing services with systemctl, SSH, and file permissions
- Network configuration: DHCP management and assigning static IPs
- DNS resolution: end-to-end process (recursive vs. iterative lookups, root, TLD, and authoritative servers)
- DNS roles: difference between forwarding and recursive resolvers, including privacy implications

