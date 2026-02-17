 **WhatsApp High-Level Architecture (HLD)** for **100M+ concurrent users**.

This is how you answer in senior interviews.

---

# 🟢 1️⃣ Goals of WhatsApp HLD

System must support:

* 1–1 Messaging
* Group Messaging
* Status
* Audio/Video Calls
* End-to-End Encryption
* 100M+ concurrent users
* Low latency (<100ms message delivery)
* High availability (99.99%)

---

# 🏗 2️⃣ High-Level Architecture Overview

![Image](https://www.infosys.com/content/dam/infosys-web/en/techcompass/images/distributed-messaging-systems06.jpg)

![Image](https://miro.medium.com/1%2AgW4JrHTr86HnTrouQYLgJQ.png)

![Image](https://i.sstatic.net/7nPwb.png)

![Image](https://media2.dev.to/dynamic/image/width%3D800%2Cheight%3D%2Cfit%3Dscale-down%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fraw.githubusercontent.com%2Fsw360cab%2Fwebsockets-scaling%2Fmaster%2Fdiagrams%2Fclustered_k8s_nodeport.png)

---

# 🧱 3️⃣ Core Components

```
Clients (Mobile/Web)
        ↓
Global Load Balancer
        ↓
API Gateway
        ↓
Auth Service
        ↓
Real-Time Messaging Service (WebSocket Cluster)
        ↓
Message Queue (Kafka)
        ↓
Message Service
        ↓
Databases + Cache
        ↓
Notification Service
```

---

# 4️⃣ Client Layer

* Android / iOS / Web
* Persistent WebSocket connection
* Local encryption/decryption
* Stores session keys locally

---

# 5️⃣ Global Load Balancer

Distributes traffic across regions.

Used:

* Geo-DNS
* Anycast routing

Ensures:

* Lowest latency region routing
* Failover handling

---

# 6️⃣ API Gateway

Responsibilities:

* Rate limiting
* Authentication validation
* Routing to microservices
* Metrics collection

Acts as:
**Single entry point**

---

# 7️⃣ Authentication Service

* Validates JWT
* Manages sessions
* Handles device binding
* Key bundle distribution (for E2EE)

---

# 8️⃣ Real-Time Messaging Layer

Core of WhatsApp.

Uses:

* WebSocket cluster
* Sticky sessions

Each server maintains:

```
userId → socket connection map
```

When message arrives:

1. Check if receiver online
2. Push via WebSocket
3. If offline → enqueue

---

# 9️⃣ Message Queue (Kafka)

Used for:

* Decoupling real-time layer
* Reliability
* Message durability
* Replay in case of failure

Flow:

```
WebSocket → Kafka → Message Service → DB
```

Benefits:

* Handles spikes
* Prevents overload
* Enables async processing

---

# 🔟 Message Service

Responsible for:

* Persisting encrypted messages
* Updating delivery status
* Group fan-out logic
* Triggering notifications

---

# 1️⃣1️⃣ Database Design (At Scale)

We use **polyglot persistence**.

## Primary DB (Messages)

* Cassandra / DynamoDB
* Partitioned by chatId
* Optimized for write-heavy workload

Why NoSQL?

* Massive scale
* Horizontal scalability
* High availability

---

## User Metadata DB

* MySQL / PostgreSQL
* Strong consistency

---

## Cache Layer

* Redis

Used for:

* Online users
* Session tokens
* Rate limiting
* Presence info

---

# 1️⃣2️⃣ Media Storage

Images/videos stored in:

* Object storage (S3 equivalent)
* CDN for global delivery

Flow:

```
Client encrypts media
Upload to storage
Store media URL in message
```

---

# 1️⃣3️⃣ Status Service

Separate microservice.

* TTL index (24hr expiry)
* Cached feed generation
* Privacy filtering

---

# 1️⃣4️⃣ Call System HLD

![Image](https://webrtc.github.io/webrtc-org/assets/images/webrtc-public-diagram-for-website.png)

![Image](https://runby.com/system/inserted_images/images/000/000/583/blog_export/TURN.png?1488875881=)

![Image](https://blog.ivrpowers.com/postimages/technologies/ivrpowers-turn-stun-screen.005.jpeg)

![Image](https://storage.googleapis.com/100ms-cms-prod/cms/turn_server_usage_6868821b66/turn_server_usage_6868821b66.jpg)

Uses:

* Signaling Server (WebSocket)
* WebRTC for media
* STUN/TURN servers

Flow:

```
Caller → Signaling Server → Receiver
      ↓
Offer/Answer exchange
      ↓
Direct peer-to-peer media
```

Media does NOT pass through WhatsApp servers.

---

# 1️⃣5️⃣ Group Messaging at Scale

Problem:

* 1 message → 1000 users

Solution:

Fan-out on write:

```
Sender
  ↓
Kafka
  ↓
Generate copies per user
  ↓
Store in user inbox partitions
```

Scales better than fan-out on read.

---

# 1️⃣6️⃣ End-to-End Encryption Layer

Encryption occurs:

* On client
* Before network transmission

Server stores:

* Ciphertext only
* No plaintext
* No private keys

Key distribution service:

* Public keys only

---

# 1️⃣7️⃣ Presence System

Tracks:

* Online / Offline
* Typing indicator
* Last seen

Stored in:

* Redis (in-memory)
* TTL-based expiration

---

# 1️⃣8️⃣ Scalability Strategy

### Horizontal Scaling

* Stateless services
* Auto-scaling groups
* Kubernetes orchestration

### Data Partitioning

* Shard by userId
* Shard by chatId

---

# 1️⃣9️⃣ Reliability Mechanisms

* Multi-region deployment
* Data replication
* Circuit breakers
* Retry with exponential backoff
* Idempotent message IDs

---

# 2️⃣0️⃣ Observability

* Prometheus (metrics)
* ELK stack (logs)
* Distributed tracing
* Alerting system

---

# 2️⃣1️⃣ Security

* TLS everywhere
* E2EE
* Rate limiting
* DDoS protection
* Device binding

---

# 2️⃣2️⃣ Handling 100M Concurrent Users

Key optimizations:

* Persistent WebSocket (no polling)
* Efficient binary protocol
* Minimal payload size
* Sharded DB clusters
* Event-driven architecture
* CDN offloading for media

---

# 🎯 Final HLD Architecture Summary

```
Clients
  ↓
Global LB
  ↓
API Gateway
  ↓
Auth
  ↓
WebSocket Cluster
  ↓
Kafka
  ↓
Message Service
  ↓
NoSQL DB
  ↓
Redis Cache
  ↓
Notification + Media CDN
```

---

# 🧠 How to Present in Interview

1. Start with requirements
2. Draw high-level flow
3. Explain scaling
4. Explain storage choice
5. Add reliability
6. Add security
7. Discuss tradeoffs

---
Now we enter **real distributed systems territory**.

Message storage is the hardest part of WhatsApp scale.

We design **Message Sharding Strategy for 100M–1B users**.

---

# 🎯 1️⃣ Problem Statement

We must handle:

* Billions of messages per day
* Massive write-heavy workload
* Low-latency reads
* Group fan-out
* Multi-region replication
* No single point of failure

---

# 🧱 2️⃣ Why Sharding Is Mandatory

Single DB will fail due to:

* Write bottleneck
* Storage limits
* Lock contention
* Index explosion

So we **horizontally shard**.

---

# 🧠 3️⃣ Sharding Strategy Options

## Option A — Shard by UserID

## Option B — Shard by ChatID

## Option C — Hybrid (Recommended)

We analyze each.

---

# 🔹 Option A: Shard by UserID

```
shard = hash(userId) % N
```

Each user’s inbox stored in one shard.

### ✅ Pros

* Fast user message fetch
* Balanced distribution (if users uniform)

### ❌ Cons

* Group message duplication complex
* Heavy users create hotspots

---

# 🔹 Option B: Shard by ChatID

```
shard = hash(chatId) % N
```

Each chat lives fully in one shard.

### ✅ Pros

* Group messages easy
* All chat messages colocated

### ❌ Cons

* Large groups → hotspot shard
* Uneven distribution

---

# 🔥 Option C (Production-Grade): Hybrid Model

We combine:

* **Chat-based partitioning**
* **User inbox indexing**

---

# 🟢 4️⃣ Recommended Production Architecture

### Primary Partition Key → `chatId`

### Secondary Index → `userId`

We use something like:

* Cassandra
* DynamoDB

Schema:

```
Partition Key: chatId
Clustering Key: timestamp
```

This allows:

* Efficient range queries
* Ordered retrieval
* Append-only writes

---

# 🧱 5️⃣ Physical Shard Distribution

![Image](https://assets.digitalocean.com/articles/understanding_sharding/DB_image_3_cropped.png)

![Image](https://cassandra.apache.org/_/_images/diagrams/apache-cassandra-diagrams-01.jpg)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AChr0HbRtaRYZRtNB1mrh6Q.png)

![Image](https://i.sstatic.net/QgZA3.png)

We distribute shards across:

* Multiple nodes
* Multiple availability zones
* Multiple regions

Using **consistent hashing ring**.

---

# 🔁 6️⃣ Consistent Hashing

Instead of:

```
hash(key) % N
```

We use:

* Hash ring
* Virtual nodes
* Minimal reshuffling when adding nodes

Benefits:

* Easy scaling
* Minimal data migration
* No downtime scaling

---

# 🧠 7️⃣ Handling Group Messages at Scale

Problem:
Group of 10K users → 1 message

Two strategies:

---

## Fan-Out on Write (WhatsApp uses this)

```
1 message →
   copy into each user's inbox
```

Stored as:

```
userId + messageId
```

### Why?

* Fast read
* No heavy aggregation during fetch

Tradeoff:

* Higher write amplification

At WhatsApp scale:
Reads > Writes → So optimize reads.

---

# 🧱 8️⃣ Logical Data Model (Inbox Model)

Instead of storing single group copy:

We store:

```
UserInbox Table

Partition Key: userId
Clustering Key: timestamp
Columns:
  messageId
  chatId
  encryptedPayload
  status
```

Each user fetches from own shard.

---

# 🔥 9️⃣ Avoiding Hot Shards

We prevent hotspots via:

### 1️⃣ Virtual Nodes

Each physical node hosts multiple token ranges.

### 2️⃣ Dynamic Rebalancing

Monitor load → move tokens.

### 3️⃣ Rate Limiting Large Groups

Prevent spam storms.

---

# 🌍 1️⃣0️⃣ Multi-Region Strategy

We use:

* Region-based sharding
* User affinity routing

Example:

```
India users → India cluster
Europe users → EU cluster
```

Messages cross-region via async replication.

---

# 🔁 1️⃣1️⃣ Replication Strategy

We use:

Replication Factor = 3

Across:

* AZ1
* AZ2
* AZ3

Ensures:

* High availability
* Read availability during node failure

---

# ⚡ 1️⃣2️⃣ Read Optimization

We use:

* Read replicas
* Redis cache for recent chats
* Pagination (limit 50 messages)

Query pattern:

```
SELECT * 
FROM UserInbox
WHERE userId = ?
ORDER BY timestamp DESC
LIMIT 50
```

Highly efficient in Cassandra.

---

# 📊 1️⃣3️⃣ Write Optimization

Messages are:

* Append-only
* No updates (except status)
* No joins

This keeps:

* Write latency low
* Locking minimal

---

# 🔐 1️⃣4️⃣ Encryption Compatibility

Since payload encrypted:

DB does NOT need:

* Content indexing
* Text search

Only stores:

* Binary blobs

Improves performance.

---

# 🧠 1️⃣5️⃣ Scaling to 1 Billion Users

Key strategies:

* Auto-scaling DB nodes
* Partition key carefully chosen
* Compact storage format
* Background compaction
* Time-based archiving (cold storage)

Old messages → moved to cheaper storage.

---

# ⚖ 1️⃣6️⃣ Tradeoffs Discussion (Interview Gold)

| Decision             | Tradeoff              |
| -------------------- | --------------------- |
| Fan-out on write     | High write cost       |
| NoSQL over SQL       | No joins              |
| Eventual consistency | Faster availability   |
| Shard by chatId      | Risk of group hotspot |
| Hybrid model         | More infra complexity |

---

# 🧠 1️⃣7️⃣ Failure Handling

If shard fails:

* Replica takes over
* Kafka replay restores missed writes
* Idempotent message IDs prevent duplicates

---

# 🎯 Final Production Sharding Strategy

✔ Partition by chatId
✔ User-based inbox for fast read
✔ Consistent hashing
✔ Multi-AZ replication
✔ Fan-out on write
✔ Append-only model
✔ Encrypted blob storage

---

# 🚀 How to Explain in Interview

Say:

> “At WhatsApp scale, message storage is write-heavy and read-critical. I would use Cassandra with partition key as chatId, clustering by timestamp, and implement fan-out-on-write to user inbox tables. Shards would be distributed via consistent hashing with replication factor 3 across availability zones to ensure high availability and fault tolerance.”

That sounds senior-level.

---

