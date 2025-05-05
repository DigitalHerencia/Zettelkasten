---
id: lcv8rmq4j66uqtoieau5a9d
title: OffenderServices
desc: ''
updated: 1742227045487
created: 1742227045487
---
## 1\. Overview of Offender Services

**Offender Services** are designed to ensure that offenders are alerted to upcoming court dates and other important events. These services include:

-   **Push Notifications / Banner Alerts:**  
    When the offender is using the app (or even when it’s in the background), notifications can be displayed to remind them of upcoming court dates.
    
-   **Reminders / Alarms:**  
    These can be in-app reminders or scheduled notifications that appear at a specified time (for example, an alarm one hour before a court date).
    
-   **Internal Notifications:**  
    If the device doesn’t support native notifications (or the user has not granted permission), you can still display reminders within the app itself (for example, a notifications panel).
    

___

## 2\. Requesting Notification Permissions on the Web

### A. Using the Web Notifications API

Modern browsers provide a [Notifications API](https://developer.mozilla.org/en-US/docs/Web/API/Notifications_API) that allows you to display notifications to users. For a Progressive Web App (PWA), you can also combine this with Service Workers to handle push notifications.

**Basic Steps:**

1.  **Check for API Support:**  
    Ensure the browser supports notifications.
2.  **Request Permission:**  
    Ask the user for permission to display notifications.
3.  **Handle the Response:**  
    If granted, you can create and display notifications.

**Example (in a React component):**


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span><span class="hljs-keyword">import</span></span><span> { useEffect, useState } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"react"</span></span><span>;

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">default</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">NotificationRequester</span></span><span>(</span><span><span class="hljs-params"></span></span><span>) {
  </span><span><span class="hljs-keyword">const</span></span><span> [permission, setPermission] = </span><span><span class="hljs-title function_">useState</span></span><span>(</span><span><span class="hljs-title class_">Notification</span></span><span>.</span><span><span class="hljs-property">permission</span></span><span>);

  </span><span><span class="hljs-title function_">useEffect</span></span><span>(</span><span><span class="hljs-function">() =&gt;</span></span><span> {
    </span><span><span class="hljs-keyword">if</span></span><span> (permission !== </span><span><span class="hljs-string">"granted"</span></span><span>) {
      </span><span><span class="hljs-title class_">Notification</span></span><span>.</span><span><span class="hljs-title function_">requestPermission</span></span><span>().</span><span><span class="hljs-title function_">then</span></span><span>(</span><span><span class="hljs-function">(<span class="hljs-params">perm</span></span></span><span>) =&gt; {
        </span><span><span class="hljs-title function_">setPermission</span></span><span>(perm);
      });
    }
  }, [permission]);

  </span><span><span class="hljs-keyword">const</span></span><span> </span><span><span class="hljs-title function_">showNotification</span></span><span> = (</span><span><span class="hljs-params"></span></span><span>) =&gt; {
    </span><span><span class="hljs-keyword">if</span></span><span> (permission === </span><span><span class="hljs-string">"granted"</span></span><span>) {
      </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Notification</span></span><span>(</span><span><span class="hljs-string">"Court Jester Alert"</span></span><span>, {
        </span><span><span class="hljs-attr">body</span></span><span>: </span><span><span class="hljs-string">"Your court date is coming up!"</span></span><span>,
        </span><span><span class="hljs-attr">icon</span></span><span>: </span><span><span class="hljs-string">"/favicon.ico"</span></span><span>,
      });
    }
  };

  </span><span><span class="hljs-keyword">return</span></span><span> (
    </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">div</span></span></span></span><span>&gt;
      </span><span><span class="hljs-tag">&lt;<span class="hljs-name">p</span></span></span><span>&gt;Notification permission: {permission}</span><span><span class="hljs-tag">&lt;/<span class="hljs-name">p</span></span></span><span>&gt;
      </span><span><span class="hljs-tag">&lt;<span class="hljs-name">button</span></span></span><span> </span><span><span class="hljs-attr">onClick</span></span><span>=</span><span><span class="hljs-string">{showNotification}</span></span><span>&gt;Show Test Notification</span><span><span class="hljs-tag">&lt;/<span class="hljs-name">button</span></span></span><span>&gt;
    </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">div</span></span></span><span>&gt;
  );
}
</span></span></code></div></div>


### B. Handling Push Notifications (Advanced)

If you want notifications to be delivered even when the app isn’t open (i.e., in the background), you need to use push notifications with a Service Worker and a push service (for example, Firebase Cloud Messaging or a custom Web Push solution). This involves:

-   **Service Worker Registration:**  
    Register a Service Worker in your Next.js app.
-   **Subscribe to Push Notifications:**  
    Use the Push API to subscribe the user’s browser to push notifications.
-   **Send Notifications from Your Server:**  
    Your backend (or a third-party service) sends push messages to subscribed devices.

This setup is more involved, but for many applications, the basic Notifications API is sufficient—especially when combined with in-app notifications (like Toasts).

___

## 3\. Scheduling Reminders / Alarms

### A. In-App Reminders

Within your Court Jester app, you can schedule reminders for upcoming court dates using JavaScript timers. For example, you might use `setTimeout` to trigger a reminder a few minutes or hours before the event.

**Example:**


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span><span class="hljs-keyword">import</span></span><span> { useEffect } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"react"</span></span><span>;

</span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">scheduleReminder</span></span><span>(</span><span><span class="hljs-params">courtDate: <span class="hljs-built_in">Date</span></span></span><span>) {
  </span><span><span class="hljs-keyword">const</span></span><span> now = </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Date</span></span><span>();
  </span><span><span class="hljs-keyword">const</span></span><span> timeUntilCourt = courtDate.</span><span><span class="hljs-title function_">getTime</span></span><span>() - now.</span><span><span class="hljs-title function_">getTime</span></span><span>() - </span><span><span class="hljs-number">3600000</span></span><span>; </span><span><span class="hljs-comment">// 1 hour before</span></span><span>
  </span><span><span class="hljs-keyword">if</span></span><span> (timeUntilCourt &gt; </span><span><span class="hljs-number">0</span></span><span>) {
    </span><span><span class="hljs-built_in">setTimeout</span></span><span>(</span><span><span class="hljs-function">() =&gt;</span></span><span> {
      </span><span><span class="hljs-comment">// Display a notification or update the UI to remind the user</span></span><span>
      </span><span><span class="hljs-title function_">alert</span></span><span>(</span><span><span class="hljs-string">"Reminder: Your court date is in 1 hour!"</span></span><span>);
    }, timeUntilCourt);
  }
}

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">default</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">CourtDateReminder</span></span><span>(</span><span><span class="hljs-params">{ courtDate }: { courtDate: <span class="hljs-built_in">Date</span></span></span><span> }) {
  </span><span><span class="hljs-title function_">useEffect</span></span><span>(</span><span><span class="hljs-function">() =&gt;</span></span><span> {
    </span><span><span class="hljs-title function_">scheduleReminder</span></span><span>(courtDate);
  }, [courtDate]);

  </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">div</span></span></span></span><span>&gt;Your court date is scheduled for {courtDate.toLocaleString()}</span><span><span class="hljs-tag">&lt;/<span class="hljs-name">div</span></span></span><span>&gt;;
}
</span></span></code></div></div>


### B. Push Notification Reminders (PWA)

For PWAs, you can schedule push notifications using a Service Worker. Since web standards do not allow precise scheduling via the Push API natively, you may need to use a server-side scheduler that sends out push messages at the appropriate time.

___

## 4\. Integrating Offender Services in Your App

### Workflow for Offender Services

1.  **Offender Login and Profile Check:**  
    When an offender logs in with their inmate number, your backend verifies and, if it’s a new registration, creates a profile with `profileEnabled: false` and sends a notification to the admin.
    
2.  **Admin Dashboard – Document Parsing & Profile Setup:**
    
    -   **Document Parsing Tab:**
        -   **File Upload:** Upload PDFs (e.g., court cases) and use packages like **pdf-parse** to extract text and auto-populate case fields.
        -   **Text Parsing:** Paste text from standardized forms to extract additional profile details.
    -   **Profile Update:**  
        Once all necessary data is parsed, update the offender’s profile in your MongoDB database.
        -   Set `profileEnabled: true`.
        -   Create a notification (e.g., "Your profile is now ready!") which is stored persistently in your database and, if possible, sent as a push or in-app notification.
3.  **Offender Notification & Reminder Services:**
    
    -   **Immediate Notification:**  
        When the profile is updated, trigger a notification (using the Web Notifications API or a Toast in-app) to alert the offender.
    -   **Scheduled Reminders:**  
        Based on the court dates stored in the offender’s profile, schedule local reminders or push notifications to alert the offender of upcoming events.

### Technologies and Packages Involved

-   **Next.js 15 (App Router) & React 19:**  
    Handle routing, UI components, and client-side logic.
-   **TypeScript:**  
    Provides type safety across your application.
-   **Zod:**  
    Used for validating incoming data (e.g., validating the inmate number format).
-   **pdf-parse:**  
    To extract text from uploaded PDFs and parse court case information.
-   **Web Notifications API & Service Workers:**  
    For requesting permission and delivering notifications to the offender’s device.
-   **MongoDB:**  
    To store offender profiles, court case data, and notifications.
-   **Tailwind CSS & Toast Components:**  
    For styling and displaying transient notifications (Toast messages).

___

## 5\. Implementation Summary

-   **Backend Endpoints:**  
    Build API endpoints that:
    
    -   **Validate input** using Zod.
    -   **Create/update offender profiles** based on parsed data.
    -   **Store notifications** in MongoDB.
    -   **Handle file uploads and PDF parsing.**
-   **Frontend Components:**  
    Create React components that:
    
    -   **Request notification permissions** and display test notifications.
    -   **Allow admin users to upload PDFs** and paste text.
    -   **Show in-app notifications** (e.g., Toast messages) and scheduled reminders.
-   **Session and State Management:**  
    Use HTTP-only cookies with a signed token (or a simple session mechanism) to keep track of the offender’s login state.
    

___

## Final Thoughts

This Offender Services system leverages both browser capabilities (via the Notifications API and Service Workers) and your backend services (via RESTful API endpoints in Next.js) to create a robust reminder and alert system. The goal is to ensure offenders never miss an important court date by combining real-time notifications, in-app reminders, and persistent data in your database.

Feel free to ask more questions or dive into any part of this system in greater detail!