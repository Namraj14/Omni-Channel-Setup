# Salesforce Omni-Channel Routing Configuration Explained

## Routing Configuration Settings

### 1. Routing Configuration Name & Developer Name
- **What it is:**  
  The name and unique API developer name to identify this routing configuration.
  
- **Why you need it:**  
  To distinguish this routing setup from others. You might have different routing rules for different teams or case types.
  
- **What happens if you skip:**  
  You can’t save or reference this configuration without a name.

---

### 2. Overflow Assignee
- **What it is:**  
  A user or queue designated to receive work items when no agents are available or when work items "overflow."
  
- **Why you need it:**  
  Ensures no work gets stuck waiting indefinitely when all agents are busy. Overflow assignee acts like a safety net.
  
- **Important:**  
  The overflow assignee **must** have access to the object types handled by the queues linked to this routing config, otherwise overflow won’t work.
  
- **What happens if you skip:**  
  Work items may never get assigned if agents are all busy; overflow assignments will fail.

---


### 3. Routing Priority
- **What it is:**  
  A numeric priority that determines the order Omni-Channel routes work items across multiple queues.
  
- **Why you need it:**  
  Lower numbers mean higher priority. Work items from higher-priority queues get routed before lower-priority ones.
  
- **Example:**  
  A queue with priority 1 routes work before a queue with priority 5.
  
- **What happens if you skip:**  
  Omni-Channel won't know which queue’s work to route first if multiple queues feed into agents.

---

### 4. Routing Model
- **What it is:**  
  Defines the logic for distributing work among agents when multiple agents qualify to receive the same work item.
  
- **Options:**  
  - **Least Active:** Routes work to the agent with the fewest open work items (lowest current workload).  
  - **Most Available:** Routes work to the agent with the highest available capacity proportionally.
  
- **Why you need it:**  
  To balance workload fairly and efficiently.
  
- **What happens if you skip:**  
  Omni-Channel won’t know how to break ties and distribute work fairly.

---

### 5. Push Time-Out (seconds)
- **What it is:**  
  How long Omni-Channel tries to push work to an agent before trying someone else.
  
- **Why you need it:**  
  To prevent work items from getting stuck waiting on an unresponsive agent.
  
- **What happens if you skip:**  
  The default time applies, which may not suit your team’s responsiveness.

---

### 6. Drop Additional Skills Time-Out (seconds)
- **What it is:**  
  The time Omni-Channel waits before relaxing skill matching requirements if no agent with all required skills is found.
  
- **Why you need it:**  
  To ensure work still gets routed even if a perfect skill match isn’t available.
  
- **What happens if you skip:**  
  Work items might stay unassigned if strict skill matching can’t be met.

---

### 7. Capacity Type
- **What it is:**  
  Determines how capacity is measured for work assignments.
  
- **Options:**  
  - **Inherited:** Uses the capacity set on the presence configuration for agents.  
  - Other options may specify fixed units or percentages.
  
- **Why you need it:**  
  To control how much work an agent can handle simultaneously.
  
- **What happens if you skip:**  
  Default or inherited capacity is used, which may or may not fit your needs.

---

### 8. Skills-Based Routing Rules
- **What it is:**  
  Allows you to route work based on agent skills matched to work item skills.
  
- **Why you need it:**  
  To ensure work goes to agents qualified for the task.
  
- **Note:**  
  If using Omni-Channel Flow, routing rules may be triggered in flow instead.
  
- **What happens if you skip:**  
  No skill-based filtering; routing might be less precise.

---

### 9. Work Item Size (Units of Capacity or Percentage of Capacity)
- **What it is:**  
  Defines the "size" of a work item relative to agent capacity.
  
- **Example:**  
  - Units of Capacity: a big case might take 2 units, a small case 1 unit.  
  - Percentage of Capacity: a work item might consume 20% of agent capacity.
  
- **Why you need it:**  
  To let Omni-Channel understand how much agent workload each item represents.
  
- **What happens if you skip:**  
  Omni-Channel assumes each work item has equal size, which may overload agents with heavy tasks.

---

## Summary Flow Example

Imagine you have a **"High Priority Cases"** queue with Cases waiting. You create a routing configuration called **"High Priority Routing"** with:

- **Priority:** 1 (high priority)
- **Routing Model:** Most Available (to spread work evenly)
- **Overflow Assignee:** A senior agent or manager user
- **Units of Capacity:** 2 (because high priority cases are complex)
- **Skills-Based Routing:** Enabled for "Language" skill

**What happens when a new case comes in:**

- Omni-Channel looks at the queue linked with this routing config.
- Routes the case to the most available qualified agent.
- If no agent is available after the timeout, it sends the case to the overflow assignee.

If you skip setting the overflow assignee, the case might get stuck waiting if all agents are busy.

---

*This guide helps you understand the important settings for Omni-Channel routing configuration in Salesforce, ensuring efficient and fair work distribution among agents.*

