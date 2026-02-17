## 🔹 What is Sharding?

**Sharding is a database scaling technique where large data is split horizontally across multiple machines (called shards) to distribute load and storage.**

Instead of:

```
1 massive database
```

We do:

```
Shard 1 → Part of data
Shard 2 → Part of data
Shard 3 → Part of data
```

Each shard stores a **subset of rows**, not a copy of the whole database.

---

# 🧠 Simple Example

Suppose we have 1 billion users.

Instead of storing all in one DB:

```
Shard 1 → Users 1–250M
Shard 2 → Users 250M–500M
Shard 3 → Users 500M–750M
Shard 4 → Users 750M–1B
```

Now:

* Load is distributed
* Writes are parallel
* Storage is distributed

---

# 🔹 What Exactly Gets Split?

👉 Rows, not columns
This is called **horizontal partitioning**.

Example:

Original table:

| userId | name |
| ------ | ---- |

After sharding:

Shard A:
| userId 1–1M |

Shard B:
| userId 1M–2M |

---

# 🔥 Why We Need Sharding

Because a single DB has limits:

* CPU limit
* RAM limit
* Disk IOPS limit
* Write throughput limit

At large scale (WhatsApp, Instagram, Amazon), one DB cannot handle the load.

---

# 🔹 How Data Is Assigned to Shards

Using a **shard key**.

Example:

```
shard = hash(userId) % N
```

This decides which shard stores the data.

Shard key must:

* Evenly distribute data
* Avoid hotspots
* Be frequently used in queries

---

# 🔹 Sharding vs Replication

Very important difference:

| Sharding                      | Replication                |
| ----------------------------- | -------------------------- |
| Splits data                   | Copies data                |
| Increases capacity            | Increases availability     |
| Each shard has different data | Each replica has same data |

Production systems use **both together**.

---

# 🔹 Real-World Example

In messaging app:

If we shard by `chatId`:

```
Chat A → Shard 1
Chat B → Shard 3
Chat C → Shard 2
```

All messages of a chat live in one shard.

---

# 🔹 When Do We Use Sharding?

When:

* Data size is huge (TBs–PBs)
* Write-heavy workload
* Millions of concurrent users
* Low latency required globally

---

# 🔥 One-Line Interview Definition

> Sharding is a horizontal scaling technique where a large database is split into smaller, independent databases called shards, each storing a subset of data based on a shard key.

---
Now we move from “what” to **how to do it correctly at scale**.

---

# 🟢 1️⃣ Types of Sharding Strategies

There are 4 real strategies used in production.

---

## 🔹 A. Range-Based Sharding

Data split by value range.

Example:

```
Shard 1 → userId 1–1M
Shard 2 → userId 1M–2M
```

### ✅ Pros

* Simple
* Easy range queries

### ❌ Cons

* Hotspot risk (new users always in last shard)
* Uneven distribution

Used when:

* Predictable growth
* Sequential queries needed

---

## 🔹 B. Hash-Based Sharding (Most Common)

```
shard = hash(userId) % N
```

### ✅ Pros

* Even distribution
* Prevents hotspots

### ❌ Cons

* Harder range queries
* Resharding painful if N changes

Used in:

* Messaging systems
* User services

---

## 🔹 C. Directory-Based Sharding

Lookup table decides shard.

```
userId → shardMap[userId]
```

### ✅ Pros

* Flexible
* Easy migration
* Fine-grained control

### ❌ Cons

* Extra lookup cost
* Directory becomes critical component

Used in:

* Large-scale custom systems

---

## 🔹 D. Consistent Hashing (Advanced)

Uses hash ring instead of modulo.

Benefits:

* Minimal data reshuffling when adding nodes
* Better dynamic scaling

Used in:

* Cassandra
* Dynamo-style systems

---

# 🟢 2️⃣ How to Choose a Shard Key

This is where most systems fail.

A good shard key must:

### ✔ High Cardinality

Millions of unique values.

Bad:

```
country
```

Good:

```
userId
chatId
```

---

### ✔ Even Distribution

Avoid skew.

If one key value generates 90% traffic → hotspot.

---

### ✔ Query Alignment

Shard key must match common query pattern.

If queries are:

```
fetch messages by chatId
```

Then shard by chatId.

If queries are:

```
fetch user inbox
```

Then shard by userId.

---

### ✔ Immutable

Shard key should never change.

Changing it means data migration nightmare.

---

### ✔ Avoid Sequential Growth Bias

If using range sharding:

* Don’t use auto-increment ID
* Use random UUID or hashed value

---

# 🟢 3️⃣ Sharding Problems & Pitfalls

This is where real engineering begins.

---

## 🔥 1. Hot Shards

One shard gets more traffic than others.

Example:

* Large group chat
* Celebrity account

Solution:

* Virtual nodes
* Adaptive rebalancing
* Rate limiting

---

## 🔥 2. Resharding Complexity

When scaling from 10 → 20 shards:

With modulo hashing:

```
hash(key) % N
```

Almost all data must move.

Solution:

* Consistent hashing
* Directory-based sharding

---

## 🔥 3. Cross-Shard Queries

If data needed from multiple shards:

* Joins become expensive
* Aggregations slow

Solution:

* Denormalization
* Precomputed views
* Fan-out on write

---

## 🔥 4. Transactions Across Shards

Distributed transactions are slow and complex.

Solution:

* Avoid cross-shard transactions
* Use eventual consistency
* Use Saga pattern

---

## 🔥 5. Operational Complexity

More shards =

* More monitoring
* More backups
* More replication management
* More failure handling

Scaling infra complexity grows exponentially.

---

## 🔥 6. Rebalancing Downtime

Moving data between shards can:

* Impact performance
* Cause inconsistency

Solution:

* Background migration
* Dual writes
* Traffic draining

---

# 🟢 4️⃣ Sharding vs Partitioning (Deep Difference)

People confuse these.

They are NOT the same.

---

## 🔹 Partitioning

* Happens inside single database instance
* Logical split
* Same machine
* Same storage

Example:

```
CREATE TABLE messages
PARTITION BY RANGE(timestamp);
```

Data still in same DB server.

Used for:

* Query optimization
* Manage large tables

---

## 🔹 Sharding

* Happens across multiple machines
* Physical split
* Independent databases

Used for:

* Horizontal scaling
* Capacity increase
* High availability

---

# 🔥 Comparison Table

| Partitioning               | Sharding                      |
| -------------------------- | ----------------------------- |
| Single DB instance         | Multiple DB instances         |
| Improves query performance | Improves scalability          |
| Easier to manage           | Operationally complex         |
| No network overhead        | Network coordination required |
| Same hardware              | Distributed hardware          |

---

# 🧠 Real-World Insight

At small scale:

* Partitioning is enough

At WhatsApp scale:

* Sharding is mandatory

Most companies:

1. Start with partitioning
2. Then move to sharding
3. Then add consistent hashing
4. Then multi-region replication

---

# 🎯 Interview-Ready Summary

If asked:

“What are types of sharding?”

Say:

> Range-based, Hash-based, Directory-based, and Consistent Hashing. At large scale, consistent hashing with replication is preferred to avoid massive reshuffling during scaling.

If asked:

“How to choose shard key?”

Say:

> High cardinality, evenly distributed, immutable, aligned with query pattern, and avoids hotspot risk.

If asked:

“Difference between sharding and partitioning?”

Say:

> Partitioning is logical split within one DB instance, while sharding is physical distribution across multiple independent database nodes.

---


