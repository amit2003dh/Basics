# 🟢 LLD Design — WhatsApp (Production-Level Thinking)

We design **core WhatsApp features**:

* 1–1 Messaging
* Group Messaging
* Message Status (sent/delivered/read)
* Online/Last Seen
* Media Support
* Notifications

Focus = **class design, interactions, data model, extensibility**

---

# 1️⃣ Core Entities

```
User
Chat
Message
Group
Media
Notification
Session
```

---

# 2️⃣ Class Design

---

## 🧑 User

```java
class User {
    private String userId;
    private String name;
    private String phoneNumber;
    private UserStatus status;  // ONLINE, OFFLINE
    private List<Session> activeSessions;

    public void sendMessage(Chat chat, Message message);
    public void receiveMessage(Message message);
}
```

Responsibilities:

* Send/receive messages
* Manage presence
* Maintain sessions

---

## 💬 Chat (Abstract)

```java
abstract class Chat {
    protected String chatId;
    protected List<User> participants;
    protected List<Message> messages;

    public abstract void sendMessage(Message message);
}
```

Why abstract?

* Supports 1–1 and Group chats

---

## 👥 PrivateChat

```java
class PrivateChat extends Chat {

    @Override
    public void sendMessage(Message message) {
        // deliver to single recipient
    }
}
```

---

## 👨‍👩‍👧‍👦 GroupChat

```java
class GroupChat extends Chat {
    private String groupName;
    private User admin;

    public void addMember(User user);
    public void removeMember(User user);

    @Override
    public void sendMessage(Message message) {
        // broadcast to all members
    }
}
```

---

# 3️⃣ Message Design

```java
class Message {
    private String messageId;
    private User sender;
    private MessageType type;  // TEXT, IMAGE, VIDEO
    private String content;
    private MessageStatus status; // SENT, DELIVERED, READ
    private long timestamp;

    public void updateStatus(MessageStatus status);
}
```

Enums:

```java
enum MessageType {
    TEXT, IMAGE, VIDEO, AUDIO
}

enum MessageStatus {
    SENT, DELIVERED, READ
}
```

---

# 4️⃣ Media Handling (Strategy Pattern)

We separate media logic.

```java
interface MediaHandler {
    String upload(byte[] file);
}
```

Implementations:

```java
class ImageHandler implements MediaHandler {}
class VideoHandler implements MediaHandler {}
```

Why?

* Easy to extend new media types
* Follows Open/Closed principle

---

# 5️⃣ Session Management

```java
class Session {
    private String deviceId;
    private String token;
    private boolean isActive;
}
```

Purpose:

* Multi-device login
* Track active sessions

---

# 6️⃣ Notification System (Observer Pattern)

When message arrives → notify receiver.

```java
interface NotificationObserver {
    void notify(User user, Message message);
}
```

Implementation:

```java
class PushNotificationService implements NotificationObserver {}
```

Why Observer?

* Decouples messaging from notification
* Can add email/SMS later

---

# 7️⃣ Message Delivery Flow

```
User A → sendMessage()
     ↓
Chat → validate participants
     ↓
MessageService
     ↓
Store in DB
     ↓
Push to recipient session (WebSocket)
     ↓
Update status SENT → DELIVERED → READ
```

---

# 8️⃣ Database Design (LLD Level)

## Users Table

```
user_id (PK)
name
phone_number
status
```

## Chats Table

```
chat_id (PK)
chat_type
```

## ChatParticipants

```
chat_id (FK)
user_id (FK)
```

## Messages

```
message_id (PK)
chat_id (FK)
sender_id (FK)
type
content
timestamp
status
```

---

# 9️⃣ Services Layer

We introduce service classes:

```
UserService
ChatService
MessageService
NotificationService
```

Example:

```java
class MessageService {

    public void sendMessage(User sender, Chat chat, String content) {
        Message message = new Message(...);
        chat.sendMessage(message);
        saveToDatabase(message);
        notifyUsers(message);
    }
}
```

---

# 🔟 Real-Time Communication

Use:

* WebSockets (full-duplex)
* Long polling fallback

Session stores:

```
userId → active socket connection
```

---

# 1️⃣1️⃣ Handling Read Receipts

When user opens chat:

```java
public void markAsRead(String messageId) {
    message.updateStatus(MessageStatus.READ);
}
```

Trigger status update event to sender.

---

# 1️⃣2️⃣ Concurrency Handling

Problems:

* Two users sending simultaneously
* Duplicate message delivery

Solutions:

* Unique message IDs (UUID)
* Idempotency keys
* DB transactions
* Message queue (Kafka)

---

# 1️⃣3️⃣ Design Patterns Used

| Pattern   | Where Used               |
| --------- | ------------------------ |
| Strategy  | Media handling           |
| Observer  | Notifications            |
| Singleton | DB connection            |
| Factory   | Message creation         |
| Builder   | Complex message creation |

---

# 1️⃣4️⃣ Edge Cases

✔ User offline → store message
✔ Message retry
✔ Group member removed
✔ Media upload failure
✔ Duplicate message prevention

---

# 1️⃣5️⃣ Extensibility Design

Future features:

* Voice calls → add CallService
* Disappearing messages → expiry field
* End-to-end encryption → EncryptionService
* Broadcast messages

LLD should allow extension without breaking existing code.

---

# 🔥 Clean Architecture Layering

```
Controller
   ↓
Service
   ↓
Repository
   ↓
Database
```

WebSocket Handler separate.

---

# 🎯 What Makes This LLD Strong?

✔ Abstraction used
✔ Design patterns applied
✔ Clear class responsibility
✔ Extensible
✔ Testable
✔ Production mindset

---

# 🟢 PART 1 — WhatsApp Status (Stories) LLD

## 🎯 Requirements

* User can upload image/video/text status
* Visible for 24 hours
* Only visible to contacts
* Seen status tracking
* Privacy control (My Contacts / Except / Only Share With)

---

# 1️⃣ Core Entities

```
Status
StatusView
PrivacySetting
```

---

## 📌 Status Class

```java
class Status {
    private String statusId;
    private User owner;
    private StatusType type;   // IMAGE, VIDEO, TEXT
    private String mediaUrl;
    private long createdAt;
    private long expiresAt;
    private List<StatusView> views;

    public boolean isExpired();
}
```

---

## 📌 StatusView (Tracks who viewed)

```java
class StatusView {
    private User viewer;
    private long viewedAt;
}
```

---

## 📌 Privacy Settings

```java
class PrivacySetting {
    private PrivacyType type; 
    private List<User> customUsers;
}

enum PrivacyType {
    MY_CONTACTS,
    MY_CONTACTS_EXCEPT,
    ONLY_SHARE_WITH
}
```

---

# 2️⃣ Status Service

```java
class StatusService {

    public Status createStatus(User user, String mediaUrl, StatusType type);

    public List<Status> getVisibleStatuses(User viewer);

    public void markAsViewed(String statusId, User viewer);
}
```

---

# 3️⃣ Expiry Mechanism

Two options:

### Option A — TTL Index (DB Level)

Database auto deletes after 24 hours.

### Option B — Scheduled Cleanup

Cron job checks `expiresAt`.

Better: TTL index (scalable).

---

# 4️⃣ Status Fetch Flow

```
Viewer opens status tab
        ↓
StatusService.getVisibleStatuses()
        ↓
Filter:
   - Not expired
   - Privacy allowed
        ↓
Return grouped by owner
```

---

# 5️⃣ DB Design

### Status Table

```
status_id (PK)
owner_id (FK)
type
media_url
created_at
expires_at
```

### StatusViews

```
status_id (FK)
viewer_id (FK)
viewed_at
```

---

# 6️⃣ Design Patterns Used

* Strategy → media handling
* Factory → create status by type
* Observer → notify contacts on upload

---

# 🟢 PART 2 — Call System LLD

We design:

* 1–1 audio call
* 1–1 video call
* Call states
* Call signaling
* Missed call notification

---

# 🎯 Requirements

* Real-time call setup
* Accept / Reject
* End call
* Missed call log
* Handle network drop

---

# 1️⃣ Core Entities

```
Call
CallSession
CallParticipant
SignalingService
```

---

## 📌 Call Class

```java
class Call {
    private String callId;
    private User caller;
    private User receiver;
    private CallType type; // AUDIO, VIDEO
    private CallStatus status;
    private long startTime;
    private long endTime;

    public void start();
    public void end();
}
```

---

## 📌 Enums

```java
enum CallType {
    AUDIO,
    VIDEO
}

enum CallStatus {
    INITIATED,
    RINGING,
    CONNECTED,
    REJECTED,
    MISSED,
    ENDED
}
```

---

## 📌 CallSession (WebRTC Session)

```java
class CallSession {
    private String sessionId;
    private Call call;
    private String signalingServer;
    private boolean isActive;
}
```

---

# 2️⃣ Signaling Service (Critical Component)

WebRTC needs signaling server.

```java
class SignalingService {

    public void initiateCall(User caller, User receiver);

    public void sendOffer(String callId, String offer);

    public void sendAnswer(String callId, String answer);

    public void sendICECandidate(String callId, String candidate);
}
```

---

# 3️⃣ Call Flow

```
Caller clicks call
      ↓
SignalingService.initiateCall()
      ↓
Receiver gets notification
      ↓
Receiver Accept / Reject
      ↓
If Accept:
   Exchange SDP Offer/Answer
      ↓
Establish WebRTC peer connection
      ↓
CallStatus → CONNECTED
```

---

# 4️⃣ Call Logs

### CallLog Table

```
call_id (PK)
caller_id
receiver_id
type
status
start_time
end_time
duration
```

---

# 5️⃣ Missed Call Logic

If:

* Receiver doesn’t answer in X seconds
* Or offline

Then:

```java
call.setStatus(CallStatus.MISSED);
NotificationService.notifyMissedCall();
```

---

# 6️⃣ Multi-Device Handling

* Call invitation sent to all active sessions
* First accepted session locks call

Use distributed lock.

---

# 7️⃣ Edge Cases

✔ Receiver offline
✔ Network drop mid-call
✔ User blocks caller
✔ Simultaneous call attempts
✔ Call timeout

---

# 8️⃣ Scalability Considerations

* Signaling via WebSocket
* Media via WebRTC (peer-to-peer)
* Use TURN servers for NAT traversal
* Rate limit call attempts

---

# 9️⃣ Design Patterns Used

| Pattern       | Usage                       |
| ------------- | --------------------------- |
| State Pattern | CallStatus transitions      |
| Observer      | Incoming call notifications |
| Singleton     | Signaling server manager    |
| Factory       | Call creation               |

---

# 🔥 Combined Architecture (Messages + Status + Calls)

```
Users
  ↓
API Gateway
  ↓
Auth Service
  ↓
Message Service
Status Service
Call Service
  ↓
DB + Cache
  ↓
WebSocket Server (Real-time)
  ↓
Push Notification Service
```

---

# 🎯 What Makes This Production-Level LLD?

✔ Extensible
✔ Real-time capable
✔ Handles concurrency
✔ Applies patterns
✔ Database modeled
✔ Edge cases covered

---
