# Salesforce Omni-Channel

## Definition

**Omni-Channel** is a **Salesforce Service Cloud feature** that intelligently routes work items (such as Cases, Chats, Leads, or custom objects) to the **right agents** in real-time based on their availability, skill set, and workload.

## Overview

Omni-Channel ensures that:
- The **right agent** gets the **right work**, at the **right time**.
- It prevents agents from being overwhelmed.
- It supports multiple channels like **Chat, Email, Web, Phone, and Social Media**, hence the name **Omni** (meaning all).

## Key Features

| Feature              | Description                                              |
|----------------------|----------------------------------------------------------|
| **Work Routing**     | Routes records (Cases, Leads, etc.) to agents automatically. |
| **Routing Configurations** | Define how work is prioritized and assigned.             |
| **Presence Status**   | Agents can set themselves as available/unavailable for different types of work. |
| **Skills-Based Routing** | Matches work with agents based on skill sets.             |
| **Push vs. Pull**    | Pushes work to agents (versus agents picking work from queues). |

## Example Use Case

1. A new **Case** is created from email.
2. Omni-Channel checks which agent is **available** and has the right **skills**.
3. It **automatically assigns** the case to that agent and **notifies** them in the console.
4. The agent accepts and starts working immediately.

## Objects Omni-Channel Can Route

- **Standard**: Cases, Leads, Chats, SOS Sessions
- **Custom**: Any custom object (e.g., `Work_Order__c`)

## Benefits

- Faster customer service.
- Balanced agent workload.
- Increased productivity.
- Better SLA adherence.



# 🎯 Omni-Channel Setup Guide (Salesforce)

A step-by-step explanation and setup for Omni-Channel with deep insights into **why** each step is necessary.

---

## 📌 What is Omni-Channel?

Omni-Channel is a Salesforce feature that **automatically routes work items (like Cases, Leads, Chats, etc.)** to the most suitable, available agents in real time.

---

## ✅ Why Use Omni-Channel?

- Automatically distributes work based on agent availability
- Prevents agent overload
- Ensures high-priority work gets attention first
- Boosts service efficiency and customer satisfaction

---

## 🛠 Prerequisites

1. Omni-Channel must be enabled in your org.
2. You must have the **Service Console** license and set up.
3. You need admin access to configure Presence, Routing, and Queues.

---

## 🔁 Omni-Channel Setup Steps

---

### 🔹 Step 1: Enable Omni-Channel

**Why?** Activates the Omni-Channel settings in your org.

- Go to **Setup → Omni-Channel**
- Click **Enable Omni-Channel**

---

### 🔹 Step 2: Create Presence Statuses

**Why?** These are the online/offline indicators agents use (e.g., "Available for Case", "Offline").

**How:**
- Go to **Setup → Presence Statuses**
- Click **New**
  - Name: `Available for Cases`
  - Status Type: `Online`
  - Channels: `Cases`
- Add more statuses as needed (Offline, Chat, etc.)

---

### 🔹 Step 3: Create Presence Configuration

**Why?** Groups the statuses and defines:
- Which objects (Cases, Leads, Chats) an agent can receive
- Max capacity (total workload units allowed)

**How:**
- Go to **Setup → Presence Configurations**
- Click **New**
  - Name: `Case Support Agents`
  - Capacity: `6`
  - Assign previously created Presence Statuses

---

### 🔹 Step 4: Create a Routing Configuration

**Why?** Tells Salesforce **how** to assign work:
- Priority (lower = more urgent)
- Capacity weight (how heavy is this work)
- Routing model (Least Active or Most Available)

**How:**
- Go to **Setup → Routing Configurations**
- Click **New**
  - Name: `High Priority Cases`
  - Routing Priority: `1`
  - Capacity Units: `2`
  - Routing Model: `Most Available`

---

### 🔹 Step 5: Create a Queue & Link Routing Configuration

**Why?** The Queue is the holding area for work. You must assign a Routing Configuration to tell Salesforce how to process the items in it.

**How:**
- Go to **Setup → Queues**
- Click **New**
  - Name: `Case Queue`
  - Object: `Case`
  - Add members (users/profiles)
  - Assign Routing Configuration: `High Priority Cases`

---

### 🔹 Step 6: Assign Users to Presence Configuration

**Why?** Agents won’t be able to go online or receive work unless assigned.

**How:**
- Go to **Setup → Users**
- Edit a User
  - Presence Configuration: `Case Support Agents`

---

### 🔹 Step 7: Add Omni-Channel to Console App

**Why?** This lets agents see the Omni-Channel widget in their workspace.

**How:**
- Go to **App Manager → [Your Console App] → Edit**
- Under **Utility Bar**, click **Add Utility Item → Omni-Channel**
- Set Panel Height: `300`, Panel Width: `400`

---

### 🔹 Step 8: Test the Setup

1. Login as an agent.
2. Open the console app.
3. Change Presence Status to "Available for Cases".
4. Create a new Case assigned to the Queue.
5. Watch it get automatically routed.

---

## 🧠 Bonus Tips

- Use **"Most Available"** for balanced workload distribution.
- Use **Routing Priority** wisely — it ensures urgent work is not stuck.
- Monitor with **Omni Supervisor** for real-time visibility.

---

## 🧪 FAQs

### Q: Can a queue have multiple routing configs?
❌ No. One queue = One routing config.

### Q: Can a routing config be reused?
✅ Yes. One routing config can be used by multiple queues **if they have the same routing logic**.

### Q: What happens if a user has no presence config?
❌ They can't go online, receive work, or use the Omni-Channel widget.

---

## 🧩 Real-World Example Setup

| Element                | Value                          |
|------------------------|--------------------------------|
| Queue Name             | `High Priority Cases`          |
| Routing Configuration  | `High Priority Routing (1)`    |
| Presence Statuses      | `Available for Cases`, `Offline` |
| Presence Configuration | `Case Support Agents` (Capacity: 6) |
| Console App            | `Service Console` with Omni Widget |

---

## 🧰 Useful Objects

| Object                        | Description                      |
|-------------------------------|----------------------------------|
| `PresenceUserConfig`          | User-Presence Configuration link |
| `PresenceStatus`              | Statuses like "Available"        |
| `RoutingConfiguration`        | Routing rules per queue          |
| `Omni-Channel Supervisor`     | Monitor agent workloads          |

---

## ✅ You're Ready!

Now your Omni-Channel setup is production-ready. You’ve not only configured it — you understand **why** it works that way. 🎯


