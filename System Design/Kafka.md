# 🔵 What is Kafka?

**Kafka is a distributed event streaming platform.**

It is used to:

* Handle high-throughput data streams
* Decouple services
* Enable asynchronous processing
* Build real-time pipelines

Kafka is not just a message queue.
It is a **distributed commit log system**.

---

# 🔵 Core Idea

Instead of:

Service A → directly calls → Service B

We do:

Service A → publishes event → Kafka → Service B consumes event

This makes systems:

* Loosely coupled
* Scalable
* Fault tolerant

---

# 🔵 Core Concepts

---

## 1️⃣ Producer

Component that sends messages to Kafka.

It writes events to a topic.

---

## 2️⃣ Consumer

Component that reads messages from Kafka.

Multiple consumers can read independently.

---

## 3️⃣ Topic

A logical stream of events.

Example conceptually:

* orders
* payments
* notifications

A topic is like a category of messages.

---

## 4️⃣ Partition

Each topic is divided into partitions.

Why?

* Parallel processing
* Horizontal scalability

Each partition is:

* Ordered
* Append-only
* Stored on disk

Order is guaranteed only within a partition.

---

## 5️⃣ Broker

A Kafka server.

Kafka cluster = multiple brokers.

Each broker stores partitions.

---

## 6️⃣ Consumer Group

Multiple consumers can form a group.

Kafka distributes partitions across consumers.

Important:

* One partition → consumed by only one consumer in a group
* Enables parallel processing

---

## 7️⃣ Offset

Each message has a sequential ID called offset.

Consumers track offset to know:

* What they have processed
* Where to resume after crash

---

# 🔵 Architecture Model

High-level flow:

Producer
→ Topic
→ Partition
→ Broker
→ Consumer Group

Kafka persists data to disk and replicates across brokers.

---

# 🔵 Why Kafka is Powerful

---

## 1️⃣ High Throughput

* Millions of messages per second
* Sequential disk writes (very fast)

---

## 2️⃣ Horizontal Scalability

* Add more brokers
* Add more partitions
* Increase parallelism

---

## 3️⃣ Durability

* Messages written to disk
* Replicated across brokers
* Survive node failures

---

## 4️⃣ Fault Tolerance

Each partition has:

* Leader
* Followers

If leader fails:

* Follower becomes leader

---

## 5️⃣ Decoupling

Producers and consumers don’t know each other.

They communicate only via topics.

This allows independent scaling.

---

# 🔵 Kafka vs Traditional Message Queue

| Traditional Queue           | Kafka                 |
| --------------------------- | --------------------- |
| Messages deleted after read | Messages retained     |
| Pull-based mostly           | Pull-based            |
| Limited replay              | Full replay support   |
| Lower throughput            | Very high throughput  |
| Queue model                 | Distributed log model |

Kafka keeps data for configurable time.

Consumers can re-read old data.

---

# 🔵 Delivery Guarantees

Kafka supports:

* At most once
* At least once
* Exactly once (with configuration)

---

# 🔵 When to Use Kafka

Use Kafka when:

* High volume of events
* Need decoupling
* Need event replay
* Need stream processing
* Need scalable async processing

Avoid Kafka when:

* Very low traffic
* Simple request-response system
* No async need

---

# 🔵 Real Architectural Uses

Kafka is used for:

* Event-driven architecture
* Microservices communication
* Log aggregation
* Real-time analytics
* Activity tracking
* Background processing pipelines

---

# 🔵 Important Design Considerations

---

## Partition Count

More partitions = more parallelism
But too many = overhead.

---

## Ordering

Guaranteed only within a partition.
Choose partition key carefully.

---

## Replication Factor

Higher replication = better durability
But more network cost.

---

## Retention Policy

* Time-based
* Size-based

Controls storage growth.

---

# 🔵 Common Challenges

* Hot partitions
* Consumer lag
* Rebalancing overhead
* Large message size issues
* Schema evolution problems

---

# 🔵 Architectural Thinking

Kafka is best viewed as:

A durable, distributed event backbone.

It connects independent services at scale.

It is not a database.
It is not a simple queue.
It is a distributed streaming log.

---
Now we go deep.
Pure **Kafka internals** — architecture, storage model, replication, and message flow.

---

# 🟢 1️⃣ Kafka High-Level Internal Architecture

![Image](https://daxg39y63pxwu.cloudfront.net/images/blog/apache-kafka-architecture-/image_589142173211625734253276.png)

![Image](https://dz2cdn1.dzone.com/storage/temp/14018525-kafka-architecture-topics-replication-to-partition-0.png)

![Image](https://developers.redhat.com/sites/default/files/RHOSAK%20LP1%20Fig4.png)

![Image](https://media.licdn.com/dms/image/v2/D5612AQEz3BPwHTJdSA/article-cover_image-shrink_600_2000/article-cover_image-shrink_600_2000/0/1709743981368?e=2147483647\&t=AjH6AsIGiSB-k4pwfLBq-pOSiSAteNF-QJDRya0uoto\&v=beta)

Core components:

* Producers
* Brokers
* Topics
* Partitions
* Consumers
* Zookeeper (legacy) / KRaft (modern metadata quorum)

Kafka = Distributed log system across brokers.

---

# 🟢 2️⃣ Kafka Storage Internals (Commit Log)

Kafka is fundamentally an **append-only log**.

Each partition is:

* A sequence of immutable records
* Stored on disk
* Indexed by offset

Structure:

```
Topic
  └── Partition 0
        ├── segment-0001.log
        ├── segment-0002.log
        └── index files
```

Important:

* Writes are sequential
* Sequential disk writes are extremely fast
* No in-place updates

---

# 🟢 3️⃣ Log Segments

Kafka doesn’t keep one giant file.

It splits partitions into segments.

Each segment has:

* `.log` file → actual messages
* `.index` file → offset to file position
* `.timeindex` file → timestamp lookup

Benefits:

* Easier retention cleanup
* Efficient disk management
* Faster lookup

---

# 🟢 4️⃣ Producer Internals

Producer workflow:

1. Serialize message
2. Choose partition
3. Batch messages
4. Send to broker leader
5. Wait for acknowledgment

Partition selection:

* Round-robin
* Key-based hashing
* Custom partitioner

Batching is critical for performance.

---

# 🟢 5️⃣ Partition Leadership

![Image](https://media.licdn.com/dms/image/v2/D5612AQEz3BPwHTJdSA/article-cover_image-shrink_600_2000/article-cover_image-shrink_600_2000/0/1709743981368?e=2147483647\&t=AjH6AsIGiSB-k4pwfLBq-pOSiSAteNF-QJDRya0uoto\&v=beta)

![Image](https://miro.medium.com/1%2AYCJipz7DoweC6R7n15JdGQ.png)

![Image](https://miro.medium.com/0%2AVhn-nT7sMF0DOljT)

![Image](https://images.squarespace-cdn.com/content/v1/56894e581c1210fead06f878/1535902300576-U5MZB0GH8KXYS19BPC5H/KafkaPartitionFailOver1.PNG)

Each partition has:

* 1 Leader
* N Followers

Only leader:

* Accepts writes
* Serves reads (by default)

Followers:

* Replicate data
* Stay in sync

---

# 🟢 6️⃣ ISR (In-Sync Replicas)

ISR = replicas fully caught up with leader.

If leader fails:

* Kafka elects new leader from ISR
* Prevents data loss

Replication factor example:

RF = 3
→ 1 leader + 2 followers

---

# 🟢 7️⃣ Replication Mechanism

Followers:

* Pull data from leader
* Append to their log
* Send acknowledgment

Producer acks configuration:

* acks=0 → fire and forget
* acks=1 → leader confirms
* acks=all → all ISR confirm (strongest)

---

# 🟢 8️⃣ Consumer Internals

Consumers:

* Pull messages
* Track offsets
* Commit offsets periodically

Kafka does NOT track read state automatically.

Consumer stores offset in:

* Kafka internal topic (`__consumer_offsets`)

This allows:

* Restart recovery
* Exactly-once processing (with config)

---

# 🟢 9️⃣ Consumer Group Rebalancing

If:

* New consumer joins
* Consumer crashes
* Partition count changes

Kafka triggers rebalance.

Process:

1. Stop consumption
2. Redistribute partitions
3. Resume consumption

This ensures:

* One partition per consumer per group

---

# 🟢 🔟 Zero-Copy Optimization

Kafka uses:

* sendfile system call

Data moves:

Disk → Network
Without copying into user-space.

This reduces:

* CPU usage
* Memory overhead

Enables massive throughput.

---

# 🟢 1️⃣1️⃣ Page Cache Usage

Kafka relies heavily on OS page cache.

Why?

* Recent messages cached in memory
* Reads are fast
* No complex in-memory structure required

Kafka is disk-based but memory-accelerated.

---

# 🟢 1️⃣2️⃣ Retention & Cleanup

Kafka supports:

### Time-based retention

Keep messages for X hours/days

### Size-based retention

Keep up to Y GB

Cleanup methods:

* Delete policy
* Log compaction (keep latest key)

Log compaction is used for:

* State topics
* Key-value semantics

---

# 🟢 1️⃣3️⃣ Metadata Management

Old versions:

* Used ZooKeeper

Modern Kafka:

* Uses KRaft (Kafka Raft)

KRaft manages:

* Topic metadata
* Partition metadata
* Leader election
* Cluster state

Removes ZooKeeper dependency.

---

# 🟢 1️⃣4️⃣ Exactly-Once Semantics (Internally)

Kafka uses:

* Idempotent producer
* Transaction coordinator
* Producer ID tracking

Prevents:

* Duplicate writes
* Partial commits

Used in financial systems.

---

# 🟢 1️⃣5️⃣ Performance Internals

Kafka achieves high performance due to:

* Sequential writes
* Batching
* Zero-copy transfer
* Page cache reliance
* Pull-based consumption
* Partition parallelism

Throughput scales with:

* Number of partitions
* Number of brokers
* Network bandwidth

---

# 🟢 1️⃣6️⃣ Internal Data Flow

Producer → Leader partition
Leader → Followers
Followers → ISR
Consumer pulls from leader
Offsets committed
Retention cleans segments

All happening continuously and asynchronously.

---

# 🟢 1️⃣7️⃣ Failure Handling Internals

If broker fails:

* Controller detects failure
* Elects new leader from ISR
* Updates metadata
* Clients auto-refresh metadata

No global downtime.

---

# 🟢 1️⃣8️⃣ Key Internal Guarantees

Kafka guarantees:

* Ordering per partition
* Durable persistence
* Configurable consistency
* Horizontal scalability
* Replay capability

It does NOT guarantee:

* Global ordering
* Cross-partition transactions by default

---

# 🟢 Final Internal Model Summary

Kafka is:

* Distributed append-only log
* Partitioned
* Replicated
* Leader-based
* Pull-driven
* Disk-backed
* Horizontally scalable

It is optimized for:

High-throughput, fault-tolerant, real-time streaming systems.

---
