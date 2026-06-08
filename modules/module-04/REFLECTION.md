# Module 4 — Reflection

**Team name**: _______________
**Branch**: `module-04/<team-name>`
**Submitted**: before Module 5 lesson

---

Answer the three questions below. There are no right or wrong answers — we are looking for your reasoning, not a textbook definition. A few honest sentences are worth more than a long generic paragraph.

---

## 1. The "why"

In Module 3, services called each other directly over HTTP. Now activity-service drops a message into a broker and moves on — it never waits for a reply.

**What does the activity-service gain by not waiting? And what does the notification-service gain by consuming at its own pace?**

Think about what happens under load, or when notification-service is temporarily down.

By not waiting for a reply, activity-service can respond to the user immediately after saving the activity. Notifs service process messages at its own pace. and if it goes down temporarily, the messages just wait in the queue and get processed when it comes back up.

---

## 2. Your choice

In Module 3 you already knew how to call another service directly over HTTP — you did it for user validation and game enrichment.

**Why not use the same approach for notifications? What does introducing a broker give you that a direct HTTP call doesn't?**

Think about what happens if notification-service is slow, or crashes mid-message.

A direct HTTP call means activity service has to wait for notification-service to respond, and if notifs service is slow or crashes, the whole activity creation could fail. A broker decouples them completely sso tivity service just drops the message and moves on. If notification-service crashes, the message stays in the queue safely. 

---

## 3. The tradeoff

With synchronous REST, you get an immediate answer: success or failure. With async messaging, the activity is saved and the message is sent — but you have no idea if the notification was ever delivered.

**How would a user know if their notification was never sent? How would you know as a developer?**

What visibility do you lose when you go async?

A user doesn't know. the activity creation returns success regardless of whether the notification was ever delivered. 

---

*Keep this file. You will refer back to it during the oral presentation.*
