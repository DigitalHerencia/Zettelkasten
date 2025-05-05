---
id: 5ppfzolpar9q2dx4wetiiql
title: API-Documentation
desc: ''
updated: 1742878858988
created: 1742878842045
---
# API Documentation

This document outlines the main API endpoints and server actions for Project Studio.

## Endpoints

### 1. **Upload Project**
- **URL:** `/api/upload`
- **Method:** `POST`
- **Description:**  
  Accepts a ZIP file or GitHub repo URL of a Next.js project.
- **Request Body:**  
  - `file` (if uploading a ZIP) – FormData file upload.
  - `githubUrl` (if providing a URL) – JSON string.
- **Response:**  
  - `projectId` – A unique identifier for the uploaded/parsed project.

### 2. **Analyze Project**
- **URL:** `/api/analyze`
- **Method:** `POST`
- **Description:**  
  Triggers AST parsing and diagram generation for the provided project.
- **Request Body:**  
  - `projectId` – The unique project identifier.
- **Response:**  
  - JSON structure containing:
    - `dependencyGraph` – Data representing file dependencies and Next.js–specific artifacts.
    - `dataModelGraph` – Data representing the data model (ERD/UML) extracted from model definitions.

### 3. **Save/Update Configuration**
- **URL:** `/api/config`
- **Method:** `POST` or `PUT`
- **Description:**  
  Saves or updates configuration files and user customizations.
- **Request Body:**  
  - `projectId` – The unique project identifier.
  - `configFiles` – An object containing file names and content (e.g., package.json, .eslintrc.js).
- **Response:**  
  - Success status and updated configuration details.

### 4. **Fetch Project Blueprint**
- **URL:** `/api/project/[projectId]`
- **Method:** `GET`
- **Description:**  
  Retrieves all saved data (configuration files, diagram data, directory tree) for the specified project.
- **Response:**  
  - A JSON object containing project blueprint data.

## Error Handling

- API responses include proper HTTP status codes.
- Errors are logged and returned with descriptive messages for troubleshooting.

This API design provides the backbone for file uploads, AST parsing, diagram generation, configuration management, and retrieval of project blueprints.
