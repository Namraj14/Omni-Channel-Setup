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

# Omni-Channel Routing Setup in Salesforce

Omni-Channel routes work items like Cases, Chats, Leads, etc., to the right agents based on availability and capacity. Here's a step-by-step guide to set it up properly.

---

## ✅ Step 1: Create a Queue

### Why?  
Queues hold work items (e.g., Cases) waiting to be routed to agents. Omni-Channel pulls work from queues.

### What if you skip this?  
Omni-Channel won’t know where to get work from — so no routing happens.

### How to do it:  
1. Go to **Setup → Queues → New**  
2. Enter a **Queue Name** (e.g., "High Priority Cases")  
3. Select **Supported Object** (e.g., Case)  
4. Add users, roles, or public groups as queue members  
5. Save

---

## ✅ Step 2: Create a Routing Configuration

### Why?  
Defines how Omni-Channel routes work items:

- Priority (which work gets routed first)  
- Capacity units (how much agent workload the item takes)  
- Routing model (e.g., Most Available agent)

### What if you skip this?  
Omni-Channel won't know how to prioritize or assign work, even if it finds it in the queue.

### How to do it:  
1. Go to **Setup → Routing Configurations → New**  
2. Enter a name (e.g., "High Priority Routing")  
3. Set **Routing Priority** (lower number = higher priority)  
4. Set **Units of Capacity** (e.g., 2 means a big case counts as 2 units)  
5. Choose **Routing Model** (e.g., Most Available)  
6. Save

---

## ✅ Step 3: Assign the Routing Configuration to the Queue

### Why?  
Connects your queue with the routing rules so Omni-Channel knows how to handle work in that queue.

### What if you skip this?  
Work will stay in the queue without routing instructions — it won’t be assigned to agents.

### How to do it:  
1. Go to **Setup → Queues → Edit** your queue  
2. Under **Routing Configuration**, select the routing configuration you created  
3. Save

---

## ✅ Step 4: Create Presence Statuses

### Why?  
Agents must declare their availability via presence statuses (e.g., Available for Cases) for Omni-Channel to route work to them.

### What if you skip this?  
Omni-Channel thinks no agents are available — no routing happens.

### How to do it:  
1. Go to **Setup → Presence Statuses → New**  
2. Create statuses like "Available for Cases", "Offline"  
3. Attach each status to supported **Service Channels** (e.g., Cases)  
4. Save

---

## ✅ Step 5: Create a Presence Configuration

### Why?  
Groups presence statuses and defines what type of work (objects) an agent can receive and max capacity.

### What if you skip this?  
Agents won't have any presence statuses in Omni-Channel widget — no work routed.

### How to do it:  
1. Go to **Setup → Presence Configurations → New**  
2. Enter a name (e.g., "Support Agents Config")  
3. Set **Max Capacity** (e.g., 8 units)  
4. Add presence statuses you created in Step 4  
5. Save

---

## ✅ Step 6: Assign Presence Configuration to Agents

### Why?  
Enables agents to use Omni-Channel and receive work based on the assigned presence configuration.

### What if you skip this?  
Agents won’t see the Omni-Channel widget or get any routed work.

### How to do it:  
1. Go to **Setup → Users → Edit each agent user**  
2. Set **Presence Configuration** field to the one created in Step 5  
3. Save

---

## ✅ Step 7: Create a Service Channel

### Why?  
Service Channel **links a Salesforce object (e.g., Case) to the Queue and Routing Configuration** so Omni-Channel knows where to pull work and how to route it.

### What if you skip this?  
Omni-Channel won't know how to associate work items with queues or routing logic — routing will fail.

### How to do it:  
1. Go to **Setup → Service Channels → New**  
2. Select the **Salesforce Object** (e.g., Case)  
3. Select the **Queue** created in Step 1  
4. Select the **Routing Configuration** assigned in Step 3  
5. Save

---

## ✅ Step 8: Add Omni-Channel Widget to Lightning App

### Why?  
Agents need an interface to log in to Omni-Channel, change presence status, and accept work.

### What if you skip this?  
Agents won’t have access to Omni-Channel UI — they can't receive or manage work.

### How to do it:  
1. Go to **Setup → App Manager → Edit your Lightning App (e.g., Service Console)**  
2. Add **Omni-Channel** to the Utility Bar  
3. Save and activate the app

---

# Summary Flow

- **Queue**: Holds work items  
- **Routing Configuration**: Defines routing rules  
- **Assign Routing Config to Queue**: Connects routing to queue  
- **Presence Status & Configuration**: Agent availability and capacity  
- **Assign Presence Config to Agents**: Enables agent participation  
- **Service Channel**: Connects object + queue + routing for Omni-Channel  
- **Omni-Channel Widget**: Agent interface  

---

# What if you skip parts?

| Component                | Result if skipped                                  |
|--------------------------|--------------------------------------------------|
| Queue                    | No place to hold work → no routing               |
| Routing Configuration    | No routing priority or capacity info             |
| Routing Config + Queue   | Work stays idle, no routing happens               |
| Presence Status          | Agents appear unavailable, no routing            |
| Presence Configuration   | Agents can't choose status, no routing            |
| Agent Presence Assignment| Agents can't receive routed work                  |
| Service Channel          | Omni-Channel can't link work items to queues     |
| Omni-Channel Widget      | Agents have no UI to accept and manage work      |

---

This setup ensures work items flow smoothly from creation to the right agent, based on priorities and availability.


