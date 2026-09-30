<img width="1366" height="768" alt="Screenshot (15)" src="https://github.com/user-attachments/assets/dfe7e0bb-896a-4fe2-aefc-63d39b58cbba" />

<img width="1366" height="768" alt="Screenshot (12)" src="https://github.com/user-attachments/assets/ffda076e-426c-42ef-ba7b-c755cadac8b8" />



Auto Ticket Classification — ServiceNow
 Project Overview

Auto Ticket Classification is a ServiceNow-based project that automatically classifies incoming support tickets and assigns them to the appropriate category based on the information provided in the ticket.

The project was developed and tested using a ServiceNow Developer Instance.

The objective is to reduce manual ticket classification, improve ticket routing, and make the incident management process more efficient.

# Objectives

Automatically classify incoming tickets.

Reduce manual effort for Service Desk agents.

Standardize ticket categorization.

Improve incident routing.

Automatically populate relevant ticket fields.

Demonstrate automation capabilities within ServiceNow.

# ServiceNow Environment

The project was implemented using:

ServiceNow Developer Instance

Incident Management

ServiceNow Tables

Business Rules

Client Scripts

UI Policies

Flow Designer / Workflow

Script Includes

Server-side JavaScript

ServiceNow Form and List views

# Project Workflow
        ┌─────────────────────┐
        │   User Creates      │
        │      Ticket         │
        └──────────┬──────────┘
                   │
                   ▼
        ┌─────────────────────┐
        │ Ticket Information  │
        │   is analyzed       │
        └──────────┬──────────┘
                   │
                   ▼
        ┌─────────────────────┐
        │ Classification Logic │
        │     is executed      │
        └──────────┬──────────┘
                   │
                   ▼
        ┌─────────────────────┐
        │ Category / Subcategory│
        │    is identified     │
        └──────────┬──────────┘
                   │
                   ▼
        ┌─────────────────────┐
        │ Assignment / Routing│
        └──────────┬──────────┘
                   │
                   ▼
        ┌─────────────────────┐
        │ Classified Incident │
        └─────────────────────┘

#ServiceNow Table

The primary table used for the project is:

Incident [incident]


Important incident fields include:

Field	Purpose
Number	Unique incident number
Short Description	Main ticket description
Description	Detailed ticket information
Category	Classification category
Subcategory	More specific classification
Priority	Incident priority
Assignment Group	Team responsible for the ticket
Assigned To	Individual handling the ticket
State	Current incident state
#Ticket Classification

The classification logic analyzes information entered into the ticket, particularly the Short Description and/or Description fields.

Example classifications:

Ticket Description	Category
Password reset required	Software
Laptop is not working	Hardware
Unable to access application	Software
Network connection unavailable	Network
Request for new laptop	Hardware
Email is not working	Software

The categories and classification rules can be customized according to the organization's requirements.

# ServiceNow Components Used
1. Incident Form

The Incident form is used by users or Service Desk agents to create and manage tickets.

The classification process uses information entered into the incident fields.

2. Business Rule

A Business Rule can be used to execute the classification logic when an incident is created or updated.

Example use case:

When:
    Incident is inserted

Then:
    Analyze ticket description
    Determine category
    Set category/subcategory
    Route the incident


Example server-side logic:

(function executeRule(current, previous) {

    var description = (current.short_description + ' ' +
                       current.description).toLowerCase();

    if (description.indexOf('password') >= 0 ||
        description.indexOf('login') >= 0) {

        current.category = 'software';

    } else if (description.indexOf('laptop') >= 0 ||
               description.indexOf('keyboard') >= 0 ||
               description.indexOf('mouse') >= 0) {

        current.category = 'hardware';

    } else if (description.indexOf('network') >= 0 ||
               description.indexOf('internet') >= 0 ||
               description.indexOf('wifi') >= 0) {

        current.category = 'network';
    }

})(current, previous);


The above is an example implementation. The actual classification logic can be modified based on the rules configured in the Developer Instance.

# Automated Ticket Routing

After classification, the incident can be routed to the appropriate Assignment Group.

Example:

Hardware Issue
      ↓
Hardware Support

Software Issue
      ↓
Software Support

Network Issue
      ↓
Network Support


This helps reduce the need for Service Desk agents to manually determine the appropriate support team.

# Flow Designer

The project can also use Flow Designer to automate the classification and routing process.

Example flow:

Trigger
   ↓
Incident Created
   ↓
Get Incident Details
   ↓
Evaluate Ticket
   ↓
Determine Category
   ↓
Update Incident
   ↓
Set Assignment Group
   ↓
Complete

Example Flow Actions

Trigger: Incident Created

Get Record

If / Else conditions

Update Record

Assign Assignment Group

Update Category/Subcategory

#Example
Input Incident
Short Description:
Unable to connect to office Wi-Fi

Description:
My laptop cannot connect to the office wireless network.

Classification
Category:
Network

Assignment Group:
Network Support

Result
Incident
   ↓
Ticket Analysis
   ↓
Network Classification
   ↓
Network Support Assignment

#Testing

The classification logic was tested using different types of incident descriptions.

Example test cases:

Test Case	Input	Expected Result
1	Password reset required	Software
2	Laptop screen not working	Hardware
3	Internet connection unavailable	Network
4	Application login issue	Software
5	Keyboard not working	Hardware

Testing was performed within the ServiceNow Developer Instance by creating and updating incident records.

# Benefits

Reduces manual ticket categorization.

Improves consistency in incident classification.

Speeds up ticket assignment.

Reduces incorrect routing.

Helps Service Desk teams handle tickets more efficiently.

Demonstrates ServiceNow automation and scripting capabilities.

#Future Enhancements

The project can be extended with more advanced ServiceNow capabilities:

Integration with ServiceNow Predictive Intelligence.

Machine-learning-based ticket classification.

Automatic priority prediction.

Automatic assignment-group prediction.

Natural-language processing for incident descriptions.

Integration with external AI/ML services.

Confidence scores for classifications.

Automated notification to support teams.

Performance dashboards and classification reports.

<img width="1366" height="768" alt="Screenshot (14)" src="https://github.com/user-attachments/assets/47f8c891-cf87-4a50-bbd5-cdd45ab4e222" />

 ServiceNow Concepts Demonstration

This project provides practical experience with:

ServiceNow Developer Instance

Incident Management

Tables and Records

Incident Forms

Business Rules

Client Scripts

UI Policies

Script Includes

GlideRecord

Server-side JavaScript

Flow Designer

Automated Assignment

Ticket Categorization

Incident Routing

 Author:

-TAMILVANAN.S — ServiceNow Development
-VASUDEVAN.M  — Classification Logic
-DIVYASHREE.S— Testing & Documentation
-SATHISHKUMAR.M — Workflow / Automation

Project

Auto Ticket Classification using ServiceNow

Platform

ServiceNow Developer Instance
