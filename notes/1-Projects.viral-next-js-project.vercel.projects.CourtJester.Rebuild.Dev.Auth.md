---
id: unpfhixpbzi1019bovs6c7m
title: Aut
desc: ''
updated: 1742225956439
created: 1742225936189
---
# Revised Authentication and Notification Flow

## New Requirements Overview

-   **User Authentication:**  
    Inmates do not have a separate password. They use a valid inmate number as both the username and the password to access their profile.
    
-   **Admin Access:**  
    The admin dashboard is accessed using a fixed code (admin86).
    
-   **Notification on First Login:**  
    When an inmate logs in for the first time (i.e. when there isn’t an existing profile), a notification should be sent to the admin.
    
    -   The inmate sees a message: “You will be notified soon when your profile is ready.”
    -   Meanwhile, the admin receives a notification so that you (manually) can set up their profile (including cases, reminders, notifications, and motions).

___

# Adjustments in the Codebase

## 1\. **Authentication Changes**

-   **Inmate Login Page:**
    -   Replace any authentication logic that uses external providers with a simple form that takes an inmate number.
    -   Validate that the provided inmate number exists in your database.
    -   Since the inmate number acts as both the username and password, a basic check (e.g., matching against a list of valid inmate numbers) can be implemented.
    -   If the inmate’s profile does not yet exist, redirect them to a page showing the message that their profile is pending.
-   **Admin Dashboard:**
    -   Remove the `requireAdmin` middleware for user-related endpoints if they are to be accessible via this simplified authentication.
    -   For the admin area, implement a simple check against the input code (admin86) instead of a full auth system.
    -   Ensure that this code is compared securely (e.g., using environment variables if needed) so that it isn’t hard-coded in production code.

## 2\. **Notification and Profile Setup Behavior**

-   **First-Time Inmate Submission:**
    -   When an inmate number is submitted for the first time:
        -   **Trigger a Notification:**  
            Create a notification entry that informs the admin that a new inmate registration has occurred. This notification can include the inmate number and any other identifying information.
        -   **Show User Message:**  
            The inmate is shown a message such as:  
            _“Your inmate number has been received. You will be notified soon when your profile is ready.”_
    -   **Profile Setup by Admin:**  
        The admin dashboard should list such notifications. The admin will then manually create the inmate’s profile, enter their cases, set up reminders, and prepare notifications/motions. Once set up, the admin can send a final notification to the inmate indicating that their profile is now active.

## 3\. **Code Adjustments (Examples)**

-   **Inmate Login Component:**
    
    -   Remove any calls to external auth or require functions.
    -   Add a simple form with an input field for the inmate number.
    -   On submission, perform a lookup in your database:
        -   If a matching profile is found, redirect to the profile page.
        -   If not found, trigger the notification (via an API call) and display the “pending” message.
-   **Admin Dashboard Component:**
    
    -   Change the logic from checking for an authenticated admin (via `requireAdmin`) to verifying that the provided code equals `admin86`.
    -   Optionally, store the admin access code securely (for example, via an environment variable) and compare it on login.
    -   Display a notification list that includes new inmate submissions.
    -   Provide admin controls to mark a notification as “handled” once the inmate’s profile is set up.
-   **API Endpoints:**
    
    -   For endpoints that previously required `requireAdmin`, decide if they need to be protected by the new logic or if they can use a lightweight check.
    -   Modify the notification API:
        -   On first-time inmate login, create a new notification entry.
        -   You can also add metadata (like a flag “newUser” or “profilePending”) to the notification so the admin dashboard can highlight new registrations.

___

# Developer Task Checklist

1.  **Authentication Flow Changes:**
    
    -   [ ]  Implement a simple login form for inmates that accepts an inmate number.
    -   [ ]  Validate that the inmate number exists; if not, consider it a new registration.
    -   [ ]  For new registrations, bypass standard auth and trigger a notification to the admin.
    -   [ ]  Update the admin login form to require the fixed code (`admin86`), and if possible, read this value from a secure environment variable.
2.  **Notification Trigger for First-Time Login:**
    
    -   [ ]  In the login logic, detect if an inmate’s profile is missing.
    -   [ ]  Make an API call to create a new notification for the admin that includes the inmate number.
    -   [ ]  Display a user-facing message: “You will be notified soon when your profile is ready.”
3.  **Admin Dashboard Adjustments:**
    
    -   [ ]  Remove or bypass the `requireAdmin` check in relevant API endpoints if using the new admin code.
    -   [ ]  Update the notifications section to display new inmate submissions clearly.
    -   [ ]  Include a control or button that allows the admin to mark the registration as handled (after setting up the profile).
4.  **Backend and API Updates:**
    
    -   [ ]  Update API endpoints to support the new logic for inmate submissions and notifications.
    -   [ ]  Ensure that the API for notifications can handle creating, listing, and deleting notifications as needed.
    -   [ ]  Adjust error handling where necessary to account for the simplified auth logic.
5.  **Testing and Verification:**
    
    -   [ ]  Test the inmate login process with a valid inmate number (both existing and new).
    -   [ ]  Verify that new registrations trigger a notification to the admin.
    -   [ ]  Check that the admin login works using `admin86`.
    -   [ ]  Ensure that the admin dashboard correctly displays notifications and that you can manually update inmate profiles.
    -   [ ]  Confirm that all fallback behaviors (e.g., showing a pending message) work as intended.
6.  **Cleanup and Documentation:**
    
    -   [ ]  Remove any temporary bypasses or debug code related to authentication.
    -   [ ]  Update documentation to explain the new authentication process and the notification mechanism.
    -   [ ]  Add inline comments explaining that inmate numbers act as both username and password and that admin access is via a fixed code.

___

# Final Thoughts

By making these changes, the system will work as a lightweight identity verification method, where the inmate number alone determines access to a profile. This approach minimizes complexity on the user side while still allowing the admin to maintain control over profile setup and notifications. Following the checklist should help ensure that the revised flow is implemented correctly and tested thoroughly on your local environment.

Feel free to ask if you need further details on any specific part of the implementation.