---
id: fc8z18m7qpvevrzetkn8jz8
title: Types
desc: ''
updated: 1742227385695
created: 1742227385695
---
## 1\. Organizing Your TypeScript Types and Interfaces

### A. Create a Centralized Types Folder

It’s common practice to maintain a dedicated folder (e.g., `/src/types` or `/types`) for all your shared type definitions. This folder might include files for:

-   **Domain Models:** Offender, Notification, Motion, Template, etc.
-   **API Payloads:** Request and response payloads for each API endpoint.
-   **Component Props:** Types for React component props (if they aren’t defined locally).

**Example Folder Structure:**


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">bash</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre"><span><span>/src
  /components
    /ui
      Button.tsx
      Card.tsx
      ...
  /pages
    ... 
  /lib
    db
    auth.ts
  /types
    offender.ts
    notification.ts
    motion.ts
    template.ts
    api.ts
    common.ts
</span></span></code></div></div>


### B. Splitting Domain Models and API Types

Keep your domain models (data stored in MongoDB) and your API request/response types separated. This allows you to reuse the same types for both database operations and API contracts, but also extend or transform them as needed.

___

## 2\. Defining Domain Models (Interfaces)

Here’s an example of what your core interfaces might look like. These interfaces represent the shape of your data in MongoDB.

### A. Offender Interface


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// src/types/offender.ts</span></span><span>
</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">interface</span></span><span> </span><span><span class="hljs-title class_">Offender</span></span><span> {
  </span><span><span class="hljs-attr">_id</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">inmateNumber</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  name?: </span><span><span class="hljs-built_in">string</span></span><span>;
  dateOfBirth?: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">profileEnabled</span></span><span>: </span><span><span class="hljs-built_in">boolean</span></span><span>;
  </span><span><span class="hljs-comment">// Additional fields from court cases or DOC forms</span></span><span>
  height?: </span><span><span class="hljs-built_in">string</span></span><span>;
  eyeColor?: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-comment">// Timestamps if needed</span></span><span>
  createdAt?: </span><span><span class="hljs-built_in">string</span></span><span>;
  updatedAt?: </span><span><span class="hljs-built_in">string</span></span><span>;
}
</span></span></code></div></div>


### B. Notification Interface


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// src/types/notification.ts</span></span><span>
</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">interface</span></span><span> </span><span><span class="hljs-title class_">Notification</span></span><span> {
  </span><span><span class="hljs-attr">_id</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">offenderId</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">title</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">type</span></span><span>: </span><span><span class="hljs-string">"system"</span></span><span> | </span><span><span class="hljs-string">"motion"</span></span><span> | </span><span><span class="hljs-string">"hearing"</span></span><span> | </span><span><span class="hljs-string">"case"</span></span><span>;
  </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-string">"unread"</span></span><span> | </span><span><span class="hljs-string">"read"</span></span><span>;
  </span><span><span class="hljs-attr">createdAt</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
}
</span></span></code></div></div>


### C. Motion Interface


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// src/types/motion.ts</span></span><span>
</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">interface</span></span><span> </span><span><span class="hljs-title class_">Motion</span></span><span> {
  </span><span><span class="hljs-attr">_id</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">offenderId</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">caseId</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">templateId</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">title</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">content</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">variables</span></span><span>: </span><span><span class="hljs-title class_">Record</span></span><span>&lt;</span><span><span class="hljs-built_in">string</span></span><span>, </span><span><span class="hljs-built_in">any</span></span><span>&gt;;
  </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-string">"draft"</span></span><span> | </span><span><span class="hljs-string">"finalized"</span></span><span>;
  </span><span><span class="hljs-attr">createdAt</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">updatedAt</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
}
</span></span></code></div></div>


### D. Template Interface


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// src/types/template.ts</span></span><span>
</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">interface</span></span><span> </span><span><span class="hljs-title class_">MotionTemplate</span></span><span> {
  </span><span><span class="hljs-attr">_id</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">name</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">content</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>; </span><span><span class="hljs-comment">// content with placeholders (e.g., {{name}}, {{court}})</span></span><span>
  </span><span><span class="hljs-comment">// Optionally, you can store metadata about the template (jurisdiction, etc.)</span></span><span>
}
</span></span></code></div></div>


___

## 3\. Defining API Payload Types

For each API endpoint, define request and response types. This ensures that both your server and client agree on the contract.

### A. Example: Inmate Login API


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// src/types/api.ts</span></span><span>

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">interface</span></span><span> </span><span><span class="hljs-title class_">InmateLoginRequest</span></span><span> {
  </span><span><span class="hljs-attr">inmateNumber</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
}

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">interface</span></span><span> </span><span><span class="hljs-title class_">InmateLoginResponse</span></span><span> {
  success?: </span><span><span class="hljs-built_in">boolean</span></span><span>;
  offender?: </span><span><span class="hljs-title class_">Offender</span></span><span>; </span><span><span class="hljs-comment">// imported from offender.ts</span></span><span>
  </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
}
</span></span></code></div></div>


### B. Example: Create Motion API


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">interface</span></span><span> </span><span><span class="hljs-title class_">CreateMotionRequest</span></span><span> {
  </span><span><span class="hljs-attr">offenderId</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">caseId</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">templateId</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  title?: </span><span><span class="hljs-built_in">string</span></span><span>;
  content?: </span><span><span class="hljs-built_in">string</span></span><span>;
  variables?: </span><span><span class="hljs-title class_">Record</span></span><span>&lt;</span><span><span class="hljs-built_in">string</span></span><span>, </span><span><span class="hljs-built_in">any</span></span><span>&gt;;
}

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">interface</span></span><span> </span><span><span class="hljs-title class_">CreateMotionResponse</span></span><span> {
  </span><span><span class="hljs-attr">success</span></span><span>: </span><span><span class="hljs-built_in">boolean</span></span><span>;
  </span><span><span class="hljs-attr">motionId</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
}
</span></span></code></div></div>


_Tip:_ You can group all API-related interfaces in a file like `src/types/api.ts` or break them into separate files by feature if the project grows.

___

## 4\. Component Props Interfaces

For each React component that receives props, define a corresponding interface. This keeps your components strongly typed.

### A. Example: MotionEditor Component


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span><span class="hljs-comment">// src/components/MotionEditor.tsx</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> </span><span><span class="hljs-title class_">React</span></span><span> </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"react"</span></span><span>;

</span><span><span class="hljs-keyword">interface</span></span><span> </span><span><span class="hljs-title class_">MotionEditorProps</span></span><span> {
  </span><span><span class="hljs-attr">initialContent</span></span><span>: </span><span><span class="hljs-built_in">string</span></span><span>;
  </span><span><span class="hljs-attr">onSubmit</span></span><span>: </span><span><span class="hljs-function">(<span class="hljs-params">data: { content: <span class="hljs-built_in">string</span></span></span></span><span> }) =&gt; </span><span><span class="hljs-built_in">void</span></span><span>;
}

</span><span><span class="hljs-keyword">const</span></span><span> </span><span><span class="hljs-title class_">MotionEditor</span></span><span>: </span><span><span class="hljs-title class_">React</span></span><span>.</span><span><span class="hljs-property">FC</span></span><span>&lt;</span><span><span class="hljs-title class_">MotionEditorProps</span></span><span>&gt; = </span><span><span class="hljs-function">(<span class="hljs-params">{ initialContent, onSubmit }</span></span></span><span>) =&gt; {
  </span><span><span class="hljs-comment">// Component logic here (e.g., integrating React Quill)</span></span><span>
  </span><span><span class="hljs-keyword">return</span></span><span> (
    </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">form</span></span></span></span><span> </span><span><span class="hljs-attr">onSubmit</span></span><span>=</span><span><span class="hljs-string">{(e)</span></span><span> =&gt; { e.preventDefault(); onSubmit({ content: initialContent }); }}&gt;
      {/* Editor UI */}
      </span><span><span class="hljs-tag">&lt;<span class="hljs-name">button</span></span></span><span> </span><span><span class="hljs-attr">type</span></span><span>=</span><span><span class="hljs-string">"submit"</span></span><span>&gt;Send Motion</span><span><span class="hljs-tag">&lt;/<span class="hljs-name">button</span></span></span><span>&gt;
    </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">form</span></span></span><span>&gt;
  );
};

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">default</span></span><span> </span><span><span class="hljs-title class_">MotionEditor</span></span><span>;
</span></span></code></div></div>


_Tip:_ Use React.FC (or explicitly type your function component) to ensure props are well defined.

___

## 5\. Using Zod for Runtime Validation and Type Inference

To catch errors at runtime (and not just at compile time), use Zod to validate incoming data. Zod also allows you to infer TypeScript types from schemas, keeping your types DRY.

### A. Example: Validating Inmate Number


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// src/lib/validation.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> { z } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"zod"</span></span><span>;

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">const</span></span><span> inmateNumberSchema = z.</span><span><span class="hljs-title function_">string</span></span><span>().</span><span><span class="hljs-title function_">min</span></span><span>(</span><span><span class="hljs-number">5</span></span><span>, </span><span><span class="hljs-string">"Invalid inmate number"</span></span><span>);

</span><span><span class="hljs-comment">// Infer the type</span></span><span>
</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">type</span></span><span> </span><span><span class="hljs-title class_">InmateNumber</span></span><span> = z.</span><span><span class="hljs-property">infer</span></span><span>&lt;</span><span><span class="hljs-keyword">typeof</span></span><span> inmateNumberSchema&gt;;
</span></span></code></div></div>


Now you can validate and use the inferred type in your API endpoint:


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// In your API endpoint:</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> { inmateNumberSchema } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/validation"</span></span><span>;

</span><span><span class="hljs-keyword">const</span></span><span> payload = </span><span><span class="hljs-keyword">await</span></span><span> request.</span><span><span class="hljs-title function_">json</span></span><span>();
</span><span><span class="hljs-keyword">const</span></span><span> validated = inmateNumberSchema.</span><span><span class="hljs-title function_">parse</span></span><span>(payload.</span><span><span class="hljs-property">inmateNumber</span></span><span>);
</span></span></code></div></div>


_Tip:_ Use try/catch around Zod’s `parse` to handle validation errors gracefully.

___

## 6\. Integrating With Your Database Functions

When writing your database functions (e.g., in `src/lib/db/offenders.ts`), use the interfaces to ensure that the documents you read and write conform to your expected shape.


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// src/lib/db/offenders.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> </span><span><span class="hljs-title class_">Offender</span></span><span>, { </span><span><span class="hljs-title class_">Offender</span></span><span> </span><span><span class="hljs-keyword">as</span></span><span> </span><span><span class="hljs-title class_">OffenderType</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/models/Offender"</span></span><span>; </span><span><span class="hljs-comment">// Mongoose model with TypeScript generics</span></span><span>

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">getOffenderByInmateNumber</span></span><span>(</span><span><span class="hljs-params">inmateNumber: <span class="hljs-built_in">string</span></span></span><span>): </span><span><span class="hljs-title class_">Promise</span></span><span>&lt;</span><span><span class="hljs-title class_">OffenderType</span></span><span> | </span><span><span class="hljs-literal">null</span></span><span>&gt; {
  </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">Offender</span></span><span>.</span><span><span class="hljs-title function_">findOne</span></span><span>({ inmateNumber });
}

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">createOffender</span></span><span>(</span><span><span class="hljs-params">data: Pick&lt;OffenderType, <span class="hljs-string">"inmateNumber"</span></span></span><span> | </span><span><span class="hljs-string">"profileEnabled"</span></span><span>&gt;): </span><span><span class="hljs-title class_">Promise</span></span><span>&lt;</span><span><span class="hljs-title class_">OffenderType</span></span><span>&gt; {
  </span><span><span class="hljs-keyword">const</span></span><span> offender = </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Offender</span></span><span>(data);
  </span><span><span class="hljs-keyword">return</span></span><span> offender.</span><span><span class="hljs-title function_">save</span></span><span>();
}
</span></span></code></div></div>


_Tip:_ Use `Pick` or `Partial` to create types for update operations.

___

## 7\. Final Considerations and Best Practices

-   **Centralize Your Types:**  
    Keep all interfaces and types in one or several well-organized files. This makes it easy to import and use them consistently across your project.
    
-   **Leverage Type Inference:**  
    Use libraries like Zod to infer types. This avoids duplication between runtime validation and static types.
    
-   **Keep Component Props Clear:**  
    Always define props interfaces for your components. This prevents common errors like “missing property” or “wrong type.”
    
-   **Integrate with Mongoose (if used):**  
    When using Mongoose, define your schema with TypeScript interfaces so that your models are typed.
    
-   **API Contracts:**  
    Define request and response types for every API endpoint. This ensures your client and server communicate reliably.
    
-   **Tooling:**  
    Enable strict mode in your `tsconfig.json` to catch type errors early. Consider using ESLint and Prettier to maintain code quality and consistency.
    

___

## 8\. Example tsconfig.json Settings

Make sure your `tsconfig.json` is set up for strict type checking:


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">json</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-json"><span><span><span class="hljs-punctuation">{</span></span><span>
  </span><span><span class="hljs-attr">"compilerOptions"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-punctuation">{</span></span><span>
    </span><span><span class="hljs-attr">"target"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-string">"esnext"</span></span><span><span class="hljs-punctuation">,</span></span><span>
    </span><span><span class="hljs-attr">"lib"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-punctuation">[</span></span><span><span class="hljs-string">"dom"</span></span><span><span class="hljs-punctuation">,</span></span><span> </span><span><span class="hljs-string">"dom.iterable"</span></span><span><span class="hljs-punctuation">,</span></span><span> </span><span><span class="hljs-string">"esnext"</span></span><span><span class="hljs-punctuation">]</span></span><span><span class="hljs-punctuation">,</span></span><span>
    </span><span><span class="hljs-attr">"allowJs"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-literal"><span class="hljs-keyword">false</span></span></span><span></span><span><span class="hljs-punctuation">,</span></span><span>
    </span><span><span class="hljs-attr">"skipLibCheck"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-literal"><span class="hljs-keyword">true</span></span></span><span></span><span><span class="hljs-punctuation">,</span></span><span>
    </span><span><span class="hljs-attr">"strict"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-literal"><span class="hljs-keyword">true</span></span></span><span></span><span><span class="hljs-punctuation">,</span></span><span>
    </span><span><span class="hljs-attr">"forceConsistentCasingInFileNames"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-literal"><span class="hljs-keyword">true</span></span></span><span></span><span><span class="hljs-punctuation">,</span></span><span>
    </span><span><span class="hljs-attr">"noEmit"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-literal"><span class="hljs-keyword">true</span></span></span><span></span><span><span class="hljs-punctuation">,</span></span><span>
    </span><span><span class="hljs-attr">"module"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-string">"esnext"</span></span><span><span class="hljs-punctuation">,</span></span><span>
    </span><span><span class="hljs-attr">"moduleResolution"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-string">"node"</span></span><span><span class="hljs-punctuation">,</span></span><span>
    </span><span><span class="hljs-attr">"resolveJsonModule"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-literal"><span class="hljs-keyword">true</span></span></span><span></span><span><span class="hljs-punctuation">,</span></span><span>
    </span><span><span class="hljs-attr">"isolatedModules"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-literal"><span class="hljs-keyword">true</span></span></span><span></span><span><span class="hljs-punctuation">,</span></span><span>
    </span><span><span class="hljs-attr">"jsx"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-string">"preserve"</span></span><span><span class="hljs-punctuation">,</span></span><span>
    </span><span><span class="hljs-attr">"esModuleInterop"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-literal"><span class="hljs-keyword">true</span></span></span><span></span><span><span class="hljs-punctuation">,</span></span><span>
    </span><span><span class="hljs-attr">"incremental"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-literal"><span class="hljs-keyword">true</span></span></span><span>
  </span><span><span class="hljs-punctuation">}</span></span><span><span class="hljs-punctuation">,</span></span><span>
  </span><span><span class="hljs-attr">"include"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-punctuation">[</span></span><span><span class="hljs-string">"next-env.d.ts"</span></span><span><span class="hljs-punctuation">,</span></span><span> </span><span><span class="hljs-string">"**/*.ts"</span></span><span><span class="hljs-punctuation">,</span></span><span> </span><span><span class="hljs-string">"**/*.tsx"</span></span><span><span class="hljs-punctuation">]</span></span><span><span class="hljs-punctuation">,</span></span><span>
  </span><span><span class="hljs-attr">"exclude"</span></span><span><span class="hljs-punctuation">:</span></span><span> </span><span><span class="hljs-punctuation">[</span></span><span><span class="hljs-string">"node_modules"</span></span><span><span class="hljs-punctuation">]</span></span><span>
</span><span><span class="hljs-punctuation">}</span></span><span>
</span></span></code></div></div>


___

## Final Recap

1.  **Centralize Types:**  
    Create a dedicated folder for all your interfaces and types, splitting domain models, API payloads, and component props.
    
2.  **Define Clear Interfaces:**  
    Write interfaces for Offender, Notification, Motion, Template, and API payloads to ensure consistency across your codebase.
    
3.  **Use Zod for Validation:**  
    Leverage Zod for runtime validation and type inference, keeping your type definitions DRY and reliable.
    
4.  **Integrate in Components and API Endpoints:**  
    Use these types in your React components, API endpoints, and database functions to catch errors at compile time and ensure data consistency.
    
5.  **Configure Strict TypeScript Settings:**  
    Enable strict mode and use ESLint/Prettier to enforce best practices.
    

Following these guidelines will help you build a foolproof, type-safe system where TypeScript errors are minimized, and you can confidently develop your Court Jester app without running into unexpected type issues.

If you have any more questions or need further examples, feel free to ask!