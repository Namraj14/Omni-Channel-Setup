# 🔄 Omni-Channel Routing Types in Salesforce

Salesforce supports three main types of Omni-Channel routing:

---

## 1️⃣ Queue-Based Routing

- **Description:** Routes work items from a queue to the next available agent.
- **Best For:** Standard objects like `Case`, `Lead`, `Task`.
- **How to Use:**
  - Create a Queue
  - Assign a Routing Configuration to the Queue

---

## 2️⃣ Skill-Based Routing

- **Description:** Routes work items to agents based on specific skills.
- **Best For:** Scenarios requiring specialized agents (e.g., language support, product expertise).
- **How to Use:**
  - Define Skills
  - Assign Skills to Users
  - Add Skill Requirements to records
  - Use Routing Rules or Flows to evaluate and assign

---

## 3️⃣ External Routing

- **Description:** Routes work via external systems (e.g., telephony, chatbots) using APIs.
- **Best For:** Advanced integrations (e.g., Amazon Connect, custom bots).
- **How to Use:**
  - Use the **External Routing Interface**
  - Configure external systems to send/receive work items

---
