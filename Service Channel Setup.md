# Salesforce Service Channel Setup Explained

## What is a Service Channel?
A **Service Channel** in Salesforce Omni-Channel is a configuration that routes work items from Salesforce objects (like Cases, Chats, Leads, or custom objects) to support agents. It acts as the bridge between the data (records) and the Omni-Channel routing engine.

---

## Step-by-Step Guide to Service Channel Setup

### 1. Create a Service Channel
- **Why?**  
  The Service Channel tells Omni-Channel which Salesforce object’s records will be routed to agents. It controls how work is delivered and how agents interact with it.
  (A Service Channel tells Omni-Channel what kind of records (Cases, Leads, custom objects, etc.) it should pay attention to and route.)
- **What happens if you skip?**  
  Omni-Channel won’t know which object’s records to route, so no work will be routed automatically to agents for that object.
  | Component                    | Role/Relation                                                   |
| ---------------------------- | --------------------------------------------------------------- |
| **Case/Lead/Custom Object**  | The actual record needing attention (like a customer complaint) |
| **Service Channel**          | Tells Omni-Channel: “Hey! This type of record needs routing”    |
| **Queue**                    | Owns those records (who should receive them?)                   |
| **Routing Configuration**    | Defines how fast, how big, how urgent, etc.                     |
| **Presence Status & Config** | Defines when agents are available for which channel             |

📥 Example:
You want to route Case records:
✅ Create a Service Channel with Object = Case

✅ Create a Queue that supports Case object

✅ Create a Routing Configuration

✅ Link the Queue to Routing Configuration

✅ Add agents to a Presence Configuration with a Presence Status like "Available for Cases"

✅ Agent logs into console → goes “Available” → Case gets routed via the Service Channel

- **How to do it:**  
  - Go to **Setup** → Search **Service Channels** → **New**  
  - Enter **Service Channel Name** (e.g., "miaw service channel")  
  - Select the **Salesforce Object** you want to route (e.g., Case)  
  - Optionally select a **Custom Console Footer Component** for UI enhancements  
  - Configure these settings:
    - **Minimize Omni-Channel component when work is accepted:** Automatically minimize the Omni-Channel widget when agents accept work (optional)  
    - **Automatically accept work requests:** Automatically assigns work to agents without requiring manual acceptance (optional)  
    - **Is Interruptible:** Allows this work type to interrupt other work an agent is doing (optional)  
    - **Audio Settings:** Override agent audio alerts for incoming work (optional)  
  
---

### Example:  
You want to route **Case** records to your support agents. You create a service channel named "miaw service channel" linked to the **Case** object. Agents get notified via Omni-Channel when new Cases arrive and can accept or automatically receive them depending on the settings.

---

## Key Fields Explained

| Field                             | Purpose                                                  | Impact if Not Configured                         |
|----------------------------------|----------------------------------------------------------|-------------------------------------------------|
| **Service Channel Name**          | Name to identify this channel                            | You can't create or select the channel          |
| **Salesforce Object**             | Specifies which object’s records to route               | Work from this object won't route                |
| **Custom Console Footer Component** | Add UI components for enhanced agent experience          | No custom footer UI                               |
| **Minimize Omni-Channel component when work is accepted** | Helps reduce UI clutter when agents accept work        | Agent Omni-Channel panel stays open and visible  |
| **Automatically accept work requests** | Assigns work without manual acceptance by agents          | Agents must manually accept every work item      |
| **Is Interruptible**              | Allows this work to interrupt other active work          | Work waits until agent finishes current task     |
| **Audio Settings**                | Controls agent notification sounds                        | Default audio settings apply                      |

---

## How Service Channel Fits in the Omni-Channel Flow

1. **Records created or updated** on the selected Salesforce object (e.g., new Cases).  
2. These records enter the **Queue** associated with that object.  
3. The **Routing Configuration** defines priority and capacity for routing work from the queue.  
4. The **Service Channel** defines *which object* Omni-Channel should monitor and route from.  
5. **Omni-Channel routes the work** to agents based on their presence and capacity.  

---

## Summary

| Step                     | Why                                     | What if skipped                     | How to do it                           |
|--------------------------|----------------------------------------|-----------------------------------|--------------------------------------|
| Create Service Channel    | Define which object records route to agents | Work from object won’t route       | Setup → Service Channels → New       |
| Set Object               | Specify the Salesforce object          | No routing for that object         | Select object during channel creation|
| Configure Settings       | Customize agent experience and routing | Default behavior applies           | Adjust options in service channel setup|

---

*Properly configuring Service Channels ensures Omni-Channel routes the right Salesforce records to the right agents, with customized behavior for efficient work distribution and agent experience.*

