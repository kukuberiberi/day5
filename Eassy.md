## DAY 5 ASSIGNMENT 

# A) User Manual Procedure (20 minutes)


How to Set Up a GitHub Repository and Make Your First Commit
This guide walks you through creating a new project repository on GitHub and uploading your first set of files from your local computer using the command line.

Prerequisites
Before starting this procedure, ensure you have the following:

A web browser with an active account on GitHub.


Git installed on your computer.


A terminal application (Terminal on macOS/Linux or Git Bash / Command Prompt on Windows).


Basic familiarity with navigating folders using your command terminal.


Step-by-Step Instructions
Log in to GitHub.



Action: Open your browser, navigate to [https://github.com](https://github.com), and sign in to your account.


Expected Result: You see your GitHub dashboard homepage.


Create a new repository on GitHub.



Action: Click the "+" icon in the top-right corner of the page and select New repository.


Expected Result: The "Create a new repository" configuration page loads.


Configure your repository details.



Action: Type my-first-repo into the Repository name field, leave the visibility set to Public, and click Create repository.


Expected Result: GitHub creates the empty repository and displays a page containing quick setup commands and your repository URL.


Screenshot Description:
A screenshot of the GitHub repository setup landing page. The image highlights the HTTPS repository URL (e.g., [https://github.com/username/my-first-repo.git](https://github.com/username/my-first-repo.git)) and the section titled "…or create a new repository on the command line" containing the quick-start terminal commands.


Create a project folder on your local computer.



Action: Open your terminal, navigate to where you store projects, and type mkdir my-first-repo && cd my-first-repo.


Expected Result: A new folder named my-first-repo is created, and your terminal directory changes into this folder.


Initialize Git in your local folder.



Action: Type git init in your terminal and press Enter.


Expected Result: The terminal outputs Initialized empty Git repository in....


Create a starter file.



Action: Type echo "# My First Repo" > README.md in your terminal and press Enter.


Expected Result: A file named README.md containing the text # My First Repo is created in your folder.


Stage the file for commit.



Action: Type git add README.md in your terminal and press Enter.


Expected Result: The terminal returns to a new prompt line with no error messages.


Commit the staged file.



Action: Type git commit -m "Initial commit" in your terminal and press Enter.


Expected Result: The terminal displays output indicating 1 file changed and insertions made.


Link your local repository to GitHub.



Action: Copy the URL from your GitHub repository page (from Step 3) and run git remote add origin <YOUR-REPOSITORY-URL> in your terminal (replace <YOUR-REPOSITORY-URL> with your actual link).


Expected Result: The terminal silently completes the command with no errors.


Push your code to GitHub.



Action: Type git push -u origin main (or git push -u origin master depending on your default branch) and press Enter.


Expected Result: The terminal shows transfer progress ending with Branch 'main' set up to track remote branch 'main' from 'origin'.


Verify your upload on GitHub.



Action: Refresh your repository page in your web browser.


Expected Result: You see your README.md file listed and rendered on the repository homepage.


Troubleshooting
Issue: fatal: remote origin already exists


Cause: You ran the git remote add origin command more than once or linked a previous project to the same remote name.


Solution: Run git remote remove origin in your terminal to remove the incorrect link, and then re-run the git remote add origin <YOUR-REPOSITORY-URL> command with your correct URL.


B) API Reference Entry (25 minutes)

API Reference: Create a New Task
Overview
This endpoint allows an authenticated user to create a new task within a project. It accepts task details in the request body, creates the record in the system, and returns the newly created task object.

Endpoint Information
HTTP Method: POST


Path: /api/v1/projects/{project_id}/tasks


Content-Type: application/json
Request Headers
Header Name
Type
Required
Description
Authorization
String
Yes
Bearer token formatted as Bearer <your_token_here> to authenticate the requesting user.
Content-Type
String
Yes
Must be set to application/json.

Request Parameters
Path Parameters
Parameter
Type
Required
Description
project_id
String
Yes
The unique identifier (UUID) of the project where the task will be created.

Body Parameters
Parameter
Type
Required
Description
title
String
Yes
The title or headline of the task (1–100 characters).
description
String
Optional
Detailed text describing the task details or requirements.
assignee_id
String
Optional
The unique identifier (UUID) of the user assigned to the task.
due_date
String
Optional
The deadline date formatted as an ISO 8601 timestamp (e.g., YYYY-MM-DD or YYYY-MM-DDTHH:MM:SSZ).
priority
String
Optional
The urgency level of the task. Acceptable values: "low", "medium", "high". Default is "medium".

Example Request Body
JSON
{
  "title": "Set up database migrations",
  "description": "Create initial PostgreSQL tables for users and authentication using Knex.js.",
  "assignee_id": "usr_98765432-10ab-cdef-0123-456789abcdef",
  "due_date": "2026-10-15T17:00:00Z",
  "priority": "high"
}


Response Status Codes
Code
Status
Description
201
Created
The task was created successfully. Returns the full task object.
400
Bad Request
Request validation failed (e.g., missing required title, invalid priority value, or malformed JSON).
401
Unauthorized
The request lacks a valid Authorization header or the authentication token has expired.
403
Forbidden
The authenticated user does not have permission to create tasks in the specified project.
404
Not Found
The specified project_id or assignee_id does not exist.
500
Internal Server Error
An unexpected server error occurred while processing the request.

Example Successful Response (HTTP 201 Created)
JSON
{
  "success": true,
  "data": {
    "id": "tsk_12345678-abcd-ef01-2345-6789abcdef01",
    "project_id": "prj_55555555-aaaa-bbbb-cccc-111122223333",
    "title": "Set up database migrations",
    "description": "Create initial PostgreSQL tables for users and authentication using Knex.js.",
    "status": "todo",
    "priority": "high",
    "assignee_id": "usr_98765432-10ab-cdef-0123-456789abcdef",
    "creator_id": "usr_11112222-3333-4444-5555-666677778888",
    "due_date": "2026-10-15T17:00:00Z",
    "created_at": "2026-09-30T16:00:00Z",
    "updated_at": "2026-09-30T16:00:00Z"
  }
}

