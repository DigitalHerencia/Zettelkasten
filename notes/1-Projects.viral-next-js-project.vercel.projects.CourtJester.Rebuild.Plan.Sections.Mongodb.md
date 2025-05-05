---
id: lh6lpl9p1hhoyqmiv8qbnzb
title: Mongodb
desc: ''
updated: 1742227202806
created: 1742227202806
---
## 1\. MongoDB Schemas and Collections

Your system uses MongoDB to store all persistent data for the offender profiles, notifications, motions, and even templates. Typically, each “collection” in MongoDB is like a table in SQL, and each document is a JSON‑like object that follows a defined schema.

### A. Example Collections

-   **Offenders Collection:**  
    Stores all offender profiles. Each document might include fields such as:
    
    -   `_id` (automatically generated ObjectId)
    -   `inmateNumber`
    -   `name`
    -   `dateOfBirth`
    -   `profileEnabled` (a boolean indicating whether the profile is complete)
    -   Additional fields from parsed court cases and DOC forms (like height, eye color, etc.)
-   **Notifications Collection:**  
    Stores notifications for both admin actions and offender alerts.
    
    -   Fields include: `_id`, `offenderId`, `title`, `message`, `type`, `status` (e.g., "unread"), and `createdAt`.
-   **Motions Collection:**  
    Stores individual motion records created by the admin.
    
    -   Fields include: `_id`, `offenderId`, `caseId`, `templateId`, `title`, `content`, `variables` (the data used to auto‑populate the template), `status`, `createdAt`, and `updatedAt`.
-   **Templates Collection (Optional):**  
    You might store pre‑defined motion templates here with placeholders (e.g., `{{name}}`, `{{court}}`).
    

### B. Defining Schemas with Mongoose (or the native driver)

Even though MongoDB is schema‑less by design, it’s common to enforce some structure using Mongoose or by manual validation (for example, with Zod on the server side). For instance, using Mongoose your offender schema might look like this:


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// models/Offender.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">Schema</span></span><span>, model, </span><span><span class="hljs-title class_">Document</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"mongoose"</span></span><span>;

</span><span><span class="hljs-keyword">interface</span></span><span> </span><span><span class="hljs-title class_">OffenderDocument</span></span><span> </span><span><span class="hljs-keyword">extends</span></span><span> </span><span><span class="hljs-title class_">Document</span></span><span> {
  </span><span><span class="hljs-attr">inmateNumber</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  name?: </span><span><span class="hljs-built_in">string</span></span><span>;
  dateOfBirth?: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">profileEnabled</span></span><span>: </span><span><span class="hljs-built_in">boolean</span></span><span>;
  </span><span><span class="hljs-comment">// other fields like height, eye color, etc.</span></span><span>
}

</span><span><span class="hljs-keyword">const</span></span><span> </span><span><span class="hljs-title class_">OffenderSchema</span></span><span> = </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Schema</span></span><span>&lt;</span><span><span class="hljs-title class_">OffenderDocument</span></span><span>&gt;({
  </span><span><span class="hljs-attr">inmateNumber</span></span><span>: { </span><span><span class="hljs-attr">type</span></span><span>: </span><span><span class="hljs-title class_">String</span></span><span>, </span><span><span class="hljs-attr">required</span></span><span>: </span><span><span class="hljs-literal">true</span></span><span>, </span><span><span class="hljs-attr">unique</span></span><span>: </span><span><span class="hljs-literal">true</span></span><span> },
  </span><span><span class="hljs-attr">name</span></span><span>: { </span><span><span class="hljs-attr">type</span></span><span>: </span><span><span class="hljs-title class_">String</span></span><span> },
  </span><span><span class="hljs-attr">dateOfBirth</span></span><span>: { </span><span><span class="hljs-attr">type</span></span><span>: </span><span><span class="hljs-title class_">String</span></span><span> },
  </span><span><span class="hljs-attr">profileEnabled</span></span><span>: { </span><span><span class="hljs-attr">type</span></span><span>: </span><span><span class="hljs-title class_">Boolean</span></span><span>, </span><span><span class="hljs-attr">default</span></span><span>: </span><span><span class="hljs-literal">false</span></span><span> },
  </span><span><span class="hljs-comment">// additional fields...</span></span><span>
}, { </span><span><span class="hljs-attr">timestamps</span></span><span>: </span><span><span class="hljs-literal">true</span></span><span> });

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">default</span></span><span> model&lt;</span><span><span class="hljs-title class_">OffenderDocument</span></span><span>&gt;(</span><span><span class="hljs-string">"Offender"</span></span><span>, </span><span><span class="hljs-title class_">OffenderSchema</span></span><span>);
</span></span></code></div></div>


You would have similar schemas for notifications and motions. This helps ensure that your documents follow a consistent structure when your API functions (like `createOffender` or `updateOffender`) interact with the database.

___

## 2\. How the API Interacts with MongoDB

In your API endpoints, you call functions such as `getOffenderByInmateNumber`, `createOffender`, and `updateOffender`. These functions encapsulate the logic for querying or updating MongoDB documents.

### A. Offender Login Example

When an offender logs in:

-   **Step 1:** The API receives the inmate number and uses Zod to validate it.
-   **Step 2:** It calls a function like `getOffenderByInmateNumber(inmateNumber)`. This function queries the offenders collection for a document with that inmate number.
-   **Step 3:** If no document is found, it calls `createOffender({ inmateNumber, profileEnabled: false })` to insert a new document into MongoDB.
-   **Step 4:** If a new offender is created, the API then calls a function like `storeNotification(notification)` to insert a new notification document into the notifications collection.

A simplified pseudo‑code might look like this:


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// Example: app/api/inmate/login/route.ts</span></span><span>
</span><span><span class="hljs-keyword">const</span></span><span> offender = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">getOffenderByInmateNumber</span></span><span>(inmateNumber);
</span><span><span class="hljs-keyword">if</span></span><span> (!offender) {
  </span><span><span class="hljs-comment">// Create a new offender profile in MongoDB</span></span><span>
  </span><span><span class="hljs-keyword">const</span></span><span> newOffender = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">createOffender</span></span><span>({ inmateNumber, </span><span><span class="hljs-attr">profileEnabled</span></span><span>: </span><span><span class="hljs-literal">false</span></span><span> });
  </span><span><span class="hljs-comment">// Create a notification for the admin</span></span><span>
  </span><span><span class="hljs-keyword">const</span></span><span> notification = {
    </span><span><span class="hljs-attr">offenderId</span></span><span>: newOffender.</span><span><span class="hljs-property">_id</span></span><span>,
    </span><span><span class="hljs-attr">title</span></span><span>: </span><span><span class="hljs-string">"New Offender Registration"</span></span><span>,
    </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">`New registration for inmate number <span class="hljs-subst">${inmateNumber}</span></span></span><span>.`,
    </span><span><span class="hljs-attr">type</span></span><span>: </span><span><span class="hljs-string">"system"</span></span><span>,
    </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-string">"unread"</span></span><span>,
    </span><span><span class="hljs-attr">createdAt</span></span><span>: </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Date</span></span><span>().</span><span><span class="hljs-title function_">toISOString</span></span><span>(),
  };
  </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">storeNotification</span></span><span>(notification);
  </span><span><span class="hljs-comment">// Return an appropriate response</span></span><span>
}
</span></span></code></div></div>


### B. Data Storage vs. Session Storage

-   **Persistent Data in MongoDB:**  
    All offender profiles, notifications, motions, and templates are stored persistently in MongoDB. This data remains across sessions and server restarts.
    
-   **Session Data (Cookies or Tokens):**  
    On the client side, you store session tokens (e.g., JWTs) in HTTP‑only cookies. These tokens encode a minimal set of information (like the inmate number or an admin flag) and are used to verify that a user is logged in. They do not store the full profile data; instead, they just provide a reference to the user’s identity.
    
    For example, once an offender logs in, you might issue a JWT token that is stored in an HTTP‑only cookie. Subsequent API calls will extract the inmate number from the token and then query MongoDB for the full profile.
    

___

## 3\. Integrating MongoDB with API Endpoints

### A. Database Connection

In a typical Next.js project using Mongoose, you would create a connection handler that ensures your API endpoints have access to your MongoDB connection. This might look like:


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// lib/db/connect.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> mongoose </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"mongoose"</span></span><span>;

</span><span><span class="hljs-keyword">const</span></span><span> </span><span><span class="hljs-variable constant_">MONGO_URI</span></span><span> = process.</span><span><span class="hljs-property">env</span></span><span>.</span><span><span class="hljs-property">MONGO_URI</span></span><span> </span><span><span class="hljs-keyword">as</span></span><span> </span><span><span class="hljs-built_in">string</span></span><span>;

</span><span><span class="hljs-keyword">if</span></span><span> (!</span><span><span class="hljs-variable constant_">MONGO_URI</span></span><span>) {
  </span><span><span class="hljs-keyword">throw</span></span><span> </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Error</span></span><span>(</span><span><span class="hljs-string">"Please define the MONGO_URI environment variable."</span></span><span>);
}

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">connectToDatabase</span></span><span>(</span><span><span class="hljs-params"></span></span><span>) {
  </span><span><span class="hljs-keyword">if</span></span><span> (mongoose.</span><span><span class="hljs-property">connection</span></span><span>.</span><span><span class="hljs-property">readyState</span></span><span> &gt;= </span><span><span class="hljs-number">1</span></span><span>) {
    </span><span><span class="hljs-keyword">return</span></span><span>;
  }
  </span><span><span class="hljs-keyword">return</span></span><span> mongoose.</span><span><span class="hljs-title function_">connect</span></span><span>(</span><span><span class="hljs-variable constant_">MONGO_URI</span></span><span>);
}
</span></span></code></div></div>


Then in your API endpoints, you call `await connectToDatabase();` before performing any database operations.

### B. CRUD Functions

Your data access functions encapsulate database logic. For example:


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// lib/db/offenders.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> </span><span><span class="hljs-title class_">Offender</span></span><span> </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/models/Offender"</span></span><span>;

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">getOffenderByInmateNumber</span></span><span>(</span><span><span class="hljs-params">inmateNumber: <span class="hljs-built_in">string</span></span></span><span>) {
  </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">Offender</span></span><span>.</span><span><span class="hljs-title function_">findOne</span></span><span>({ inmateNumber });
}

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">createOffender</span></span><span>(</span><span><span class="hljs-params">data: { inmateNumber: <span class="hljs-built_in">string</span></span></span><span>; profileEnabled: </span><span><span class="hljs-built_in">boolean</span></span><span> }) {
  </span><span><span class="hljs-keyword">const</span></span><span> offender = </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Offender</span></span><span>(data);
  </span><span><span class="hljs-keyword">return</span></span><span> offender.</span><span><span class="hljs-title function_">save</span></span><span>();
}

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">updateOffender</span></span><span>(</span><span><span class="hljs-params">id: <span class="hljs-built_in">string</span></span></span><span>, updates: </span><span><span class="hljs-built_in">any</span></span><span>) {
  </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">Offender</span></span><span>.</span><span><span class="hljs-title function_">findByIdAndUpdate</span></span><span>(id, updates, { </span><span><span class="hljs-attr">new</span></span><span>: </span><span><span class="hljs-literal">true</span></span><span> });
}
</span></span></code></div></div>


Similar functions exist for notifications and motions.

___

## 4\. Summary of Integration

-   **MongoDB as Persistent Storage:**  
    All essential data (offender profiles, notifications, motions, templates) is stored in MongoDB. Your collections use defined schemas (via Mongoose or manual validation) to ensure consistent structure.
    
-   **Data Access via API Endpoints:**  
    Each endpoint (in `/api/`) uses functions to query, update, and delete documents in MongoDB. For instance, when an offender logs in, the API checks MongoDB for an existing profile, creates one if needed, and then logs a notification.
    
-   **Session vs. Persistent Data:**
    
    -   **Session Data:** Managed via HTTP‑only cookies with signed tokens (like JWTs). This data is transient and used for authentication.
    -   **Persistent Data:** Stored in MongoDB and includes all user profiles, motions, notifications, and related documents.
-   **Best Practices:**
    
    -   Use proper error handling and status codes.
    -   Validate incoming data (using Zod).
    -   Ensure that your database connection is established before performing operations.
    -   Encapsulate your CRUD operations in helper functions for maintainability and reuse.

___

## Final Thoughts

By using MongoDB with defined schemas, you ensure that all your offender data, notifications, and motions are stored reliably and can be queried or updated as needed. Your API endpoints in Next.js interact with MongoDB to retrieve and modify these JSON documents, while session information (managed in cookies) keeps track of user authentication. This clear separation between persistent data and session data is key to a robust system.

Feel free to ask any further questions or request deeper insights into any part of the integration!