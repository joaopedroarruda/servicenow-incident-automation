# ServiceNow - Incident Automation

## About the Project

This project was created in a ServiceNow Personal Developer Instance (PDI) using **Flow Designer**.

The goal is to automate the initial analysis of incidents that have a **Configuration Item (CI)** and identify if there are other open incidents related to the same CI.

## Objective

When a new incident is created, the Flow checks whether:

* The incident has a Configuration Item.
* There are other open incidents for the same Configuration Item.

Based on the result, the Flow automatically updates the incident with the appropriate information.

## Flow Logic

The automation follows these steps:

```text
Incident Created
       │
       ▼
Has Configuration Item?
       │
      Yes
       ▼
Look Up Incident Records
       │
       ▼
Has Open Incidents?
     /       \
   Yes        No
    │          │
    ▼          ▼
Update       Update
Incident     Incident
    │          │
    ▼          ▼
High         Work Notes:
Impact       No other open
Urgency      incidents found
Work Notes
```

## Technologies Used

* ServiceNow
* Flow Designer
* Incident Management
* Flow Logic
* Look Up Records
* Update Record
* Conditions and Data Pills

## Flow Configuration

### 1. Trigger

The Flow starts when an **Incident is Created**.

### 2. Configuration Item Check

The first condition verifies if the new incident has a **Configuration Item**.

If there is no Configuration Item, the automation does not continue.

### 3. Look Up Records

The Flow searches the **Incident** table for other incidents that:

* Are not Closed, Resolved, or Canceled.
* Have the same Configuration Item as the new incident.
* Are different from the current incident.

The current incident is excluded using its **Sys ID**.

### 4. Check for Open Incidents

The Flow checks the number of records returned by the search.

If the number is greater than `0`, the Flow identifies that there are other open incidents related to the same Configuration Item.

### 5. Update Incident - Open Incidents Found

When other open incidents are found, the Flow updates the current incident:

* **Impact:** 1 - High
* **Urgency:** 1 - High
* **Work Notes:** Information explaining that other open incidents were found for the same Configuration Item.

### 6. Update Incident - No Open Incidents

If no other open incidents are found, the Flow updates the Work Notes with information indicating that no other open incidents were found for the Configuration Item.

## Test Result

The Flow was tested successfully in the ServiceNow instance.

**Execution result:** Completed

The test confirmed that:

* The Incident Created trigger executed successfully.
* The Configuration Item condition was evaluated.
* The Look Up Records action completed successfully.
* The condition for open incidents was evaluated.
* The appropriate Update Record action was executed.

## Screenshots

### 1. Flow Overview

![Flow Overview](screenshots/print%20incident%201.png)

### 2. Look Up Records Configuration

![Look Up Records](screenshots/print%20incident%202.png)

### 3. Open Incidents Condition

![Open Incidents Condition](screenshots/print%20incident%203.png)

### 4. Update Incident - Open Incidents Found

![Update Incident](screenshots/print%20incident%204.png)

### 5. Else Branch

![Else Branch](screenshots/print%20incident%205.png)

### 6. Update Incident - No Open Incidents

![Update Incident - No Open Incidents](screenshots/print%20incident%206.png)

### 7. Complete Flow

![Complete Flow](screenshots/print%20incident%207.png)

### 8. Flow Execution Result

![Flow Execution](screenshots/print%20incident%208.png)

## What I Learned

Through this project, I practiced:

* Creating automated flows in ServiceNow.
* Using conditions in Flow Designer.
* Searching records with **Look Up Records**.
* Working with Data Pills.
* Using record counts in flow conditions.
* Updating Incident records automatically.
* Testing and analyzing Flow executions.

## Project Status

**Completed and tested successfully.**

---

**Created by João Pedro**
ServiceNow Developer in Training | ServiceNow CSA
