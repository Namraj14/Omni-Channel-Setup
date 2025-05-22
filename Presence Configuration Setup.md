# Presence Configuration Setup Explanation

Presence Configurations define how agents interact with Omni-Channel, including their capacity to handle work, behavior on accepting/declining work, and notification settings.

---

## What is Presence Configuration?

Presence Configuration controls:

- **How much work** an agent can handle at once (capacity).
- Whether agents can **automatically accept** or **decline** work.
- How the system **notifies agents** about incoming work.
- What **wrap-up time** agents get after finishing work.
- Settings for **transferring** work to other agents or queues.

---

## Fields and Explanation

### Presence Configuration Name  
- **What:** The display name of the configuration.  
- **Why:** To identify the configuration among multiple ones.  
- **Example:** `"miaw"`

### Developer Name  
- **What:** The API name for the configuration.  
- **Why:** Used for programmatic reference.  
- **Example:** `"miaw"`

### Capacity  
- **What:** Maximum units of work an agent can handle simultaneously.  
- **Why:** Controls workload per agent to avoid overloading.  
- **Example:** `20` means agent can handle 20 units of work total.

### Interruptible Capacity  
- **What:** Portion of the capacity that can be interrupted by higher-priority work.  
- **Why:** Allows urgent tasks to preempt less critical ones within this capacity.  
- **Example:** If set to 5, up to 5 units of ongoing work can be interrupted.

### Automatically accept work requests  
- **What:** If enabled, agents automatically accept incoming work without manual action.  
- **Why:** Speeds up processing, useful for high-volume scenarios.  
- **Example:** In a busy call center, agents get work assigned instantly.

### Allow agents to decline work requests  
- **What:** If enabled, agents can reject work assignments.  
- **Why:** Gives agents control to refuse tasks they can’t handle.  
- **Example:** Agent can decline if busy or not skilled for a task.

### Update Status on Decline  
- **What:** Status the agent is switched to when declining work.  
- **Why:** Keeps presence status accurate (e.g., sets agent to “Busy”).  
- **Example:** Agent status changes to "Offline" after declining.

### Allow agents to choose a decline reason  
- **What:** Lets agents specify why they declined a work item.  
- **Why:** Helps managers track and analyze declined work patterns.  
- **Example:** Reasons could be “Not skilled”, “Too busy”, or “Out of office.”

### Update Status on Push Timeout  
- **What:** Status agent switches to if they don’t respond to a work push in time.  
- **Why:** Ensures agents who miss work assignments don’t stay “Available.”  
- **Example:** Agent moved to “Away” after ignoring work assignment.

### Play a notification sound for work requests  
- **What:** Enables sound alerts for new work assignments.  
- **Why:** Notifies agents actively when new work arrives.  
- **Example:** A chime or beep when a new chat or case arrives.

### Notification Sound  
- **What:** Choose default or custom sound for notifications.  
- **Why:** Customize sounds to fit your team’s preferences.  
- **Example:** Custom sound with company branding.

### Sound Length (Seconds)  
- **What:** Duration of the notification sound, max 30 seconds.  
- **Why:** Controls how long the alert plays.  
- **Example:** Set to 5 seconds to avoid long distractions.

### Play a notification sound if Omni-Channel loses connection  
- **What:** Sound alert if Omni-Channel disconnects.  
- **Why:** Notifies agents to check connectivity issues.  
- **Example:** Warning beep if internet drops.

### After Conversation Work Time  
- **What:** Wrap-up time given to agents after finishing a task.  
- **Why:** Allows agents to complete notes or prepare before next work.  
- **Example:** 2 minutes to finalize case details.

### Agent Alias (Enhanced Messaging Only)  
- **What:** Custom alias agents use in enhanced messaging interactions.  
- **Why:** Masks real agent name, for privacy or branding.  
- **Example:** Alias like "Support Agent 01".

### Transfer Destinations  
- **What:** Defines where agents can transfer messaging sessions (profiles, queues, flows).  
- **Why:** Controls transfer targets to ensure proper routing and permissions.  
- **Example:** Agents can transfer to “Tier 2 Support” queue or specific flows.

---

## Why configure Presence Configuration?

- Without it, agents won’t know how much work they can handle.
- Routing may send too much work to agents, causing overload.
- Agents won’t have proper status updates, leading to poor workload tracking.
- Notifications won’t function, so agents may miss work assignments.
- No wrap-up time can cause rushed or incomplete task handling.

---

## How it fits in Omni-Channel flow

1. **Service Channel** monitors work from objects like Cases.
2. **Queues** hold records waiting for agents.
3. **Routing Configurations** define how work moves from queues to agents.
4. **Presence Configuration** defines agents’ capacity and behavior for accepting/declining work.
5. **Agents** assigned to a Presence Configuration see their capacity and statuses in the Omni-Channel widget.

---

