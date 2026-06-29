# Salesforce Record-Triggered Flow — Auto-Create Interviewer Records

A Salesforce automation built using **Flow Builder** that eliminates manual data entry in a recruiting app. Whenever a new **Position** record is created with a Hiring Manager assigned, the flow automatically generates a linked **Interviewer** record — no clicks required.

---

## What This Does

In a growing recruiting team, every open position needs an interviewer record tied to it. Doing this by hand is repetitive and error-prone. This flow handles it automatically the moment a Position is saved.

**Trigger:** A new Position record is created  
**Condition:** Hiring Manager field is not null  
**Action:** Create an Interviewer record, mapping:
- `Employee` ← Position's Hiring Manager
- `Position` ← Position's Record ID

---

## Screenshots

### 1. Flow Builder — Active Flow
![Flow Builder](screenshots/Flow_Builder.png)

The Record-Triggered Flow in Flow Builder, showing the trigger node (Position created), the **Create Interviewer Record** action, and the End node. Status is **Active**.

---

### 2. Flow Detail Page
![Flow Details](screenshots/Flow_Details.png)

The flow's detail page in Salesforce Automation, confirming:
- **Type:** Record–Run After Save
- **Status:** Activated
- **API Name:** `Create_Interviewer_Record`
- **Created:** 29/06/2026, 6:30 pm by Budutha Harish Reddy

---

### 3. Position Record — Related Tab
![Position Record Related Tab](screenshots/Position_Record___Related_Tab.png)

The **Super Support Supervisor** Position record after being saved. The **Related** tab shows `Interviewers (1)`, confirming the flow fired and created the linked record automatically.

---

### 4. Interviewers List View
![Interviewers List](screenshots/Interviewers_List.png)

The Interviewers object list view showing two auto-generated records: `INT-0002` and `INT-0000` — both created by the flow, not manually.

---

### 5. Positions List View
![Positions List](screenshots/Positions_List.png)

The Positions list showing all three test records used to validate the automation, including **Super Support Supervisor**, which was used as the primary test case.

---

## Flow Configuration

### Trigger Settings

| Setting | Value |
|---|---|
| Object | Position |
| Trigger | A record is created |
| Condition | Hiring Manager ≠ null |
| Optimization | Actions and Related Records |

### Create Records Element

| Field | Value Source |
|---|---|
| Object | Interviewer |
| Employee | Triggering Position → Hiring Manager |
| Position | Triggering Position → Record ID |

---

## How to Deploy

1. Open **Salesforce Setup → Flows → New Flow**
2. Choose **Record-Triggered Flow**
3. Set Object to `Position`, trigger to `A record is created`
4. Add condition: `Hiring Manager` → `Is Null` → `False`
5. Add a **Create Records** element:
   - Object: `Interviewer`
   - Map `Employee` to Hiring Manager, `Position` to Record ID
6. Save and **Activate**

> **Note:** Before activating this flow, deactivate any existing validation rule that requires a Hiring Manager on Position records, as the flow handles that logic instead.

---

## Testing

1. Navigate to the **Recruiting** app → Positions → New
2. Create a Position with a Hiring Manager assigned
3. After saving, open the **Related** tab — an Interviewer record should appear automatically
4. Navigate to **Interviewers** to confirm the new record with correct Employee and Position values

---

## Tech Stack

- **Salesforce Flow Builder** — Record-Triggered (After Save)
- **Recruiting App** (custom Salesforce org built across multiple Trailhead projects)
- Objects involved: `Position__c`, `Interviewer__c`

---

## Project Context

This automation is part of a series of Salesforce admin projects built on the **AW Computing Recruiting App**, covering:
- Data modeling
- UI customization
- Data quality (validation rules)
- Security (roles, profiles, sharing)
- **Automation (this project)**

---

*Built by [Budutha Harish Reddy](https://github.com/Buduthaharishreddy)*
