# Salesforce Queue Setup Explained

## What is a Queue?
A **Queue** is a holding place for work items (like Cases, Leads, or custom objects) that need to be assigned to users or teams. Queues help organize work so it can be efficiently routed and managed.

---

## Step-by-Step Queue Setup Guide

### 1. Create a Queue
- **Why?**  
  You need a place to collect work items before they get assigned or routed. Omni-Channel and manual assignment pull work from queues.
  
- **What happens if you skip?**  
  Work items won’t have a holding place, making it difficult to assign and track tasks efficiently.
  
- **How to do it:**  
  - Go to **Setup** → **Queues** → **New**  
  - Enter a **Queue Name** (e.g., "High Priority Cases")  
  - Optionally add a **Queue Email** for notifications when items are assigned to the queue  
  - Select **Supported Objects** — the objects whose records can be assigned to this queue (e.g., Case, Lead)  
  - Add **Queue Members** — users, roles, or public groups who can own or take work from this queue  
  
---

### 2. Queue Email Address
- **What is it?**  
  An email address used for sending notifications about items assigned to the queue.
  
- **Why use it?**  
  To keep queue members informed when new work arrives or when work is assigned.
  
- **What if you skip?**  
  No email notifications will be sent when work is assigned to the queue.
  
- **Example:**  
  Use a distribution list email (e.g., support-team@example.com) so all team members get notified.

---

### 3. Supported Objects
- **What is it?**  
  Specifies which Salesforce objects’ records can be assigned to this queue.
  
- **Why select it?**  
  You want to control which object records belong to this queue (e.g., Cases, Leads, or custom objects).
  
- **What if you skip?**  
  You can’t assign records of unsupported objects to the queue.
  
- **Example:**  
  For a Case support team, select **Case** as the supported object.

---

### 4. Queue Members
- **What is it?**  
  Users, roles, or public groups that can take ownership or receive notifications for items in the queue.
  
- **Why add members?**  
  Only members can be assigned work or notified about queue activity.
  
- **What happens if you skip?**  
  No one can take ownership of records assigned to this queue.

---

### 5. Linking Queue to Routing Configuration (Omni-Channel)
- **What is it?**  
  Routing Configurations define how Omni-Channel routes work from queues to agents.
  
- **Why link?**  
  This enables Omni-Channel to push work from the queue to agents with routing logic (priority, capacity).
  
- **What if you skip?**  
  The queue will hold work but Omni-Channel won’t route it automatically to agents.
  
- **How to do it:**  
  - Edit the queue  
  - In the **Routing Configuration** lookup, select an existing routing configuration that defines routing behavior for this queue.

---

### 6. Example Use Case

- **Scenario:** You create a queue named **"Support Queue"** for Case objects.
- You add your support team roles as members.
- You provide a queue email like support-team@example.com for notifications.
- You link this queue to a routing configuration named **"Support Routing Config"** that prioritizes urgent cases and balances workload.
  
**Outcome:**  
New Cases assigned to the "Support Queue" notify the team via email and are automatically routed to available agents using Omni-Channel routing rules.

---

## Summary

| Step                        | Why                                | What if skipped                    | How to do it                               |
|-----------------------------|-----------------------------------|----------------------------------|--------------------------------------------|
| Create Queue                | Hold work items before assignment | No place to organize work         | Setup → Queues → New                        |
| Set Queue Email             | Notify members of new assignments | No email notifications            | Add email on queue setup                    |
| Select Supported Objects    | Define which object records to hold| Can't assign unsupported objects  | Choose objects in queue setup               |
| Add Queue Members           | Define who can own/take work      | No one can take queue records     | Add users, roles, or groups as members      |
| Link Routing Configuration | Enable Omni-Channel auto routing  | Work won't be routed automatically| Edit queue → Assign routing config          |

---

*This guide helps you understand how to set up queues properly in Salesforce, link them with routing configurations, and ensure your team receives and manages work effectively.*
