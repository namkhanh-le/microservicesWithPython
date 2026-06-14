# Module 5 — Reflection

**Team name**: _______________
**Branch**: `module-05/<team-name>`
**Submitted**: before Module 6 lesson

---

Answer the three questions below. There are no right or wrong answers — we are looking for your reasoning, not a textbook definition. A few honest sentences are worth more than a long generic paragraph.

---

## 1. The "why"

The game-service now has two models for the same data: SQLite for writes, Redis for reads. They store the same games in two different shapes.

**Why go through the trouble of maintaining two representations of the same data?**

Think about what kind of queries each model is optimised for, and what would happen if you tried to use the write model for high-traffic read operations.

SQLite is optimised for accurate writes for storing the authoritative version of a game.Maintaining two representations lets me serve reads at scale without putting pressure on the write model.

---

## 2. Your choice

The logging-service checks GDPR consent before recording any activity. If a user has not opted in, the log is silently dropped.

**What does this consent check force you to accept about your data?** It is incomplete by design — some activities will never be recorded.

From a system design perspective: where is the right place to enforce this rule — in the logging-service, in the activity-service, or at the gateway? Why?

It forces you to accept that your data will always be incomplete. The right place to enforce this rule is in the logging-service, not at the gateway or activity service. =

---

## 3. The tradeoff

With CQRS, your write model and read model can drift out of sync — a game is updated in SQLite but the Redis projection still shows the old data.

**In what scenario does this inconsistency matter to the user? In what scenario is it completely acceptable?**

Is there a class of applications where eventual consistency is never acceptable? What are they?

It matters when a user updates something and expects to see the change immediately. Applications where eventual consistency is never acceptable include anything involving money inventory medical records or legal data 

---

*Keep this file. You will refer back to it during the oral presentation.*
