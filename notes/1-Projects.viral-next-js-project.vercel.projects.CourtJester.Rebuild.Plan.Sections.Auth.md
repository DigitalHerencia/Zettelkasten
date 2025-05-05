---
id: 2df3opkve2n84a26edinyh8
title: Auth
desc: ''
updated: 1742226593659
created: 1742226553129
---
# Authentication Strategy Overview

Since nothing in your system is meant to be “secret” and you’re using a simple single-field login (the inmate number, which acts as both username and password), the primary goal is to validate the input (using Zod, as you mentioned), confirm that it’s a real inmate number (by comparing it against known external sources), and then create or retrieve the corresponding user profile from your database. For the admin, you’re using a fixed code ("admin86").

Even though the data is public, you still want to keep the sessions secure enough so that a user can’t accidentally impersonate someone else or switch between profiles without a proper session mechanism.

___

## Recommended Approach: HTTP-Only Cookies with Signed Tokens

1.  **Input Validation and Profile Lookup:**
    
    -   **Zod Validation:**  
        Use Zod to ensure that the inmate number provided is valid (for example, matches patterns for the Bureau of Prisons or New Mexico corrections).
        
    -   **Profile Creation/Lookup:**  
        Once validated, send the inmate number to your backend. Here, check if a profile exists in your MongoDB database:
        
        -   **If it exists:** Return the profile.
        -   **If not:** Create a new profile with `profileEnabled: false` (and trigger a notification to you for manual profile setup).
2.  **Authentication State and Session Management:**
    
    Since you’re not using a separate password, the key is to establish a session that indicates “this user has logged in with this inmate number.”
    
    **Use HTTP-Only Cookies with a Signed Token:**
    
    -   **Generate a Token:**  
        After a successful login (or registration), create a signed token (for example, using JWT). This token might simply encode the inmate number and a timestamp.
        
    -   **Store in an HTTP-Only Cookie:**  
        Set the token in an HTTP-only cookie. This means the cookie isn’t accessible via JavaScript on the client side (reducing the risk of XSS) and is sent automatically with each request.
        
    -   **Session Validation:**  
        On every protected API endpoint or page load, decode and verify the token from the cookie. This confirms the user is authenticated as that inmate.
        
    
    **Benefits:**
    
    -   **Security:** HTTP-only cookies are a secure way to store session tokens. Even if the token isn’t highly sensitive (because everything’s public), using http-only cookies is best practice.
    -   **Simplicity:** Since you’re using only one field (the inmate number), the JWT payload can be minimal (inmate number and an expiration time).
3.  **Admin Authentication:**
    
    -   **Fixed Code ("admin86"):**  
        For admin login, you can follow a similar pattern. When an admin enters "admin86", create a separate signed token (or simply mark the session as admin) and store it in an HTTP-only cookie.
        
    -   **Separation:**  
        Ensure that your endpoints check for the admin token (or a flag within the token) when needed. For example, your `isAdminRequest` helper might decode the token and verify it has an admin flag.
        
4.  **Storage Considerations:**
    
    -   **MongoDB:**  
        You might want to store user profiles (inmate profiles) in MongoDB. However, you don’t necessarily have to store the raw inmate number as a “password” – the authentication is stateless once the token is issued.
        
    -   **Session Store (Optional):**  
        For an even more robust system, you could maintain a session store in MongoDB (or another database) where you keep active sessions, but for a simple system, a signed token in an HTTP-only cookie is sufficient.
        

___

## Example Workflow

1.  **User Submits Inmate Number:**
    
    -   The client sends a POST request to `/api/inmate/login` with the inmate number.
    -   Zod validates the number.
    -   The backend checks MongoDB:
        -   If the profile exists and is enabled, it issues a JWT token.
        -   If not, it creates the profile (with `profileEnabled: false`) and sends a notification to the admin. It then issues a token that reflects the “pending” state.
    -   The token is set as an HTTP-only cookie in the response.
2.  **Subsequent Requests:**
    
    -   Each time the user (or admin) makes a request, the token is automatically sent.
    -   Your API endpoints verify the token to authenticate the user.
3.  **Admin Login:**
    
    -   The admin enters "admin86" on a login form.
    -   The backend verifies the code and issues an admin token stored in an HTTP-only cookie.
    -   Admin-only endpoints check for this token.

___

## Final Thoughts

For your simple auth system:

-   **HTTP-Only Cookies with Signed Tokens** are the recommended method to manage sessions.
-   **JWTs (or a similar signed token mechanism)** provide a simple, stateless way to authenticate users without storing extra credentials.
-   **Data in MongoDB:**  
    Store your inmate profiles and any related information, but don’t store a separate password since the inmate number is self-validating after Zod validation.

This setup keeps your application simple and secure while ensuring that the inmate number is the sole credential for login and that only the admin (with "admin86") can access administrative functions.

If you have further questions or need additional code examples, feel free to ask!