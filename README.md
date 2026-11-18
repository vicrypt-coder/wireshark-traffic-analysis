# Wireshark Traffic Analysis

Hands-on network traffic analysis using Wireshark, completed while learning cybersecurity (started September 2026).

**Tools used:** Wireshark, Windows Command Prompt
**Environment:** Windows 10, Wi-Fi

## 01. Capturing and analysing DNS traffic

**Goal:** capture the DNS packets my computer sends when it looks up a domain, and identify what each one contains.

**Steps:**
1. Started a Wireshark capture on the Wi-Fi interface.
2. Cleared the DNS cache with `ipconfig /flushdns`, so the lookup would go out on the network.
3. Ran `nslookup example.com`.
4. Applied the display filter `dns.qry.name == "example.com"` to isolate the relevant packets.

![DNS capture in Wireshark](01-dns-capture/dns-capture-example-com.png)

**What I found:**
- The capture had 2,254 packets. The filter reduced the view to 4.
- Two queries and two responses: one for an **A** record (IPv4) and one for an **AAAA** record (IPv6).
- Source of the queries: my computer (192.168.193.87). Destination: the DNS server (192.168.193.223), the same server `nslookup` reported.
- The A response returned two IPv4 addresses: 104.20.23.154 and 172.66.147.243, matching my earlier NsLookup.io results.
- The AAAA response returned two IPv6 addresses.
- Each response arrived roughly 30 to 40 milliseconds after its query.

**What I learned:**
- How a DNS lookup looks at packet level: a query goes out, a response comes back.
- Why a domain can have both IPv4 and IPv6 addresses.
- How display filters make it possible to find a few relevant packets in thousands.
- DNS queries are sent in plain text, so anyone who can see the traffic can see which domains I look up.

## Ethical note
Captures were taken only on my own device and network. Raw capture files are not uploaded because they can contain private traffic.

## Next steps
Capturing and comparing HTTP and HTTPS traffic, and following a TCP connection.
