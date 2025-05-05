---
id: foswrmk4afzq9th4rm1pdl4
title: Lesso
desc: ''
updated: 1742226429105
created: 1742226417461
---
# Lesson: Building and Understanding API Endpoints in Next.js 15 with TypeScript

In this lesson, we’ll start with basic API concepts and progressively build toward more complex topics. We’ll use real examples from your Court Jester project to illustrate key points.

> **Interactive Tip:** Feel free to pause, review the code snippets, and try writing your own small examples as you progress.

___

## 1\. Basic API Concepts and Vocabulary

### What Is an API Endpoint?

-   **Endpoint:** A URL or route where an API (Application Programming Interface) listens for requests. In our Next.js project, endpoints are defined inside the `app/api` folder.
-   **HTTP Methods:**
    -   **GET:** Retrieves data.
    -   **POST:** Sends new data.
    -   **PATCH:** Updates existing data.
    -   **DELETE:** Removes data.

### Vocabulary Check

-   **Request:** The data or message sent by a client (like a web browser or another service) to an API.
-   **Response:** The data sent back from the API to the client.
-   **Status Codes:** Numeric codes (like 200, 400, 404, 500) that indicate the result of the request.

___

## 2\. Next.js API Routes in the App Router

In Next.js 15 using the new App Router, API routes are colocated with your project under the `app/api` directory. Each folder (or file) corresponds to an endpoint.

### Anatomy of an API Route

Consider the following simple example from your Court Jester codebase—the inmate login endpoint:

```
<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// app/api/inmate/login/route.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">NextRequest</span></span><span>, </span><span><span class="hljs-title class_">NextResponse</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"next/server"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { isValidInmate } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/auth"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { getOffenderByInmateNumber, createOffender } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/db/offenders"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { storeNotification } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/db/blob-storage"</span></span><span>;

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">POST</span></span><span>(</span><span><span class="hljs-params">request: NextRequest</span></span><span>) {
  </span><span><span class="hljs-keyword">try</span></span><span> {
    </span><span><span class="hljs-keyword">const</span></span><span> { inmateNumber } = </span><span><span class="hljs-keyword">await</span></span><span> request.</span><span><span class="hljs-title function_">json</span></span><span>();
    </span><span><span class="hljs-keyword">if</span></span><span> (!inmateNumber) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Inmate number is required"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">400</span></span><span> });
    }
    </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isValidInmate</span></span><span>(inmateNumber))) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Invalid inmate number"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">400</span></span><span> });
    }
    </span><span><span class="hljs-comment">// ...additional logic to check for or create an offender</span></span><span>
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Registration received. You will be notified soon when your profile is ready."</span></span><span> });
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error in inmate login:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to process login"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}
</span></span></code></div></div>
```

### Key Points in This Example

-   **Imports:**
    -   `NextRequest` and `NextResponse` are Next.js utilities to handle incoming requests and outgoing responses.
-   **Async Function:**
    -   API endpoints are asynchronous, allowing you to perform database operations or external calls.
-   **HTTP Method:**
    -   The function name (here, `POST`) tells Next.js that this code handles POST requests.
-   **Error Handling:**
    -   Try-catch blocks ensure that errors are caught, and the client receives a proper error message and status code.
-   **Response Creation:**
    -   `NextResponse.json(...)` is used to send JSON responses back to the client.

> **Interactive Exercise:**  
> _What do you think happens if the inmate number isn’t provided? How does the endpoint respond?_  
> (Answer: It returns a 400 status with a message "Inmate number is required.")

___

## 3\. Diving Deeper: HTTP Methods and Their Purposes

Let’s explore the different HTTP methods with examples from your code:

### GET Requests

-   **Purpose:** Retrieve data.
    
-   **Example:** In your offender endpoint:
    
    ```
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// app/api/admin/offenders/[id]/route.ts</span></span><span>
    </span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">GET</span></span><span>(</span><span><span class="hljs-params">request: NextRequest, { params }: { params: { id: <span class="hljs-built_in">string</span></span></span><span> } }) {
      </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isAdminRequest</span></span><span>(request))) {
        </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Unauthorized"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
      }
      </span><span><span class="hljs-keyword">try</span></span><span> {
        </span><span><span class="hljs-keyword">const</span></span><span> { id } = params;
        </span><span><span class="hljs-keyword">const</span></span><span> offender = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">getOffenderById</span></span><span>(id);
        </span><span><span class="hljs-keyword">if</span></span><span> (!offender) {
          </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Offender not found"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">404</span></span><span> });
        }
        </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>(offender);
      } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
        </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error fetching offender:"</span></span><span>, error);
        </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to fetch offender"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
      }
    }
    </span></span></code></div></div>
    ```
    
    **Vocabulary Focus:**
    
    -   **Route Parameters:** The `[id]` in the file path allows us to capture a dynamic value (the offender's ID) from the URL.

### POST Requests

-   **Purpose:** Create new data.
    
-   **Example:** The admin login endpoint:
    
    ```
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// app/api/admin/login/route.ts</span></span><span>
    </span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">POST</span></span><span>(</span><span><span class="hljs-params">request: NextRequest</span></span><span>) {
      </span><span><span class="hljs-keyword">try</span></span><span> {
        </span><span><span class="hljs-keyword">const</span></span><span> { adminCode } = </span><span><span class="hljs-keyword">await</span></span><span> request.</span><span><span class="hljs-title function_">json</span></span><span>();
        </span><span><span class="hljs-keyword">if</span></span><span> (adminCode !== </span><span><span class="hljs-string">"admin86"</span></span><span>) {
          </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Invalid admin code"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
        }
        </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">success</span></span><span>: </span><span><span class="hljs-literal">true</span></span><span>, </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Admin authenticated"</span></span><span> });
      } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
        </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error in admin login:"</span></span><span>, error);
        </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to process admin login"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
      }
    }
    </span></span></code></div></div>
    ```
    
    **Vocabulary Focus:**
    
    -   **Payload:** The data sent in the body of the POST request, accessed here via `request.json()`.

### PATCH and DELETE Requests

-   **PATCH:** Updates an existing resource.
    
-   **DELETE:** Removes a resource.
    
-   **Example:** The PATCH and DELETE in your motion endpoint demonstrate how to update or remove data, including checking for authorization.
    
    ```
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// app/api/admin/motions/[id]/route.ts</span></span><span>
    </span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">PATCH</span></span><span>(</span><span><span class="hljs-params">request: NextRequest, { params }: { params: { id: <span class="hljs-built_in">string</span></span></span><span> } }) {
      </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isAdminRequest</span></span><span>(request))) {
        </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Unauthorized"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
      }
      </span><span><span class="hljs-keyword">try</span></span><span> {
        </span><span><span class="hljs-keyword">const</span></span><span> { id } = params;
        </span><span><span class="hljs-keyword">const</span></span><span> updates = </span><span><span class="hljs-keyword">await</span></span><span> request.</span><span><span class="hljs-title function_">json</span></span><span>();
        </span><span><span class="hljs-keyword">const</span></span><span> motion = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">getMotionById</span></span><span>(id);
        </span><span><span class="hljs-keyword">if</span></span><span> (!motion) {
          </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Motion not found"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">404</span></span><span> });
        }
        </span><span><span class="hljs-keyword">const</span></span><span> updatedMotion = {
          ...motion,
          ...updates,
          </span><span><span class="hljs-attr">updatedAt</span></span><span>: </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Date</span></span><span>().</span><span><span class="hljs-title function_">toISOString</span></span><span>(),
        };
        </span><span><span class="hljs-keyword">if</span></span><span> (updates.</span><span><span class="hljs-property">variables</span></span><span> &amp;&amp; motion.</span><span><span class="hljs-property">templateId</span></span><span>) {
          </span><span><span class="hljs-keyword">const</span></span><span> template = </span><span><span class="hljs-title function_">getTemplateById</span></span><span>(motion.</span><span><span class="hljs-property">templateId</span></span><span>);
          </span><span><span class="hljs-keyword">if</span></span><span> (template) {
            </span><span><span class="hljs-keyword">const</span></span><span> newVariables = { ...motion.</span><span><span class="hljs-property">variables</span></span><span>, ...updates.</span><span><span class="hljs-property">variables</span></span><span> };
            updatedMotion.</span><span><span class="hljs-property">content</span></span><span> = </span><span><span class="hljs-title function_">fillTemplate</span></span><span>(template, newVariables);
            updatedMotion.</span><span><span class="hljs-property">variables</span></span><span> = newVariables;
          }
        }
        </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">updateMotion</span></span><span>(id, updatedMotion);
        </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>(updatedMotion);
      } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
        </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error updating motion:"</span></span><span>, error);
        </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to update motion"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
      }
    }
    </span></span></code></div></div>
    ```
    
    **Vocabulary Focus:**
    
    -   **Idempotency:** PATCH operations update data without creating duplicates, and DELETE operations remove data safely.

> **Interactive Challenge:**  
> _Try to think of a scenario where you’d use PATCH instead of PUT._  
> (Hint: When you need to update only specific fields of a resource rather than replacing it entirely.)

___

## 4\. Security Concepts in API Endpoints

Your code uses simple authentication via functions like `isAdminRequest` and `isValidInmate`. Here’s what to note:

-   **Authorization:**  
    For sensitive operations, your endpoints check if the request is authorized. For example:
    
    ```
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isAdminRequest</span></span><span>(request))) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Unauthorized"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
    }
    </span></span></code></div></div>
    ```
    
-   **Error Handling:**  
    Every endpoint uses try-catch blocks and returns meaningful status codes (400, 401, 404, 500) so the client knows what went wrong.
    
-   **Data Validation:**  
    Your endpoints verify required fields (e.g., inmate number, admin code) before processing further.
    

> **Interactive Discussion:**  
> _How might you further secure these endpoints in a production environment?_  
> (Possible answers: using environment variables for secret codes, JWT tokens, proper CORS policies, and rate limiting.)

___

## 5\. TypeScript in API Routes

TypeScript adds static typing to your API routes, making your code more robust.

### Example: Type Annotations in an API Route

Look at the admin login endpoint:

```
<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">POST</span></span><span>(</span><span><span class="hljs-params">request: NextRequest</span></span><span>): </span><span><span class="hljs-title class_">Promise</span></span><span>&lt;</span><span><span class="hljs-title class_">NextResponse</span></span><span>&gt; {
  </span><span><span class="hljs-comment">// ...</span></span><span>
}
</span></span></code></div></div>
```

-   **NextRequest and NextResponse:**  
    These types come from Next.js and ensure that your request and response objects have the correct properties and methods.
    
-   **Type Safety:**  
    When calling `await request.json()`, TypeScript helps you ensure that the expected keys (like `adminCode`) are present and used correctly.
    

> **Interactive Exercise:**  
> _Try adding an interface for your request payload in the inmate login endpoint to ensure that `inmateNumber` is a string._

___

## 6\. Recap and Next Steps

### Key Vocabulary

-   **Endpoint, Request, Response, HTTP Methods, Status Codes, Payload, Route Parameters**

### Concepts Covered

-   **Basic API structure** in Next.js App Router.
-   **Implementing GET, POST, PATCH, DELETE** endpoints.
-   **Using TypeScript for type safety** in your API routes.
-   **Handling security and errors** effectively.

### Interactive Reflection

-   Consider how your Court Jester codebase handles new inmate registrations and admin operations.
-   Think about how you might extend this by adding more features (e.g., JWT authentication, advanced logging, or caching strategies).

___

## Final Thoughts

You now have a comprehensive overview of building, understanding, and maintaining API endpoints in Next.js 15 with TypeScript and React 19. Your Court Jester codebase serves as a real-world example that demonstrates many of these concepts—from dynamic route parameters to error handling and authorization.

Feel free to experiment with the code examples, ask questions, or try implementing new endpoints using the vocabulary and techniques you’ve just learned. Happy coding!