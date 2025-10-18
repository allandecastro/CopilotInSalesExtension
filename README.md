# Copilot In Sales — Example Adaptive Dialogs

This repository contains example Adaptive Dialogs for Copilot in Sales (Dynamics 365 / Power Platform) showing common scenarios:
- Add a note to an Opportunity
- Create a Case from an Account
- Provide custom Copilot Sparks groups

Files
- [AddNoteToOpportunity.yaml](AddNoteToOpportunity.yaml)
- [CreateCaseFromAccount.yaml](CreateCaseFromAccount.yaml)
- [CustomSalesParks.yaml](CustomSalesParks.yaml)

Quick overview of each example

1) Add Note to Opportunity
- Trigger phrases: "add note to opportunity", "attach note to opportunity", etc.
- Flow:
  - Asks for an Opportunity ID or name (see [`Topic.OpportunityIdentifier`](AddNoteToOpportunity.yaml)).
  - Looks up the opportunity via the connector (`GetItemWithOrganization`).
  - Prompts for note text (see [`Topic.ContentNote`](AddNoteToOpportunity.yaml)).
  - Creates an annotation (note) attached to the opportunity and returns a link using [`Topic.CreateRecordWithOrganization.annotationid`](AddNoteToOpportunity.yaml).
- See implementation: [AddNoteToOpportunity.yaml](AddNoteToOpportunity.yaml)

2) Create Case from Account
- Trigger phrases: "Create a case for this account", "Open a case for this customer", etc.
- Flow:
  - Detects account context from page context or selected record (see [`Topic.varAccountRecordId`](CreateCaseFromAccount.yaml) and Global page context checks).
  - Collects case title and description (see [`Topic.CaseTitle`](CreateCaseFromAccount.yaml) and [`Topic.CaseDescription`](CreateCaseFromAccount.yaml)).
  - Collects contact name fields ([`Topic.FirstNameContact`](CreateCaseFromAccount.yaml), [`Topic.LastNameContact`](CreateCaseFromAccount.yaml)).
  - Calls a sub-dialog/action and returns the created case id and number ([`Topic.caseid`](CreateCaseFromAccount.yaml), [`Topic.casenumber`](CreateCaseFromAccount.yaml)).
- See implementation: [CreateCaseFromAccount.yaml](CreateCaseFromAccount.yaml)

3) Custom Sparks (Sparks catalog)
- Demonstrates adding custom Copilot Sparks groups surfaced to the UI.
- Defines `Global.MyCustomSparksGroup` and merges it into `Global.PA_Copilot_Sparks.sparkGroups` (see [`Global.MyCustomSparksGroup`](CustomSalesParks.yaml) and [`Global.PA_Copilot_Sparks.sparkGroups`](CustomSalesParks.yaml)).
- See implementation: [CustomSalesParks.yaml](CustomSalesParks.yaml)

How to use these examples
- Open the YAML files in Visual Studio Code to review and adapt the dialogs:
  - [AddNoteToOpportunity.yaml](AddNoteToOpportunity.yaml)
  - [CreateCaseFromAccount.yaml](CreateCaseFromAccount.yaml)
  - [CustomSalesParks.yaml](CustomSalesParks.yaml)
- Trigger the dialogs in your Copilot in Sales environment using the example trigger phrases in each file.
- Inspect and adapt variables and connector references:
  - Note/opportunity variables: [`Topic.OpportunityIdentifier`](AddNoteToOpportunity.yaml), [`Topic.ContentNote`](AddNoteToOpportunity.yaml)
  - Case variables: [`Topic.varAccountRecordId`](CreateCaseFromAccount.yaml), [`Topic.CaseTitle`](CreateCaseFromAccount.yaml), [`Topic.CaseDescription`](CreateCaseFromAccount.yaml), [`Topic.FirstNameContact`](CreateCaseFromAccount.yaml), [`Topic.LastNameContact`](CreateCaseFromAccount.yaml), [`Topic.caseid`](CreateCaseFromAccount.yaml), [`Topic.casenumber`](CreateCaseFromAccount.yaml)
  - Sparks variables: [`Global.MyCustomSparksGroup`](CustomSalesParks.yaml), [`Global.PA_Copilot_Sparks.sparkGroups`](CustomSalesParks.yaml)

Notes and pointers
- These examples use connector actions (GetItemWithOrganization / CreateRecordWithOrganization) — adapt the connection reference and environment URLs to match your tenant.
- The Adaptive Dialogs use built-in Question/Condition/InvokeConnectorAction steps — reuse patterns when building new dialogs.