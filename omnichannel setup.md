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


# ✅ Salesforce Omni-Channel Setup Guide

This guide walks you through setting up Omni-Channel in Salesforce from scratch, with clear reasons, consequences, and steps.

---

## ✅ Step 1: Create a Queue

**Why?**  
You need a place to collect work before it’s routed. Omni-Channel pulls work from queues when using queue-based routing.

**What if you skip this?**  
Omni-Channel won't know where to look for work. You can’t route anything.

**How to do it:**
- Go to `Setup → Queues → New`
- Give it a name (e.g., `High Priority Cases`)
- Choose Object = `Case`
- Add users or public groups to this queue

---

## ✅ Step 2: Create a Routing Configuration

**Why?**  
This tells Salesforce **how** to route items:
- What's the priority?
- How much capacity does it take?
- Should it interrupt other work?

**What if you skip this?**  
Even if your case goes to a queue, Omni-Channel won’t know how much load it adds or how fast to route it.

**How to do it:**
- Go to `Setup → Routing Configurations → New`
- Example:
  - **Name:** `High Priority Routing`
  - **Routing Priority:** `1` (lower number = higher priority)
  - **Units of Capacity:** `2` (e.g., big case takes 2 units)
  - **Routing Model:** `Most Available`

---

## ✅ Step 3: Assign the Routing Configuration to the Queue

**Why?**  
This connects your queue to your routing logic.

**What if you skip this?**  
The queue will have no routing instructions. Work will just sit there — no routing will happen.

**How to do it:**
- Go to `Setup → Queues → Edit`
- Assign the Routing Configuration (select the one you created in Step 2)

---

## ✅ Step 4: Create Presence Statuses

**Why?**  
Agents need a way to say:  
“I’m online and ready for work.”  
Omni-Channel only routes work to agents who are available in a specific status.

**What if you skip this?**  
Omni-Channel won’t route anything — because no agent is technically “available.”

**How to do it:**
- Go to `Setup → Presence Statuses → New`
- Create statuses like:
  - `Available for Cases`
  - `Offline`
- Assign each status to the relevant **channels** (e.g., Cases, Chats)

---

## ✅ Step 5: Create Presence Configuration

**Why?**  
This groups your statuses and defines:
- What objects the agent can receive (Cases, Chats, Leads)
- Max capacity (total workload allowed)

**What if you skip this?**  
Agents won’t have access to those statuses in the Omni-Channel widget. Work won’t route.

**How to do it:**
- Go to `Setup → Presence Configuration → New`
- Example:
  - **Name:** `Support Agents Config`
  - **Max Capacity:** `8`
  - Assign the **Presence Statuses** from Step 4

---

## ✅ Step 6: Add Agents to Presence Configuration

**Why?**  
You must assign agents to a configuration, so they get access to Omni-Channel.

**What if you skip this?**  
Your agents will see nothing. No widget. No routing. No magic.

**How to do it:**
- Go to `Setup → Users → Edit`
- Assign the **Presence Configuration** to the user

---

## ✅ Step 7: Add the Omni-Channel Widget to the App

**Why?**  
Agents need a user interface to log in to Omni-Channel and change their presence status.

**What if you skip this?**  
Even if everything’s configured, agents won’t see the Omni-Channel panel. No way to accept work.

**How to do it:**
- Go to `Setup → App Manager`
- Edit the **Lightning App** (e.g., Service Console)
- Add the **Omni-Channel** utility item (this adds it to the bottom dock)

---

✅ Done! Now your agents can receive work through Omni-Channel using queue-based routing!

