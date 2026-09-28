# Implement Client Script & UI Policy (Incident)

## 📌 Project Overview

The **Implement Client Script & UI Policy (Incident)** project demonstrates how ServiceNow client-side scripting and UI Policies can be used to improve data validation, user experience, and data integrity within the Incident Management module.

The project implements dynamic form behavior using **Client Scripts**, **UI Policies**, and **GlideForm APIs**. These controls ensure that Incident records are created with complete and valid information while reducing manual errors during Incident creation and modification.

The implementation includes mandatory field validation, automatic field population, field read-only controls, conditional field behavior, submission validation, and restrictions on inline list editing.

---

## 🎯 Objective

The objective of the Implement Client Script & UI Policy (Incident) project is to demonstrate how ServiceNow client-side controls can be used to enforce data integrity on Incident records.

This implementation showcases how UI Policies and Client Scripts can dynamically:

* Make fields mandatory
* Auto-populate field values
* Control field visibility
* Make fields read-only
* Validate Incident information
* Prevent record submission when required information is missing
* Automatically update field values based on conditions
* Restrict unauthorized inline list editing

The solution ensures that Incidents are created with complete and valid information, improving data quality and consistency across the platform.

---

## 🏢 Platform

**ServiceNow**

### Module

**Incident Management**

### Application Area

**IT Service Management (ITSM)**

---

# 📋 Table of Contents

1. [Project Overview](#-project-overview)
2. [Objective](#-objective)
3. [Problem Statement](#-problem-statement)
4. [Proposed Solution](#-proposed-solution)
5. [Project Features](#-project-features)
6. [Technologies Used](#-technologies-used)
7. [ServiceNow Concepts Used](#-servicenow-concepts-used)
8. [UI Policy Implementation](#-ui-policy-implementation)
9. [Client Script Implementation](#-client-script-implementation)
10. [Application Flow](#-application-flow)
11. [System Navigation](#-system-navigation)
12. [Functional Requirements](#-functional-requirements)
13. [Non-Functional Requirements](#-non-functional-requirements)
14. [Validation Rules](#-validation-rules)
15. [Testing](#-testing)
16. [Test Cases](#-test-cases)
17. [Expected Results](#-expected-results)
18. [Project Structure](#-project-structure)
19. [Screenshots](#-screenshots)
20. [Advantages](#-advantages)
21. [Limitations](#-limitations)
22. [Future Enhancements](#-future-enhancements)
23. [Learning Outcomes](#-learning-outcomes)
24. [Conclusion](#-conclusion)
25. [Author](#-author)

---

# 🔴 Problem Statement

In a standard Incident Management system, users may accidentally submit incomplete or invalid Incident records.

Some common problems include:

* Required fields being left empty
* Incorrect urgency values
* Important fields being modified unnecessarily
* Invalid Incident submission
* Inconsistent data entry
* Unauthorized inline editing
* Lack of automatic field updates
* Increased manual effort for validation

These problems can affect data quality and make Incident management less efficient.

Therefore, a client-side validation solution is required to dynamically control the Incident form based on user actions and predefined conditions.

---

# 💡 Proposed Solution

The proposed solution uses ServiceNow **UI Policies** and **Client Scripts** to control the Incident form dynamically.

The implementation provides:

* Conditional mandatory fields
* Automatic field value population
* Dynamic field behavior
* Read-only controls
* Form submission validation
* Impact-based urgency calculation
* Assigned To validation
* Inline list editing restriction

This improves the reliability and consistency of Incident records.

---

# ⭐ Project Features

The project contains the following major features:

### 1. UI Policy

UI Policies dynamically control Incident form fields based on specified conditions.

### 2. Mandatory Field Control

Important fields can automatically become mandatory when the defined condition is satisfied.

### 3. Read-Only Field Control

Selected fields can be made read-only to prevent unwanted modifications.

### 4. Automatic Urgency Population

Urgency can be automatically updated based on the selected Impact value.

### 5. Form Validation

The system validates required information before allowing the Incident record to be submitted.

### 6. Assigned To Validation

The Incident cannot be submitted when the required Assigned To information is missing.

### 7. onChange Validation

Changes to fields such as Impact can automatically trigger corresponding changes in other fields.

### 8. onLoad Behavior

Certain field properties can be configured automatically when the Incident form is loaded.

### 9. onCellEdit Restriction

Inline editing of selected Incident fields can be controlled using an onCellEdit Client Script.

---

# 🛠️ Technologies Used

| Technology               | Purpose                         |
| ------------------------ | ------------------------------- |
| ServiceNow               | Development Platform            |
| Incident Management      | Application Module              |
| UI Policies              | Dynamic field control           |
| Client Scripts           | Client-side validation          |
| GlideForm API            | Form manipulation               |
| JavaScript               | Client-side scripting           |
| ServiceNow Form Designer | Form configuration              |
| List Configuration       | List and inline editing control |

---

# 🧩 ServiceNow Concepts Used

## UI Policies

UI Policies are used to dynamically change the behavior of fields on a ServiceNow form.

They can be used to:

* Make fields mandatory
* Make fields optional
* Make fields read-only
* Make fields editable
* Show fields
* Hide fields

The behavior depends on the conditions configured in the UI Policy.

---

## Client Scripts

Client Scripts are JavaScript-based scripts that execute on the client side of ServiceNow forms.

The project uses different Client Script types:

* onLoad
* onChange
* onSubmit
* onCellEdit

---

## GlideForm API

The **GlideForm (`g_form`) API** is used to interact with fields on ServiceNow forms.

Common operations include:

```javascript
g_form.setMandatory();
g_form.setReadOnly();
g_form.setVisible();
g_form.setValue();
g_form.getValue();
g_form.getControl();
```

These functions allow the Incident form to respond dynamically to user actions.

---

# ⚙️ UI Policy Implementation

The UI Policy is configured on the **Incident table**.

The configuration contains:

* UI Policy Name
* Table
* Active status
* Condition
* UI Policy Actions

The policy evaluates the specified condition and applies the configured field behavior.

### Example UI Policy Behavior

When the specified condition becomes true:

* Required fields become mandatory
* Selected fields can become read-only
* Selected fields can become visible
* Form behavior changes dynamically

When the condition becomes false, the configured reverse behavior can restore the original field state.

---

# 💻 Client Script Implementation

The project demonstrates four major Client Script types.

---

## 1. onLoad Client Script

The **onLoad Client Script** executes when the Incident form is loaded.

### Purpose

It can be used to:

* Set initial field values
* Configure field properties
* Display information
* Apply initial validation

### Example Structure

```javascript
function onLoad() {
    // Client-side form logic
}
```

---

# 2. onChange Client Script

The **onChange Client Script** executes when the value of a selected field changes.

In this project, the Impact field is used to dynamically control Urgency.

### Example Logic

```text
Impact changes
      ↓
Check Impact value
      ↓
Determine appropriate Urgency
      ↓
Update Urgency field
```

This reduces manual data entry and helps maintain consistent Incident information.

### Example Structure

```javascript
function onChange(control, oldValue, newValue, isLoading, isTemplate) {

    if (isLoading) {
        return;
    }

    // Impact-based field logic
}
```

---

# 3. onSubmit Client Script

The **onSubmit Client Script** executes when the user attempts to submit the Incident form.

Its main purpose is to validate required information before the record is submitted.

### Validation Flow

```text
User clicks Submit
        ↓
Validate required information
        ↓
Is information complete?
     ↙          ↘
   YES           NO
    ↓             ↓
Submit       Display message
Incident     and stop submission
```

### Example Structure

```javascript
function onSubmit() {

    // Validate required fields

    // Return false to prevent submission
    // Return true to allow submission
}
```

---

# 4. onCellEdit Client Script

The **onCellEdit Client Script** is used to control changes made directly from a ServiceNow list.

It helps prevent unauthorized or invalid inline editing of selected fields.

### Flow

```text
User edits list field
        ↓
onCellEdit executes
        ↓
Validate change
        ↓
Allow or prevent update
```

---

# 🔄 Application Flow

The overall application flow is:

```text
Start
  ↓
Open ServiceNow
  ↓
Navigate to Incident Management
  ↓
Open/Create Incident
  ↓
UI Policy evaluates conditions
  ↓
Fields become mandatory/read-only/visible
  ↓
User enters Incident information
  ↓
Impact changes
  ↓
onChange Client Script executes
  ↓
Urgency is updated
  ↓
User clicks Submit
  ↓
onSubmit validation executes
  ↓
Is the Incident valid?
   ↙             ↘
 YES             NO
  ↓               ↓
Save Incident   Display Validation
                Message
```

---

# 🧭 System Navigation

The general navigation used for this project is:

```text
ServiceNow
   ↓
All
   ↓
Service Desk
   ↓
Incidents
   ↓
Create New
   ↓
Incident Form
```

For configuration:

```text
All
 ↓
System Definition
 ↓
Client Scripts
```

and:

```text
All
 ↓
System UI
 ↓
UI Policies
```

The exact navigation labels can vary depending on the ServiceNow version and application configuration.

---

# 📌 Functional Requirements

| ID   | Requirement                                                 |
| ---- | ----------------------------------------------------------- |
| FR01 | System should provide an Incident form                      |
| FR02 | UI Policy should control Incident fields                    |
| FR03 | Required fields should become mandatory based on conditions |
| FR04 | Selected fields should be configurable as read-only         |
| FR05 | Impact changes should trigger appropriate field logic       |
| FR06 | Urgency should be automatically updated when applicable     |
| FR07 | Form submission should validate required information        |
| FR08 | Invalid submission should be prevented                      |
| FR09 | Assigned To information should be validated                 |
| FR10 | Inline list editing should be controlled                    |

---

# 🔐 Non-Functional Requirements

### Reliability

The system should consistently apply the configured validation rules.

### Usability

The Incident form should provide clear and understandable field behavior.

### Maintainability

Client Scripts and UI Policies should be organized so that future modifications are easier.

### Performance

Client-side validation should execute efficiently without unnecessary processing.

### Data Integrity

Invalid or incomplete Incident information should be prevented whenever the configured validation rules require it.

---

# 📝 Validation Rules

The project implements the following validation concepts:

| Validation                 | Purpose                                        |
| -------------------------- | ---------------------------------------------- |
| Mandatory Field Validation | Ensures required information is entered        |
| Assigned To Validation     | Ensures required assignment information exists |
| Impact Validation          | Controls related Incident behavior             |
| Urgency Update             | Automatically maintains appropriate urgency    |
| Submission Validation      | Prevents incomplete records                    |
| Inline Edit Validation     | Controls list-level modifications              |

---

# 🧪 Testing

Testing was performed to verify that the configured UI Policies and Client Scripts work according to the defined requirements.

The Incident form was tested under different conditions, including:

* Form loading
* Field changes
* Missing required information
* Valid submission
* Invalid submission
* Impact changes
* Assigned To validation
* Inline list editing

---

# 📊 Test Cases

| Test ID | Test Scenario                       | Expected Result                                       |
| ------- | ----------------------------------- | ----------------------------------------------------- |
| TC01    | Open Incident form                  | Form loads successfully                               |
| TC02    | UI Policy condition is satisfied    | Configured field behavior is applied                  |
| TC03    | UI Policy condition is false        | Reverse/original behavior is applied where configured |
| TC04    | Change Impact                       | Related Client Script executes                        |
| TC05    | Impact requires Urgency update      | Urgency is updated                                    |
| TC06    | Submit without required information | Submission is prevented                               |
| TC07    | Submit with valid information       | Incident is submitted                                 |
| TC08    | Assigned To is missing              | Validation prevents submission where configured       |
| TC09    | Edit restricted field from list     | Edit is prevented where configured                    |
| TC10    | Load form                           | onLoad Client Script executes correctly               |

---

# ✅ Expected Results

The expected results of the project are:

* Incident fields respond dynamically to conditions.
* Required fields are properly enforced.
* Appropriate field values are automatically populated.
* Invalid submissions are prevented.
* Assigned To information is validated.
* Impact-based logic works correctly.
* Inline editing restrictions are applied.
* Incident records contain more consistent information.

---

# 📂 Project Structure

The GitHub repository is organized as follows:

```text
ServiceNow-Incident-Client-Script-UI-Policy/
│
├── Documentation/
│
├── ServiceNow_Phase_Wise_Document/
│
├── screen shots/
│
├── README.md
│
├── Screenshot 2026-09-25 223046.png
├── Screenshot 2026-09-25 223307.png
├── Screenshot 2026-09-25 224046.png
├── Screenshot 2026-09-25 224111.png
├── Screenshot 2026-09-25 224726.png
├── Screenshot 2026-09-25 225054.png
├── Screenshot 2026-09-25 225135.png
└── Screenshot 2026-09-25 225359.png
```

> **Recommended:** Keep all screenshots inside the `screen shots` folder to keep the repository clean.

---

# 📸 Screenshots

The repository contains screenshots demonstrating the ServiceNow implementation.

## 1. Incident Form

This screenshot demonstrates the configured Incident form and the fields used during the implementation.

![Incident Form](Screenshot%202026-09-25%20223046.png)

---

## 2. UI Policy Configuration

This screenshot demonstrates the UI Policy configuration applied to the Incident table.

![UI Policy Configuration](Screenshot%202026-09-25%20223307.png)

---

## 3. UI Policy Actions

This screenshot demonstrates the field actions configured through the UI Policy.

![UI Policy Actions](Screenshot%202026-09-25%20224046.png)

---

## 4. Client Script Configuration

This screenshot demonstrates the Client Script configuration used for client-side behavior.

![Client Script Configuration](Screenshot%202026-09-25%20224111.png)

---

## 5. onChange Behavior

This screenshot demonstrates the behavior triggered when the selected Incident field is changed.

![onChange Script](Screenshot%202026-09-25%20224726.png)

---

## 6. onSubmit Validation

This screenshot demonstrates the validation applied before submitting an Incident.

![onSubmit Validation](Screenshot%202026-09-25%20225054.png)

---

## 7. Validation Result

This screenshot demonstrates the result of the configured validation.

![Validation Result](Screenshot%202026-09-25%20225135.png)

---

## 8. Final Incident Result

This screenshot demonstrates the final Incident form after applying the configured Client Scripts and UI Policies.

![Final Result](Screenshot%202026-09-25%20225359.png)

---

# 🔒 Security Considerations

The project focuses mainly on client-side validation. Client-side controls improve user experience and data quality, but they should not be treated as the only security mechanism.

Important security considerations include:

* Use appropriate ServiceNow roles.
* Restrict administrative configuration access.
* Validate important data on the server side where required.
* Avoid exposing sensitive information through client-side scripts.
* Follow ServiceNow access control policies.
* Use ACLs for server-side authorization.

---

# ⚡ Advantages

The implemented solution provides several benefits:

1. Improves Incident data quality.
2. Reduces incomplete records.
3. Automates repetitive field updates.
4. Improves user experience.
5. Provides dynamic form behavior.
6. Reduces manual validation effort.
7. Prevents invalid form submission.
8. Improves consistency in Incident records.
9. Demonstrates practical ServiceNow scripting skills.
10. Provides a maintainable client-side configuration.

---

# ⚠️ Limitations

The current implementation has some limitations:

* Client-side validation depends on the configured Client Scripts.
* UI Policies mainly control form behavior.
* Client-side controls alone should not replace server-side security.
* Advanced validation may require Business Rules or Script Includes.
* The implementation is designed specifically around the Incident module.

---

# 🚀 Future Enhancements

The project can be extended with additional ServiceNow features.

Possible future enhancements include:

* Business Rules for server-side validation
* Script Includes for reusable logic
* Data Policies for stronger data validation
* ACL-based security controls
* Automated notifications
* Incident assignment automation
* SLA management
* Email notifications
* Approval workflows
* Incident dashboards
* Reporting and analytics
* Integration with external applications
* Automated testing

---

# 📚 Learning Outcomes

Through this project, the following ServiceNow concepts were practiced:

* Incident Management
* UI Policies
* Client Scripts
* onLoad Client Scripts
* onChange Client Scripts
* onSubmit Client Scripts
* onCellEdit Client Scripts
* GlideForm API
* Form validation
* Dynamic field behavior
* Mandatory field configuration
* Read-only field configuration
* Automatic field updates
* List editing control
* Testing and debugging
* ServiceNow application navigation

---

# 🏆 Project Outcomes

The project successfully demonstrates how ServiceNow client-side controls can be used to improve Incident form behavior.

The combination of UI Policies and Client Scripts provides a flexible way to:

```text
Control Fields
      ↓
Validate Input
      ↓
Automate Updates
      ↓
Prevent Invalid Submission
      ↓
Improve Data Quality
```

The implementation provides practical experience in configuring and customizing the ServiceNow Incident Management module.

---

# 📌 Conclusion

The **Implement Client Script & UI Policy (Incident)** project demonstrates the practical use of ServiceNow client-side customization techniques.

UI Policies provide dynamic control over form fields, while Client Scripts provide programmable validation and automation. Together, these features help ensure that Incident records contain complete and consistent information.

The project also demonstrates how different Client Script types such as **onLoad, onChange, onSubmit, and onCellEdit** can be used for different stages of the Incident lifecycle.

Overall, this project provides practical exposure to ServiceNow Incident Management, JavaScript-based client-side scripting, form customization, validation, and data integrity.

---

# 📖 References

* ServiceNow Platform Documentation
* ServiceNow Incident Management
* ServiceNow Client Scripts
* ServiceNow UI Policies
* ServiceNow GlideForm API
* ServiceNow Developer Resources

---

# 👩‍💻 Author

**Minnath Hassana**

B.Sc. Computer Science

---

# 📁 Repository Contents

This repository contains:

* 📄 Project README
* 📁 Project Documentation
* 📁 Phase-wise Documentation
* 📁 ServiceNow Screenshots
* 📝 Project Implementation Details
* 🧪 Testing Evidence

---

# ⭐ Project Keywords

`ServiceNow` `Incident Management` `Client Script` `UI Policy` `JavaScript` `GlideForm` `ITSM` `Form Validation` `Data Integrity` `onLoad` `onChange` `onSubmit` `onCellEdit`

---

## 🔖 Project Summary

**Project:** Implement Client Script & UI Policy (Incident)

**Platform:** ServiceNow

**Module:** Incident Management

**Technology:** JavaScript, ServiceNow Client Scripts, UI Policies, GlideForm

**Purpose:** Client-side validation, automation, dynamic form control, and Incident data integrity.
