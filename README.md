# insomniaapitesting

Automating the KRI Response Process – Documentation

Version: 1.0
Author: [Your Name]
Date: [Date]

⸻

1. Introduction

1.1 Purpose

This document provides an overview of the Automated KRI Response Process system, outlining its functionalities, design, and implementation. The system enables users to submit responses to Key Risk Indicator (KRI) questionnaires, which are required to be shared with the Reserve Bank of India (RBI) every quarter.

1.2 Stakeholders
	•	BBPLC India Branch
	•	Sree Ganesh Nadgauda
	•	I.R. Roshishankar
	•	Yogesh Bandarkar

1.3 Scope

The system replaces the existing manual spreadsheet-based process with an automated web-based solution that includes features for searching, filtering, bulk uploading, and submitting KRI responses.

⸻

2. System Overview

2.1 Existing Process
	•	Currently, the KRI response process is manual and managed via spreadsheets.
	•	Users manually enter responses, attach spreadsheets, and send them for review.
	•	The manual approach is time-consuming and prone to errors.

2.2 Proposed System

The new system provides a web-based interface for KRI response submission with the following functionalities:
	•	Search & Filter: Users can search for specific KRIs using metric-based search and apply various filter criteria.
	•	Bulk Upload: Users can upload multiple KRI responses at once.
	•	Individual KRI Submission: Each KRI has a Submit button, opening a popover for entering values.
	•	Data Entry: Users fill in fields such as bank response (current/previous quarter), comments, etc.
	•	Confirmation Window: Upon submission, a confirmation dialog appears before finalizing the entry.
	•	Database Integration: The responses are stored in the database using a POST API.
	•	Read-Only Previous Values: Data for previous quarters is displayed in read-only mode.

⸻

3. User Interface (UI) Design

3.1 Landing Page

The landing page consists of:
	•	Search Bar: Users can enter a metric to find relevant KRIs.
	•	Filters: Various filters can be applied to refine the search.
	•	Clear Filters Button: Allows resetting filters.
	•	Data Table: Displays KRIs with the following columns:
	•	ID
	•	KRI Name
	•	Accountable Team
	•	Data Provider
	•	Submit Button (for individual KRI entry)
	•	Bulk Upload Feature: Allows multiple KRIs to be updated simultaneously.

3.2 KRI Submission Window

When a user clicks the Submit button for a KRI, a popover appears where they enter the following:
	•	Bank Response (Current Quarter)
	•	Bank Response (Previous Quarter) [Read-Only]
	•	Comments (Current Quarter)
	•	Comments (Previous Quarter) [Read-Only]
	•	Clear Button: Resets fields before submission.
	•	Submit Button: Confirms data entry and triggers a confirmation window.

3.3 Confirmation Window
	•	Appears after submission to confirm the entered data.
	•	On confirmation, the data is stored in the database via a POST API.

⸻

4. Backend Implementation

4.1 API Endpoints

The system uses RESTful APIs for data retrieval and submission.

4.1.1 GET API (Fetching Existing Data)
	•	Endpoint: /api/kri-responses
	•	Method: GET
	•	Parameters:
	•	metric_id (optional) – Fetch data for a specific metric.
	•	filters (optional) – Apply filters to refine search results.
	•	Response Format:

[
  {
    "id": 101,
    "kri": "Operational Risk",
    "accountable_team": "Risk Management",
    "data_provider": "Finance Team",
    "previous_quarter_response": "Low Risk",
    "current_quarter_response": null
  }
]
{
  "kri_id": 101,
  "current_quarter_response": "Moderate Risk",
  "comments": "Increased operational challenges"
}

4.1.2 POST API (Submitting KRI Response)
	•	Endpoint: /api/kri-submit
	•	Method: POST
	•	Request Body:

 4.2 Backend Logic Implementation
	•	Serializer Creation: Used to transform data models into JSON responses.
	•	API Handlers: Functions written to process GET and POST requests.
	•	Validation Checks: Ensures correct input data types and prevents duplicate submissions.
	•	Database Integration: Data is stored and retrieved efficiently using ORM queries.
