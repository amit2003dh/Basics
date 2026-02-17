
---

# 🌐 1. OSI Model (7 Layers)

![Image](https://images.openai.com/static-rsc-3/v7CVM4JUpSDnT-VQgLU2IWuvSWhtVk1AmGHVmdwB0xlGhdF8QLRZ3xd9zLrXOFyz4vhuErazenN_QpndJqroC8eFvwq4c-cYpwiQIP4-dOA?purpose=fullsize\&v=1)

![Image](https://images.openai.com/static-rsc-3/mz0N_4TDni7Fyu78ofd7S2RXRyA6sRzdPclTSoUQNIXRUGjbJ0qLynoLM3yx0X5kfMG0ar6eLvChcO12eHoFJeZTczxqDZt8cwCxO1F9X54?purpose=fullsize\&v=1)

![Image](https://images.openai.com/static-rsc-3/0WQejBCqkoIauD04XRwVXXvBGbrbp53tsxecM7fpalksI0dXtqgEBcHZnBt7XeweVIQVbpN50ARgilxMaqesBWkhLJhvgOdFEFyOpjALOZw?purpose=fullsize\&v=1)

## 🔹 OSI Layers (Top → Bottom)

| Layer            | Purpose                               |
| ---------------- | ------------------------------------- |
| 7️⃣ Application  | User-level software (HTTP, FTP, SMTP) |
| 6️⃣ Presentation | Encryption, compression, formatting   |
| 5️⃣ Session      | Manages connections                   |
| 4️⃣ Transport    | End-to-end delivery (TCP/UDP)         |
| 3️⃣ Network      | IP addressing & routing               |
| 2️⃣ Data Link    | MAC address, frames                   |
| 1️⃣ Physical     | Cables, signals, hardware             |

---

# 🌍 2. TCP/IP Model

Simplified real-world model.

| TCP/IP Layer   | OSI Equivalent               |
| -------------- | ---------------------------- |
| Application    | App + Presentation + Session |
| Transport      | Transport                    |
| Internet       | Network                      |
| Network Access | Data Link + Physical         |

---

# 🕸 3. Network Topologies

![Image](https://images.openai.com/static-rsc-3/g0R_f_rK4TXKTv13XYnQpkVUYj3y867hZfhTiFdNcSP6CyzuBgj3zyNx76JeSmQSdbf4LlHoNKKe_CCgOUxykijwYtcOgxJouGkXn1Z6FJ4?purpose=fullsize\&v=1)

![Image](https://images.openai.com/static-rsc-3/SMk-PwjdD7uRG5H5kblA7yISAItjHRLDGrQ9lxQ4G3fKDeyRcKVVvboLVAjlgFNG2vQe5DGABe27EjKLLGdlG85r3iohMRe9bPssDhYvvFM?purpose=fullsize\&v=1)

![Image](https://images.openai.com/static-rsc-3/Uc-qY0mdhboTeZCHGBUo5g0o7UDx8ibvYkfR2g2OMgd2QxCu5uU4hec3zJp6E4g51WfJRxtTUH2VMsTMN3m5TpmfrZ-na6FLrlICyn7HBJQ?purpose=fullsize\&v=1)

![Image](https://images.openai.com/static-rsc-3/bx8DAHAoSuQrDWVCeJ-9p18u8Pj94rhvXtz_O5scXoq-0jm7hENtHj6IuC2EQCWBylI3MyBRrt5thwppcvD4G7s47uFqcPOmQHfXci9jI_c?purpose=fullsize\&v=1)

![Image](https://images.openai.com/static-rsc-3/xdpKj_jtVlOjgXIha7zKNQsmP0V2cWbgsFpItTSxy8ytKe_LHwlxjat7e1rQKRch21DIynLjfrSreIzxqOjpVJoQldtL420sjgxRCB4NrYk?purpose=fullsize\&v=1)

## 1️⃣ Bus

* One main cable
* One device transmits at a time
* If cable fails → entire network fails

## 2️⃣ Ring

* Devices connected in loop
* Data flows circularly
* Break in ring = network disruption

## 3️⃣ Star

* One central device (switch/router)
* Easy to manage
* Central failure = total failure

## 4️⃣ Mesh

* Every node connected to every node
* Very reliable
* Expensive & complex

## 5️⃣ Tree

* Combination of bus + star
* Hierarchical

---

# 🚦 4. Transport Layer

## 🔵 TCP (Transmission Control Protocol)

![Image](https://static.afteracademy.com/images/what-is-a-tcp-3-way-handshake-process-three-way-handshaking-terminating-connection-6ea4a4c72d165361.jpg)

![Image](https://images.openai.com/static-rsc-3/4Ro27QCvdKwQOoxAnzwWGl08flLAOpLgzwIT_cgE29GCzF8SBSbXwegLBOpA49cSoOBJWTo6yllEHnaJ7lpFhaDPBvbOFw6vgF5ltlaoCEo?purpose=fullsize\&v=1)

![Image](https://witestlab.poly.edu/blog/content/images/2017/04/tcp-one.svg)

![Image](https://www.researchgate.net/publication/320558615/figure/fig2/AS%3A552546483224576%401508748755515/TCP-Congestion-Control-Algorithm.png)

### Features:

* Connection-oriented
* Reliable
* Ordered delivery
* Congestion control
* Error control
* Full duplex

### 3-Way Handshake

1. SYN
2. SYN-ACK
3. ACK

Used by: HTTP, HTTPS, FTP, SMTP

---

## 🟣 UDP (User Datagram Protocol)

![Image](https://d8wojkg2185gh.cloudfront.net/strapi/UDP_Header_Structure_5fc68ec626.webp)

![Image](https://www.freecodecamp.org/news/content/images/2021/07/udp-and-tcp-comparison.jpg)

![Image](https://hpbn.co/assets/diagrams/2aaa8d11ee7fd2d8a332e6dc68dc50ae.svg)

![Image](https://cdn.kastatic.org/ka-perseus-images/9d185d3d44c7ef1e2cd61655e47befb4d383e907.svg)

### Features:

* Connectionless
* Faster
* No guarantee of delivery
* No ordering
* Small header (8 bytes)

Used by:

* DNS
* Video streaming
* Gaming

---

# 🌎 5. IP Addressing

## IPv4

* 32 bits
* Example: 192.168.1.1

## IPv6

* 128 bits
* Hexadecimal format
* Example: 2001:0db8::1

---

## IP Address Classes (IPv4)

| Class | Range                 |
| ----- | --------------------- |
| A     | 0 – 127               |
| B     | 128 – 191             |
| C     | 192 – 223             |
| D     | 224 – 239 (Multicast) |
| E     | 240 – 255 (Reserved)  |

---

## Special Addresses

* 127.0.0.1 → Localhost
* 0.0.0.0 → Default
* 192.168.x.x → Private
* 10.x.x.x → Private

---

# 🌍 6. DNS (Domain Name System)

![Image](https://www.researchgate.net/publication/354591476/figure/fig1/AS%3A1068111553912832%401631669047410/Standard-DNS-resolution-process.png)

![Image](https://substackcdn.com/image/fetch/%24s_%21P_Ol%21%2Cf_auto%2Cq_auto%3Agood%2Cfl_progressive%3Asteep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff0a1bb2c-a1bc-40ce-abde-6fb9d2a66ce8_1600x570.png)

![Image](https://miro.medium.com/0%2Aw4_IIjmSUdtMp-hT)

![Image](https://media.licdn.com/dms/image/v2/D4E22AQH0OmsagdhTcA/feedshare-shrink_800/feedshare-shrink_800/0/1674789713761?e=2147483647\&t=QmFTs76wBsK74He1FkKNZ_5mCWsiYlf8jXPm2nIq6-w\&v=beta)

DNS converts:
Domain → IP Address

### Flow:

1. Local cache
2. ISP DNS
3. Root server
4. TLD server (.com)
5. Authoritative server
6. Returns IP

---

# 🧠 7. Ports

* 16-bit numbers
* Range: 0 – 65535

| Range       | Type       |
| ----------- | ---------- |
| 0–1023      | Reserved   |
| 1024–49151  | Registered |
| 49152–65535 | Private    |

Examples:

* HTTP → 80
* HTTPS → 443
* MongoDB → 27017
* Telnet → 23

---

# 🏠 8. LAN / MAN / WAN

| Type | Meaning                  |
| ---- | ------------------------ |
| LAN  | Small area (home/office) |
| MAN  | City level               |
| WAN  | Country/Global           |

---

# 🔁 9. ARP (Address Resolution Protocol)

![Image](https://marvel-b1-cdn.bc0a.com/f00000000310757/www.fortinet.com/content/dam/fortinet/images/cyberglossary/what-is-arp.jpg)

![Image](https://www.researchgate.net/publication/346829282/figure/fig8/AS%3A1002115157725205%401615934280611/ARP-request-and-ARP-reply.ppm)

![Image](https://www.meridianoutpost.com/resources/articles/command-line/images/arp-s.png)

![Image](https://www.researchgate.net/publication/269775791/figure/fig5/AS%3A826587427639297%401574085208192/ARP-cache-table-after-an-ARP-spoofing-attack.png)

Purpose:
Convert IP Address → MAC Address

Steps:

1. Broadcast ARP request
2. Device replies with MAC
3. Stored in ARP cache

---

# 🔐 10. HTTP

## Properties:

* Application layer
* Uses TCP
* Stateless

## Methods:

* GET
* POST
* PUT
* DELETE

## Status Codes:

| Code | Meaning       |
| ---- | ------------- |
| 1xx  | Informational |
| 2xx  | Success       |
| 3xx  | Redirection   |
| 4xx  | Client Error  |
| 5xx  | Server Error  |

---

# 🍪 11. Cookies

* Stored in browser
* Used for session management
* Can be first-party or third-party

---

# 📧 12. Email Protocols

| Protocol | Purpose               |
| -------- | --------------------- |
| SMTP     | Send mail             |
| POP3     | Receive mail          |
| IMAP     | Manage mail on server |

---

# 🧱 13. Data Link Layer

* Works with frames
* Uses MAC addresses
* Handles ARP
* Switches operate here

---

# 🔥 14. Firewall

Filters packets based on:

* IP
* Port
* Protocol
* Flags

Types:

* Stateless
* Stateful (more efficient)

---

# 📦 Packet Breakdown

| Layer     | Unit    |
| --------- | ------- |
| Transport | Segment |
| Network   | Packet  |
| Data Link | Frame   |

---
