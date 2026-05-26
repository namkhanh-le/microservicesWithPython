# Module 3 — Reflection

**Team name**: namkhanh-le
**Branch**: `module-03/<namkhanh-le>`
**Submitted**: before Module 4 lesson

---

Answer the three questions below. There are no right or wrong answers — we are looking for your reasoning, not a textbook definition. A few honest sentences are worth more than a long generic paragraph.

---

## 1. The "why"

All client requests now go through the gateway. No client ever calls a service directly.

**Why does that single entry point exist? What would the client's life look like without it?**

Think about what the client would need to know and manage if it talked to each service on its own port.

> Without gateway, client would need to know address and port of every individual service. If any service moves or gets scaled, the client would need to be updated too. The gateway gives the client one stable address to talk to, and handles routing internally. 

---

## 2. Your choice

The activity-service makes two outbound calls: one to validate the user (with retry logic), one to fetch game data (with a null fallback if it fails).

**Why are these two calls treated differently? Why does one retry and the other just give up gracefully?**

What is the consequence for the user in each case if the downstream service is unavailable?

> user validation is critical. so if we cant confirm the user exists, saving the activity would be an activity with no real owner. So it's worth retrying in case the failure is temporary, and blocking if it keeps failing. game data is just extra context for the response. activity itself is still valid without it. Blocking on a missing game would mean a working feature fails for an unrelated reason, which is a worse outcome than just returning null.

---

## 3. The tradeoff

Every time a client creates an activity, three services are involved synchronously. They all have to be running, healthy, and fast.

**What is the systemic risk of chaining synchronous calls like this?**

What happens to the user experience if the slowest service in the chain takes 3 seconds to respond?

> If three services are synch, total response time is the sum. the systematic risk is that the more you have the more fragile and slow.
if slowest service takes 3 seconds to response, it means the others take at most 3 seconds, so the user waits at most 3 seconds for each
services.


**Note**: user service and game service seed data was not available on this device because I messed up. I fetched and merged your repo down THE DAY you updated it for module 4. And I can't revert back. The gateway and activity-service implementations are complete and correct but obviously there's empty stuff. There also may be edited stuff in places that shouldn't be edited because I pulled some stuff from my completed module 2 set up, just for me to complete the task for this specific exercise, which is the gateway. game service schema differences prevented full end-to-end testing of steps 6 and 7 and I couldn't test it. It makes no difference in the final push but yeah, that's the problem for now. Sorry professor!

---

*Keep this file. You will refer back to it during the oral presentation.*
