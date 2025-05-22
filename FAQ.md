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
