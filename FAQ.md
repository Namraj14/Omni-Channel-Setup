## Why do we select objects in both Queue and Service Channel?

- In **Queue**, selecting objects defines which records can be **assigned to and held in the queue**.
- In **Service Channel**, selecting objects defines which records Omni-Channel will **route from the queue to agents**.

**Example:**  
You select **Case** in the queue so Cases can be assigned there. You also select **Case** in the service channel so Omni-Channel knows to route those Cases to agents.

---

## What happens if I select an object in Queue but not in Service Channel?

The queue can hold the records of that object type, but Omni-Channel will **NOT** route these records to agents because it doesn’t know to route them.

**Example:**  
You have a queue that supports Cases, but no service channel for Cases. Cases get assigned to the queue but will just sit there — agents won’t get them routed via Omni-Channel.

---

## What happens if I select an object in Service Channel but not in Queue?

This is generally not valid, because Omni-Channel routes work items from queues. If the queue does not support that object, the records can’t be assigned to the queue in the first place.

**Example:**  
If the queue doesn’t support Cases, but the service channel does, Cases cannot be assigned to the queue, so there is nothing to route.

---

## Summary:

| Feature            | What it controls                           | What happens if missing                          |
|--------------------|-------------------------------------------|-------------------------------------------------|
| **Queue**          | Which record types the queue holds/owns  | Records cannot be assigned to the queue          |
| **Service Channel** | Which record types Omni-Channel routes from the queue | Omni-Channel won’t route work items to agents |

---

## Final Notes:

- Always create a **Queue** with supported objects first to hold records.
- Then create a **Service Channel** with the same objects to enable Omni-Channel routing.
- Link the **Routing Configuration** to the queue to control routing priority and capacity.


## 🧠 Hidden Gems & Unexpected FAQs – Omni-Channel (Salesforce)

These are advanced, overlooked, or real-world questions Salesforce admins and developers *should* ask, but often don’t.

---

### ❓ What happens if two queues use the same routing configuration?

Nothing breaks, but:
- The **same priority logic** will apply to both queues.
- This is useful if both queues should route items equally.
- Be careful: changing the config later affects **all linked queues**.

---

### ❓ Can I assign different capacity units to different types of work?

Yes!
- Go to **Routing Configuration**, and set different capacities per config.
- Example: 
  - Case: 5 units
  - Chat: 1 unit  
  - Custom Object: 3 units  
- Agent's total load is calculated across all work items.

---

### ❓ What if an agent is in two Presence Configurations?

They **can’t be**.  
- Each user can only have **one** Presence Configuration via their **profile**.
- Multiple configs? Use **permission sets + cloned profiles** strategically.

---

### ❓ Why is Omni-Channel not assigning work even when agents are online?

Check for:
- ❌ Work not assigned to a **queue**
- ❌ Queue is not connected to a **routing config**
- ❌ Missing **Service Channel**
- ❌ Presence Status not mapped to Service Channel
- ❌ Agent's profile not mapped to Presence Config
- ✅ Omni widget is **not open** in console → it must be!

---

### ❓ Can I route records from a **custom object**?

Yes!
- Just create a **Service Channel** for your custom object.
- Assign it to a queue → link with routing config → done.
- You can route `Inspection__c`, `Application__c`, etc.

---

### ❓ What if I delete a Presence Status?

- All references to that status will break silently.
- Agents might go "Available", but won't get routed.
- **Always audit presence statuses before deletion.**

---

### ❓ Can agents receive work *outside* the console (like on mobile)?

No.
- Omni-Channel routing **requires the widget** to be active.
- Mobile & non-console apps **do not support** routed work items.

---

### ❓ Can we route work based on skill or language?

Yes – but only with **Omni-Channel Skills-Based Routing**:
- You need:
  - Skill entity setup
  - Agent-to-skill assignments
  - Queue filters
- Requires extra setup, and only in **Enterprise+** editions.

---

### ❓ Can I simulate a routing test?

Not officially.
- But you can:
  - Create a test record in the Queue
  - Watch Omni-Channel widget
  - Use Developer Console → Query `AgentWork`
- Use `debug logs` to inspect routing behavior.

---

### ❓ How do I track which agent accepted which work?

Use the `AgentWork` object:
```sql
SELECT Id, WorkItemId, UserId, Status, CreatedDate FROM AgentWork
