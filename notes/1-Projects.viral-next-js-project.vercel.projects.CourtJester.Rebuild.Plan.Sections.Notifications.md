---
id: um2b9s9t2d967lm214ms5pd
title: Notifications
desc: ''
updated: 1742226815946
created: 1742226689215
---
# 1\. Notification Storage and Creation

## Database Storage

-   **Persistent Storage:**  
    When a new offender logs in (i.e., when an inmate number is submitted for the first time and validated), your backend creates a notification record.
    -   **Where?**  
        The notification is stored in your MongoDB database. This record will typically include fields such as:
        -   **\_id:** Unique identifier for the notification.
        -   **offenderId:** The ID of the offender who just registered.
        -   **title:** For example, "New Offender Registration."
        -   **message:** A short message such as "New registration for inmate number XXXXX."
        -   **type:** Could be "system" or a specific type (like "registration").
        -   **status:** Initially set to "unread."
        -   **createdAt:** A timestamp of when the notification was created.

## API Creation

-   **API Endpoint:**  
    In your API endpoints (for example, in `app/api/inmate/login/route.ts`), after validating the inmate number and creating a new offender record, you call a function like `storeNotification(notification)` to save this notification into the database.
    
    For instance:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// In inmate login endpoint:</span></span><span>
    </span><span><span class="hljs-comment">// ...</span></span><span>
    </span><span><span class="hljs-keyword">if</span></span><span> (!offender) {
      offender = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">createOffender</span></span><span>({ inmateNumber, </span><span><span class="hljs-attr">profileEnabled</span></span><span>: </span><span><span class="hljs-literal">false</span></span><span> });
      </span><span><span class="hljs-keyword">const</span></span><span> notification = {
        </span><span><span class="hljs-attr">offenderId</span></span><span>: offender.</span><span><span class="hljs-property">_id</span></span><span>,
        </span><span><span class="hljs-attr">title</span></span><span>: </span><span><span class="hljs-string">"New Offender Registration"</span></span><span>,
        </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">`New registration for inmate number <span class="hljs-subst">${inmateNumber}</span></span></span><span>.`,
        </span><span><span class="hljs-attr">type</span></span><span>: </span><span><span class="hljs-string">"system"</span></span><span>,
        </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-string">"unread"</span></span><span>,
        </span><span><span class="hljs-attr">createdAt</span></span><span>: </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Date</span></span><span>().</span><span><span class="hljs-title function_">toISOString</span></span><span>(),
      };
      </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">storeNotification</span></span><span>(notification);
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Registration received. You will be notified soon when your profile is ready."</span></span><span> });
    }
    </span><span><span class="hljs-comment">// ...</span></span><span>
    </span></span></code></div></div>
    
    
-   **Removing Mock Data:**  
    In our final version, there’s no mock data or fallback for notifications. Every notification comes directly from a call to the API and is persisted in the database.
    
## 2\. Notification Display

### Persistent Notifications (Admin Dashboard)

-   **Retrieval via API:**  
    The admin dashboard fetches notifications from the database by calling a GET request to an endpoint like `/api/admin/notifications/route.ts`. This endpoint queries the database for all notifications (or only those that are unread) and returns them as JSON.
    
    Example GET handler:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">GET</span></span><span>(</span><span><span class="hljs-params">request: NextRequest</span></span><span>) {
      </span><span><span class="hljs-keyword">try</span></span><span> {
        </span><span><span class="hljs-keyword">const</span></span><span> notifications = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">getAllNotifications</span></span><span>(); </span><span><span class="hljs-comment">// This function queries your database.</span></span><span>
        </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>(notifications);
      } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
        </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error fetching notifications:"</span></span><span>, error);
        </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to fetch notifications"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
      }
    }
    </span></span></code></div></div>
    
    
-   **UI Presentation:**  
    The admin dashboard might include a Notifications tab where each notification is listed. Admins can see details like the offender’s inmate number, registration time, and can mark notifications as read or delete them as needed.
    

### Ephemeral Notifications (User Feedback with Toasts)

-   **Toast Notifications:**  
    In addition to the persistent notifications stored in the database, your app uses Toasts to provide immediate, transient feedback to users. For example:
    
    -   When an offender submits their inmate number, the UI might display a Toast message saying, "Registration received. You will be notified soon when your profile is ready."
    -   When an admin successfully deletes a notification or sends a profile-ready notification to an offender, a Toast appears confirming the action.
-   **Difference in Usage:**
    
    -   **Persistent notifications:** Are stored in the database and displayed in a dedicated section (e.g., on the admin dashboard). They persist until you or the system marks them as read or deletes them.
    -   **Toast notifications:** Are meant for quick, immediate feedback and vanish after a few seconds.

___

## 3\. Workflow Summary

1.  **Offender Login and Registration:**
    -   **Input:** The offender enters their inmate number.
    -   **Validation:** Zod validates the number format.
    -   **Profile Check:** The backend checks if the offender already exists in MongoDB.
    -   **New User:**
        -   If not found, a new offender record is created (with `profileEnabled: false`).
        -   A notification is created and stored in MongoDB to alert you that a new registration has occurred.
        -   The offender receives an immediate Toast feedback stating, "Registration received. You will be notified soon when your profile is ready."
2.  **Admin Action:**
    -   **Dashboard Review:** You (the admin) see the new notification on the admin dashboard (fetched via the GET notifications API).
    -   **Profile Setup:** You manually look up the inmate details (from external sources like the Bureau of Prisons or New Mexico DOC) and update the offender profile with complete details.
    -   **Notify Offender:**  
        Once the profile is set up, you send a notification (via another API endpoint) to the offender informing them that their profile is now active. This notification can be sent as a persistent notification and might also trigger a Toast on the offender’s next login.
3.  **Session and Auth:**
    -   **Inmate Token:**  
        After login, a signed token is stored in an HTTP-only cookie to maintain session state. This token represents the offender’s identity (their inmate number) and is used for subsequent requests.
    -   **Admin Token:**  
        Admins log in with the fixed code ("admin86"), and a similar token mechanism secures their session.

___

## Final Considerations

-   **Database vs. API:**  
    All persistent notifications are stored in your database (MongoDB) via API calls. The API endpoints handle both the creation (POST) and retrieval (GET) of these notifications.
    
-   **UI Integration:**  
    The admin dashboard will render a list of these notifications, and Toast notifications provide immediate user feedback for actions like login, profile update, or notification deletion.
    
-   **Security:**  
    Although the data is public, using HTTP-only cookies and signed tokens for session management protects against common vulnerabilities like XSS. Even though the system is simple, these best practices help maintain consistency and safety.
    

This approach ensures that once an offender logs in, you get notified, and later, you can update their profile and notify them back—all while keeping a clear separation between persistent notifications (stored in your database) and transient, user-friendly Toast messages in your UI.