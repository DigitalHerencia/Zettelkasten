---
id: f4y2483r0e0yweb0ruprck6
title: prompt
desc: ''
updated: 1741286699948
created: 1741286676366
---
# LLM Prompt: DoorDash-Style Delivery PWA MVP Development

You are tasked with developing a demo-ready MVP of a **DoorDash-style Progressive Web App (PWA)** optimized for Next.js, React 19, and TypeScript. Use the provided resources and guidelines to implement simulated functionality clearly marked for easy upgrades to full production.

## Provided Resources & Documents:

1. **User Stories**
   - Understand the roles clearly:
     - **Customers:** Profile management, secure ordering, real-time tracking.
     - **Drivers:** Delivery management, secure navigation, communication.
     - **Admins:** User management, system monitoring, privacy compliance.

2. **Technical Requirements**
   - Implement the frontend using Next.js (App Router), Tailwind CSS, and ShadCN components.
   - Backend serverless functions via Vercel, RTK Query for state management.
   - MongoDB database integration (simulated via JSON or local mock database initially).
   - Mapbox for real-time geospatial functionality (initially simulated).
   - Clerk Authentication with ABAC roles.

3. **Security & Privacy White Paper**
   - Ensure end-to-end encryption standards and anonymity features.
   - Implement minimal data handling strategies, secure authentication, and privacy compliance.

4. **Mapbox Integration Whitepaper**
   - Use Mapbox API guidelines to integrate simulated maps and location tracking.
   - Clearly separate mock data functions to facilitate transition to production keys and APIs.

5. **SMS & Messaging Integration Documents**
   - Integrate Twilio or Telegram APIs via Next.js serverless functions.
   - Initially simulate messaging interactions through mock API routes.

## Implementation Requirements

### Frontend MVP Demo:
- Create interactive dashboards for drivers and customers with simulated data.
- Implement placeholder components clearly marked for future production API integration.
- Include simulated order placement, tracking, and payment processing.

### Backend MVP Demo:
- Mock API routes in Next.js to simulate database CRUD operations and notifications.
- Clearly comment each function and simulate API responses.
- Implement easily switchable environment variables for transitioning to production.

### Security and Privacy Considerations:
- Demonstrate encrypted messaging workflows and secure authentication in simulated environment.
- Include comprehensive comments referencing security practices outlined in the white paper.

### Geospatial Functionality:
- Simulate real-time tracking on Mapbox integrated maps.
- Clearly separate simulated data from Mapbox integration logic.

## Using Provided Documents:
- **User Stories:** Reference to ensure alignment with user expectations during development.
- **Technical Requirements:** Validate your tech stack decisions and adherence to recommended architecture.
- **Security & Privacy White Paper:** Ensure all simulated components are designed with secure transitions to production-level encryption and privacy features.
- **Mapbox Integration Guide:** Follow outlined steps to seamlessly upgrade simulated location functionality to actual Mapbox integration.
- **SMS & Messaging Guide:** Use detailed instructions to simulate interactions and prepare for simple integration of real messaging APIs.

## Outcome
Deliver an MVP clearly structured and documented, allowing straightforward transition from simulated features to full-scale, secure, production-ready implementation. Include inline documentation referencing provided knowledge documents to facilitate future development by an LLM or developer.

