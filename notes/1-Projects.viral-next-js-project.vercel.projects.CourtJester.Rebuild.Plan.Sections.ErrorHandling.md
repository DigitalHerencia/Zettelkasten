---
id: 4ak8c42h7va5nncjqh563ja
title: ErrorHandling
desc: ''
updated: 1742227572607
created: 1742227572607
---
## 1\. API Error Handling

### A. Try/Catch Blocks and Status Codes

In your API endpoints (for example, the offender login or cases deletion endpoints), you already wrap your logic in try/catch blocks. This ensures that if anything goes wrong (for example, a database error or an invalid parameter), you log the error and return a well‑formed response with an appropriate HTTP status code (like 400, 404, or 500).

**Example: Inmate Login Endpoint**


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">POST</span></span><span>(</span><span><span class="hljs-params">request: NextRequest</span></span><span>) {
  </span><span><span class="hljs-keyword">try</span></span><span> {
    </span><span><span class="hljs-keyword">const</span></span><span> { inmateNumber } = </span><span><span class="hljs-keyword">await</span></span><span> request.</span><span><span class="hljs-title function_">json</span></span><span>();
    </span><span><span class="hljs-keyword">if</span></span><span> (!inmateNumber) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Inmate number is required"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">400</span></span><span> });
    }
    </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isValidInmate</span></span><span>(inmateNumber))) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Invalid inmate number"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">400</span></span><span> });
    }
    </span><span><span class="hljs-comment">// ... logic for finding or creating the offender ...</span></span><span>
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Registration received. You will be notified soon when your profile is ready."</span></span><span> });
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error in inmate login:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to process login"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}
</span></span></code></div></div>


_Key Takeaway:_  
Always log the error and return a JSON response with a clear message and a status code so that the client knows what went wrong.

### B. Redirects on Unauthorized or Not Found

For example, in your offender detail page you redirect the user

##### You said:

Okay, let's talk about a error handling system here, and error catching, and error boundaries, and using Next.js' built-in error, and also their loading, you know, pages that are like pre-configured or whatever it is, like the, it's like part of, it's a feature of Next.js. Specifically from my code base, using, you know, particular examples from my code base, describe how the, you know, holistic error management handling system is gonna handle errors gracefully, and how redirects work, and what happens if API call fire, doesn't fire, or something like that. Give me the whole rundown, be as specific as possible. I don't really have a lot of knowledge about this, that's why my vocabulary on it is pretty sparse. So go ahead and give me everything that I need to know about implementing a robust, and functional, and graceful error management handling, whatever you want to call it. And then also, just because, why not throw in, you know, some information about the loading pages, or how to, how that kind of stuff works.

Reasoned for 5 seconds

Below is a comprehensive guide to implementing a robust error handling and loading system in your Court Jester app using Next.js 15 (App Router) with TypeScript. I’ll reference specific examples from your codebase and explain how to:

-   Catch and handle errors in API endpoints
-   Use Next.js error boundaries and built‑in error pages
-   Implement loading pages and fallback UIs
-   Handle redirects when something goes wrong

___

## 1\. API Endpoint Error Handling

Your API endpoints already use try/catch blocks to catch errors and return meaningful HTTP status codes. For example, in your inmate login endpoint you have:


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">POST</span></span><span>(</span><span><span class="hljs-params">request: NextRequest</span></span><span>) {
  </span><span><span class="hljs-keyword">try</span></span><span> {
    </span><span><span class="hljs-keyword">const</span></span><span> { inmateNumber } = </span><span><span class="hljs-keyword">await</span></span><span> request.</span><span><span class="hljs-title function_">json</span></span><span>();
    </span><span><span class="hljs-keyword">if</span></span><span> (!inmateNumber) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Inmate number is required"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">400</span></span><span> });
    }
    </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isValidInmate</span></span><span>(inmateNumber))) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Invalid inmate number"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">400</span></span><span> });
    }
    </span><span><span class="hljs-comment">// ... logic for finding or creating the offender ...</span></span><span>
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Registration received. You will be notified soon when your profile is ready."</span></span><span> });
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error in inmate login:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to process login"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}
</span></span></code></div></div>


### Key Points:

-   **Try/Catch:** Wrap your logic in try/catch to catch unexpected errors.
-   **Status Codes:** Return 400 for bad requests (e.g., missing parameters) and 500 for server errors.
-   **Logging:** Log errors to the console (or to a logging service in production) to aid debugging.
-   **JSON Responses:** Return a JSON error message so the client can show a user-friendly message.

___

## 2\. Handling Redirects on the Server

In several API endpoints (or even in client components), you might need to redirect if a resource isn’t found or if a user isn’t authorized. For instance, in your offender details page you might check for unauthorized access:


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span><span class="hljs-keyword">if</span></span><span> (!offender) {
  </span><span><span class="hljs-keyword">return</span></span><span> (
    </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">div</span></span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"min-h-screen flex items-center justify-center bg-background text-foreground"</span></span><span>&gt;
      </span><span><span class="hljs-tag">&lt;<span class="hljs-name">div</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"text-center"</span></span><span>&gt;
        </span><span><span class="hljs-tag">&lt;<span class="hljs-name">p</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"font-kings text-xl mb-4"</span></span><span>&gt;Offender not found</span><span><span class="hljs-tag">&lt;/<span class="hljs-name">p</span></span></span><span>&gt;
        </span><span><span class="hljs-tag">&lt;<span class="hljs-name">Button</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"bg-foreground text-background font-kings"</span></span><span> </span><span><span class="hljs-attr">onClick</span></span><span>=</span><span><span class="hljs-string">{()</span></span><span> =&gt; router.push("/admin/dashboard")}&gt;
          Back to Dashboard
        </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">Button</span></span></span><span>&gt;
      </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">div</span></span></span><span>&gt;
    </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">div</span></span></span><span>&gt;
  );
}
</span></span></code></div></div>


### How Redirects Work:

-   **Client-Side Redirects:**  
    In your React components, you can use Next.js’ `useRouter` hook to push a new route if an error occurs (e.g., unauthorized access).
-   **Server-Side Redirects:**  
    In API endpoints or server actions, you can return a response with a 302 status and a Location header if needed.

___

## 3\. Error Boundaries and Next.js Built‑In Error Pages

### A. Error Boundaries in Next.js App Router

Next.js 15 (and its predecessors with the App Router) allows you to create an `error.js` (or `error.tsx`) file in any route segment. This file serves as an error boundary for that segment. For example, in your admin dashboard route, you could add:


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span><span class="hljs-comment">// app/admin/dashboard/error.tsx</span></span><span>
</span><span><span class="hljs-string">"use client"</span></span><span>;

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">default</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">AdminDashboardError</span></span><span>(</span><span><span class="hljs-params">{ error, reset }: { error: <span class="hljs-built_in">Error</span></span></span><span>; reset: () =&gt; </span><span><span class="hljs-built_in">void</span></span><span> }) {
  </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error in admin dashboard:"</span></span><span>, error);
  </span><span><span class="hljs-keyword">return</span></span><span> (
    </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">div</span></span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"min-h-screen flex flex-col items-center justify-center bg-background text-foreground p-4"</span></span><span>&gt;
      </span><span><span class="hljs-tag">&lt;<span class="hljs-name">h2</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"font-jacquard text-2xl mb-4"</span></span><span>&gt;Something went wrong</span><span><span class="hljs-tag">&lt;/<span class="hljs-name">h2</span></span></span><span>&gt;
      </span><span><span class="hljs-tag">&lt;<span class="hljs-name">p</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"font-kings mb-4"</span></span><span>&gt;We encountered an error while loading the dashboard. Please try again.</span><span><span class="hljs-tag">&lt;/<span class="hljs-name">p</span></span></span><span>&gt;
      </span><span><span class="hljs-tag">&lt;<span class="hljs-name">button</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"bg-foreground text-background font-kings px-4 py-2"</span></span><span> </span><span><span class="hljs-attr">onClick</span></span><span>=</span><span><span class="hljs-string">{()</span></span><span> =&gt; reset()}&gt;
        Retry
      </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">button</span></span></span><span>&gt;
    </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">div</span></span></span><span>&gt;
  );
}
</span></span></code></div></div>


### B. How It Works:

-   **Error Boundaries:**  
    The error file catches errors thrown during rendering, data fetching, or lifecycle methods within that route segment.
-   **Reset Function:**  
    Next.js passes a `reset` function that you can call to attempt a re-render (which may re-fetch data and clear the error).

### C. Global Error Page:

If an error isn’t caught by a specific route’s error file, Next.js will fallback to a global error boundary if configured.

___

## 4\. Loading States and Fallback UI

Next.js App Router also supports a `loading.js` (or `loading.tsx`) file in any route segment to display a loading state while your data is being fetched.

### Example: Loading Page for Admin Dashboard


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span><span class="hljs-comment">// app/admin/dashboard/loading.tsx</span></span><span>
</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">default</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">AdminDashboardLoading</span></span><span>(</span><span><span class="hljs-params"></span></span><span>) {
  </span><span><span class="hljs-keyword">return</span></span><span> (
    </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">div</span></span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"min-h-screen flex items-center justify-center bg-background text-foreground"</span></span><span>&gt;
      </span><span><span class="hljs-tag">&lt;<span class="hljs-name">p</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"font-kings text-xl"</span></span><span>&gt;Loading admin dashboard...</span><span><span class="hljs-tag">&lt;/<span class="hljs-name">p</span></span></span><span>&gt;
    </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">div</span></span></span><span>&gt;
  );
}
</span></span></code></div></div>


### How It Works:

-   **Automatic Display:**  
    While your route is fetching data or rendering asynchronously, Next.js will render the `loading` component.
-   **Seamless Transition:**  
    Once the data is loaded, the main content replaces the loading component automatically.

___

## 5\. Holistic Error Management Flow in Your App

### A. API Level

1.  **Request Validation:**  
    Validate all incoming parameters (using Zod or similar).
2.  **Try/Catch in API:**  
    Wrap operations in try/catch blocks and log errors.
3.  **Error Responses:**  
    Return JSON responses with appropriate HTTP status codes.

### B. Client Side

1.  **Data Fetching:**  
    Use `useEffect` and fetch calls. For example, in your offender detail page:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span><span class="hljs-title function_">useEffect</span></span><span>(</span><span><span class="hljs-function">() =&gt;</span></span><span> {
      </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">fetchData</span></span><span>(</span><span><span class="hljs-params"></span></span><span>) {
        </span><span><span class="hljs-keyword">try</span></span><span> {
          </span><span><span class="hljs-keyword">const</span></span><span> res = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">fetch</span></span><span>(</span><span><span class="hljs-string">`/api/admin/offenders/<span class="hljs-subst">${params.id}</span></span></span><span>`);
          </span><span><span class="hljs-keyword">if</span></span><span> (!res.</span><span><span class="hljs-property">ok</span></span><span>) {
            </span><span><span class="hljs-comment">// Handle HTTP errors gracefully</span></span><span>
            </span><span><span class="hljs-keyword">throw</span></span><span> </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Error</span></span><span>(</span><span><span class="hljs-string">`Error: <span class="hljs-subst">${res.status}</span></span></span><span>`);
          }
          </span><span><span class="hljs-keyword">const</span></span><span> data = </span><span><span class="hljs-keyword">await</span></span><span> res.</span><span><span class="hljs-title function_">json</span></span><span>();
          </span><span><span class="hljs-title function_">setOffender</span></span><span>(data);
        } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
          </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error fetching offender:"</span></span><span>, error);
          </span><span><span class="hljs-comment">// Optionally, set error state to show an error message or redirect</span></span><span>
          </span><span><span class="hljs-title function_">setError</span></span><span>(error);
        }
      }
      </span><span><span class="hljs-title function_">fetchData</span></span><span>();
    }, [params.</span><span><span class="hljs-property">id</span></span><span>]);
    </span></span></code></div></div>
    
    
2.  **Error Boundaries:**  
    Use the built‑in error files (`error.tsx`) to catch rendering errors.
3.  **Fallback UI:**  
    Display loading indicators via `loading.tsx` files until data is fetched.
4.  **Redirects:**  
    If the data isn’t found (e.g., offender not found), use client-side redirects using `useRouter().push("/")`.

### C. User Feedback with Toasts

-   **Toasts for Immediate Errors:**  
    In your components, when an API call fails, trigger a Toast notification (using your Toaster component) to inform the user.
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span><span class="hljs-title function_">toast</span></span><span>({
      </span><span><span class="hljs-attr">title</span></span><span>: </span><span><span class="hljs-string">"Error"</span></span><span>,
      </span><span><span class="hljs-attr">description</span></span><span>: </span><span><span class="hljs-string">"Failed to load offender data"</span></span><span>,
      </span><span><span class="hljs-attr">variant</span></span><span>: </span><span><span class="hljs-string">"destructive"</span></span><span>,
    });
    </span></span></code></div></div>
    
    

___

## Final Summary

-   **API Endpoints:**  
    Use try/catch and return clear error messages with HTTP status codes.
-   **Error Boundaries:**  
    Create an `error.tsx` file in route segments (e.g., `app/admin/dashboard/error.tsx`) to gracefully catch and display errors.
-   **Loading Pages:**  
    Create `loading.tsx` files (e.g., `app/admin/dashboard/loading.tsx`) to display a loading state while data is being fetched.
-   **Redirects:**  
    Use client-side redirects in components (with `useRouter`) when resources aren’t found or the user isn’t authorized.
-   **User Feedback:**  
    Use Toasts to provide immediate, transient feedback when errors occur.
-   **Holistic Approach:**  
    With robust error handling at both the API and UI layers, your Court Jester app will handle issues gracefully—logging errors, informing users, and allowing retries where appropriate.

This setup ensures that whether an API call fails, a component crashes, or data isn’t available, your app will present clear, actionable feedback and continue operating smoothly. If you have more questions or need further examples on any part of this system, just let me know!