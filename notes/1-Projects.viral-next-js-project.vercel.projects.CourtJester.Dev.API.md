---
id: cl51pur0urowymzdvs9gnmx
title: API
desc: ''
updated: 1742100768002
created: 1742099334592
---

# API

## Admin Endpoints

### 1. **GET /api/admin/offenders**

1. **Purpose**: List all offenders
2. **Logic**: Retrieves offenders from storage
3. **Storage**: Offender data in blob storage

### 2. **GET /api/admin/offenders/[id]**

1. **Purpose**: Get specific offender details
2. **Logic**: Retrieves offender by ID
3. **Storage**: Offender data in blob storage

### 3. **PATCH /api/admin/offenders/[id]**

1. **Purpose**: Update offender details
2. **Data**: Partial offender object
3. **Logic**: Updates offender in storage
4. **Storage**: Offender data in blob storage

### 4. **DELETE /api/admin/offenders/[id]**

1. **Purpose**: Delete an offender
2. **Logic**: Removes offender from storage
3. **Storage**: Offender data in blob storage

### 5. **GET /api/admin/offenders/[id]/cases**

1. **Purpose**: List cases for an offender
2. **Logic**: Retrieves cases by offender ID
3. **Storage**: Case data in blob storage

### 6. **POST /api/admin/offenders/[id]/cases**

1. **Purpose**: Create a new case for an offender
2. **Data**: Case object
3. **Logic**: Stores case in storage
4. **Storage**: Case data in blob storage

### 7. **GET /api/admin/notifications**

1. **Purpose**: List all notifications
2. **Logic**: Retrieves notifications from storage
3. **Storage**: Notification data in blob storage

### 8. **POST /api/admin/notifications**

1. **Purpose**: Create a new notification
2. **Data**: Notification object
3. **Logic**: Stores notification in storage
4. **Storage**: Notification data in blob storage

### 9. **DELETE /api/admin/notifications/[id]**

1. **Purpose**: Delete a notification
2. **Logic**: Removes notification from storage
3. **Storage**: Notification data in blob storage

### 10. **GET /api/admin/search**

1. **Purpose**: Search for offenders
2. **Query**: `q` (search query)
3. **Logic**: Searches offenders by inmate number or name
4. **Storage**: Offender data in blob storage

### 11. **POST /api/admin/search/inmate**

1. **Purpose**: Search for an inmate by number
2. **Data**: `{ inmateNumber: string }`
3. **Logic**: Searches for inmate in external system
4. **Storage**: None (passes through to external API)

### 12. **POST /api/admin/search/cases**

1. **Purpose**: Search for cases by offender name
2. **Data**: `{ name: string, offenderId: string }`
3. **Logic**: Searches for cases in external system
4. **Storage**: None (passes through to external API)

### 13. **GET /api/admin/motions**

1. **Purpose**: List motions
2. **Query**: `offenderId`, `caseId` (optional filters)
3. **Logic**: Retrieves motions from storage
4. **Storage**: Motion data in blob storage

### 14. **POST /api/admin/motions**

1. **Purpose**: Create a new motion
2. **Data**: Motion object
3. **Logic**: Stores motion in storage
4. **Storage**: Motion data in blob storage

### 15. **GET /api/admin/motions/[id]**

1. **Purpose**: Get specific motion details
2. **Logic**: Retrieves motion by ID
3. **Storage**: Motion data in blob storage

### 16. **PATCH /api/admin/motions/[id]**

1. **Purpose**: Update motion details
2. **Data**: Partial motion object
3. **Logic**: Updates motion in storage
4. **Storage**: Motion data in blob storage

### 17. **DELETE /api/admin/motions/[id]**

1. **Purpose**: Delete a motion
2. **Logic**: Removes motion from storage
3. **Storage**: Motion data in blob storage

### 18. **GET /api/admin/motions/[id]/pdf**

1. **Purpose**: Generate PDF for a motion
2. **Logic**: Creates PDF from motion content
3. **Storage**: Motion data in blob storage

### 19. **GET /api/admin/reminders**

1. **Purpose**: List reminders
2. **Query**: `offenderId`, `status` (optional filters)
3. **Logic**: Retrieves reminders from storage
4. **Storage**: Reminder data in blob storage

### 20. **POST /api/admin/reminders**

1. **Purpose**: Create a new reminder
2. **Data**: Reminder object
3. **Logic**: Stores reminder in storage
4. **Storage**: Reminder data in blob storage

### 21. **GET /api/admin/reminders/[id]**

1. **Purpose**: Get specific reminder details
2. **Logic**: Retrieves reminder by ID
3. **Storage**: Reminder data in blob storage

### 22. **PATCH /api/admin/reminders/[id]**

1. **Purpose**: Update reminder details
2. **Data**: Partial reminder object
3. **Logic**: Updates reminder in storage
4. **Storage**: Reminder data in blob storage

### 23. **DELETE /api/admin/reminders/[id]**

1. **Purpose**: Delete a reminder
2. **Logic**: Removes reminder from storage
3. **Storage**: Reminder data in blob storage

### 24. **GET /api/admin/reminders/process**

1. **Purpose**: Process due reminders
2. **Logic**: Finds due reminders, creates notifications, updates reminder status
3. **Storage**: Reminder and notification data in blob storage

### 25. **POST /api/admin/documents/upload**

1. **Purpose**: Upload a document
2. **Data**: Form data with file
3. **Logic**: Uploads file to Vercel Blob
4. **Storage**: Document data in Vercel Blob

### 26. **POST /api/admin/offenders/mugshot**

1. **Purpose**: Upload an offender mugshot
2. **Data**: Form data with image file
3. **Logic**: Uploads image to Vercel Blob
4. **Storage**: Image data in Vercel Blob

### 27. **POST /api/admin/offenders/profile**

1. **Purpose**: Store offender profile data
2. **Data**: Offender profile object
3. **Logic**: Stores offender profile in storage
4. **Storage**: Offender data in blob storage

## Offender Endpoints

### 1. **GET /api/offender/profile**

1. **Purpose**: Get offender profile
2. **Logic**: Retrieves offender by inmate number from session
3. **Storage**: Offender data in blob storage

### 2. **GET /api/offender/cases**

1. **Purpose**: List cases for the authenticated offender
2. **Logic**: Retrieves cases by offender ID from session
3. **Storage**: Case data in blob storage

### 3. **GET /api/offender/motions**

1. **Purpose**: List motions for the authenticated offender
2. **Query**: `caseId` (optional filter)
3. **Logic**: Retrieves motions by offender ID from session
4. **Storage**: Motion data in blob storage

### 4. **POST /api/offender/motions**

1. **Purpose**: Create a new motion
2. **Data**: Motion object
3. **Logic**: Stores motion in storage
4. **Storage**: Motion data in blob storage

### 5. **GET /api/offender/motions/[id]**

1. **Purpose**: Get specific motion details
2. **Logic**: Retrieves motion by ID
3. **Storage**: Motion data in blob storage

### 6. **PATCH /api/offender/motions/[id]**

1. **Purpose**: Update motion details
2. **Data**: Partial motion object
3. **Logic**: Updates motion in storage
4. **Storage**: Motion data in blob storage

### 7. **DELETE /api/offender/motions/[id]**

1. **Purpose**: Delete a motion
2. **Logic**: Removes motion from storage
3. **Storage**: Motion data in blob storage

### 8. **GET /api/offender/motions/[id]/pdf**

1. **Purpose**: Generate PDF for a motion
2. **Logic**: Creates PDF from motion content
3. **Storage**: Motion data in blob storage

### 9. **GET /api/offender/notifications**

1. **Purpose**: List notifications for the authenticated offender
2. **Logic**: Retrieves notifications by offender ID from session
3. **Storage**: Notification data in blob storage

### 10. **PATCH /api/offender/notifications/[id]**

1. **Purpose**: Update notification status
2. **Data**: Partial notification object
3. **Logic**: Updates notification in storage
4. **Storage**: Notification data in blob storage

### 11. **GET /api/offender/reminders**

1. **Purpose**: List reminders for the authenticated offender
2. **Query**: `status` (optional filter)
3. **Logic**: Retrieves reminders by offender ID from session
4. **Storage**: Reminder data in blob storage

### 12. **POST /api/offender/reminders**

1. **Purpose**: Create a new reminder
2. **Data**: Reminder object
3. **Logic**: Stores reminder in storage
4. **Storage**: Reminder data in blob storage

### 13. **GET /api/offender/reminders/[id]**

1. **Purpose**: Get specific reminder details
2. **Logic**: Retrieves reminder by ID
3. **Storage**: Reminder data in blob storage

### 14. **PATCH /api/offender/reminders/[id]**

1. **Purpose**: Update reminder details
2. **Data**: Partial reminder object
3. **Logic**: Updates reminder in storage
4. **Storage**: Reminder data in blob storage

### 15. **DELETE /api/offender/reminders/[id]**

1. **Purpose**: Delete a reminder
2. **Logic**: Removes reminder from storage
3. **Storage**: Reminder data in blob storage

## Utility Endpoints

### 1. **GET /api/help-content**

1. **Purpose**: Get help content
2. **Logic**: Reads HELP.md file
3. **Storage**: File system
