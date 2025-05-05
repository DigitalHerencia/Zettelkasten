---
id: itzo3t0utiwje01qp66ix9d
title: ShadCN
desc: ''
updated: 1742227286820
created: 1742227286820
---
## 1\. Overall UI Architecture and Organization

Your app leverages ShadCN UI together with Tailwind CSS to create a consistent, responsive, and easily customizable UI. In our project, most of the reusable components reside in a dedicated folder (commonly under `/components/ui/`). This separation keeps your design system organized and allows you to reuse components throughout both the admin dashboard and offender profile pages.

### Folder Structure Example


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">bash</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre"><span><span>/components
  /ui
    card.tsx
    button.tsx
    input.tsx
    badge.tsx
    tabs.tsx
    confirmation-dialog.tsx
    toaster.tsx
    // etc.
  /motion-history.tsx
  /document-processing-tab.tsx
  /reminder-list.tsx
  /help-button.tsx
</span></span></code></div></div>


Each component is typically built as a React component styled using Tailwind CSS classes. ShadCN UI gives you pre-styled, composable primitives that you can extend or wrap for your specific use case.

___

## 2\. Key UI Components and Their Roles

Let’s walk through the most important components in your codebase and how they are used:

### A. **Card Components**

-   **Card, CardHeader, CardTitle, CardContent:**  
    _Usage:_
    
    -   These are used in various places to group related content. For example, in your admin dashboard, you use cards to display notifications, offender search results, offender lists, motion templates, system settings, etc.
    -   They help encapsulate a section with a header (title) and content body.
    
    _Example from Code:_  
    In `app/admin/dashboard/page.tsx`, you wrap notifications and offender list items inside Card components:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span>&lt;</span><span><span class="hljs-title class_">Card</span></span><span> className=</span><span><span class="hljs-string">"bg-background border border-foreground"</span></span><span>&gt;
      </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">CardHeader</span></span></span></span><span>&gt;
        </span><span><span class="hljs-tag">&lt;<span class="hljs-name">CardTitle</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"font-jacquard"</span></span><span>&gt;Recent Notifications</span><span><span class="hljs-tag">&lt;/<span class="hljs-name">CardTitle</span></span></span><span>&gt;
      </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">CardHeader</span></span></span><span>&gt;
      </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">CardContent</span></span></span></span><span>&gt;
        {/* Notification items go here */}
      </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">CardContent</span></span></span><span>&gt;
    &lt;/</span><span><span class="hljs-title class_">Card</span></span><span>&gt;
    </span></span></code></div></div>
    
    
    _Tips for Populating Data:_
    
    -   Map over data arrays (like notifications or offender list items) and render each item inside its own Card.
    -   Use Tailwind’s spacing and color classes (already defined via your theme) to keep consistent styling.

### B. **Button Component**

-   **Button:**  
    _Usage:_
    
    -   Buttons are used throughout the UI for actions like navigation (e.g., “Back to Dashboard”), submitting forms (e.g., searching offenders, sending notifications), or initiating delete operations.
    -   They come in different variants (e.g., outline, primary) to differentiate actions visually.
    
    _Example from Code:_  
    In your offender details page, you see buttons used to navigate to edit a case or delete a case:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span>&lt;</span><span><span class="hljs-title class_">Button</span></span><span>
      variant=</span><span><span class="hljs-string">"outline"</span></span><span>
      className=</span><span><span class="hljs-string">"bg-background border border-foreground font-kings"</span></span><span>
      onClick={</span><span><span class="hljs-function">() =&gt;</span></span><span> router.</span><span><span class="hljs-title function_">push</span></span><span>(</span><span><span class="hljs-string">`/admin/cases/<span class="hljs-subst">${caseItem._id}</span></span></span><span>`)}
    &gt;
      </span><span><span class="hljs-title class_">Edit</span></span><span> </span><span><span class="hljs-title class_">Case</span></span><span>
    &lt;/</span><span><span class="hljs-title class_">Button</span></span><span>&gt;
    </span></span></code></div></div>
    
    
    _Tips:_
    
    -   Consistently use variant props (like "outline") to signal destructive actions (such as delete) with a different color (e.g., text-red-600).

### C. **Input Component**

-   **Input:**  
    _Usage:_
    
    -   Used in forms such as search bars on the dashboard and text fields in the notification or motion editors.
    -   Ensures uniform styling for all form inputs.
    
    _Example from Code:_  
    Your search form in `app/admin/dashboard/page.tsx`:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span>&lt;</span><span><span class="hljs-title class_">Input</span></span><span>
      </span><span><span class="hljs-keyword">type</span></span><span>=</span><span><span class="hljs-string">"text"</span></span><span>
      placeholder=</span><span><span class="hljs-string">"Search by number or name"</span></span><span>
      value={searchQuery}
      onChange={</span><span><span class="hljs-function">(<span class="hljs-params">e</span></span></span><span>) =&gt; </span><span><span class="hljs-title function_">setSearchQuery</span></span><span>(e.</span><span><span class="hljs-property">target</span></span><span>.</span><span><span class="hljs-property">value</span></span><span>)}
      className=</span><span><span class="hljs-string">"bg-background border border-foreground font-kings"</span></span><span>
    /&gt;
    </span></span></code></div></div>
    
    
    _Tips:_
    
    -   Combine with form management libraries like React Hook Form if your forms get more complex.

### D. **Tabs Components**

-   **Tabs, TabsList, TabsTrigger, TabsContent:**  
    _Usage:_
    
    -   Tabs are used in both the admin dashboard and offender profile pages to switch between different sections (e.g., notifications, offenders, motions, settings, documents for admin; and profile, cases, motions, reminders, notifications for offenders).
    
    _Example from Code:_  
    In your admin dashboard:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span>&lt;</span><span><span class="hljs-title class_">Tabs</span></span><span> defaultValue=</span><span><span class="hljs-string">"notifications"</span></span><span> className=</span><span><span class="hljs-string">"w-full"</span></span><span>&gt;
      </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">TabsList</span></span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"w-full mb-6 bg-background border border-foreground"</span></span><span>&gt;
        </span><span><span class="hljs-tag">&lt;<span class="hljs-name">TabsTrigger</span></span></span><span> </span><span><span class="hljs-attr">value</span></span><span>=</span><span><span class="hljs-string">"notifications"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"flex-1 font-kings"</span></span><span>&gt;
          Notifications
        </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsTrigger</span></span></span><span>&gt;
        {/* Other TabsTrigger items */}
      </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsList</span></span></span><span>&gt;
      </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">TabsContent</span></span></span></span><span> </span><span><span class="hljs-attr">value</span></span><span>=</span><span><span class="hljs-string">"notifications"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"scrollable-area"</span></span><span>&gt;
        {/* Notification Card goes here */}
      </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsContent</span></span></span><span>&gt;
      {</span><span><span class="hljs-comment">/* Other TabsContent sections */</span></span><span>}
    &lt;/</span><span><span class="hljs-title class_">Tabs</span></span><span>&gt;
    </span></span></code></div></div>
    
    
    _Tips:_
    
    -   Ensure each tab’s content is scrollable if it contains long lists, using the `.scrollable-area` class.
    -   Use the defaultValue prop to determine which tab is visible on load.

### E. **Badge Component**

-   **Badge:**  
    _Usage:_
    
    -   To show counts or status indicators (e.g., the number of new notifications).
    
    _Example from Code:_  
    Displaying the new submission count on the Notifications tab:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span>{</span><span><span class="hljs-title function_">getNewSubmissionsCount</span></span><span>() &gt; </span><span><span class="hljs-number">0</span></span><span> &amp;&amp; (
      </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">Badge</span></span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"ml-2 bg-foreground text-background"</span></span><span>&gt;
        {getNewSubmissionsCount()}
      </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">Badge</span></span></span><span>&gt;
    )}
    </span></span></code></div></div>
    
    
    _Tips:_
    
    -   Keep badges simple and use them to draw attention to actionable items.

### F. **ConfirmationDialog Component**

-   **ConfirmationDialog:**  
    _Usage:_
    
    -   Used to confirm destructive actions, such as deleting a case or notification.
    
    _Example from Code:_  
    In your offender details page, before deleting a case:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span>&lt;</span><span><span class="hljs-title class_">ConfirmationDialog</span></span><span>
      title=</span><span><span class="hljs-string">"Delete Case"</span></span><span>
      description=</span><span><span class="hljs-string">"Are you sure you want to delete this case? This action cannot be undone and will also delete all associated motions."</span></span><span>
      open={isDeleteCaseDialogOpen}
      onOpenChange={setIsDeleteCaseDialogOpen}
      onConfirm={confirmDeleteCase}
      confirmText=</span><span><span class="hljs-string">"Delete Case"</span></span><span>
      cancelText=</span><span><span class="hljs-string">"Cancel"</span></span><span>
      isDestructive={</span><span><span class="hljs-literal">true</span></span><span>}
    /&gt;
    </span></span></code></div></div>
    
    
    _Tips:_
    
    -   Use clear, concise language in the dialog to ensure users understand the impact of the action.

### G. **Other Custom Components**

-   **MotionHistory:**  
    _Usage:_
    
    -   Likely used to display the history of changes or updates to a case. It might show a timeline of motions or status updates.
-   **DocumentProcessingTab:**  
    _Usage:_
    
    -   A specialized component that allows admins to upload PDFs and process document data.
    -   This component integrates file upload dialogs, triggers API calls for PDF parsing, and displays results.
-   **ReminderList:**  
    _Usage:_
    
    -   Displays a list of scheduled reminders for an offender. It could include actions for editing or deleting reminders.
-   **HelpButton:**  
    _Usage:_
    
    -   Provides context-sensitive help. When clicked, it might open a modal or link to documentation.
-   **Toaster:**  
    _Usage:_
    
    -   Displays transient messages (toasts) for actions like “Motion sent!” or “Notification deleted!”.
    -   It’s integrated globally in your RootLayout so that any part of the app can trigger a toast.

_Tips for these components:_

-   Keep their APIs consistent (e.g., using props for data and callback functions).
-   Ensure that they’re responsive and styled with Tailwind classes that match your overall theme (background, foreground, font-kings for text, font-jacquard for headings).

___

## 3\. Populating Components with Data

### Data Flow and Interaction

-   **Fetching Data:**  
    Use API endpoints (such as GET endpoints for notifications, offenders, or motions) to fetch data and store it in state using React’s useState or a global state manager like Redux or Context API.
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span><span class="hljs-title function_">useEffect</span></span><span>(</span><span><span class="hljs-function">() =&gt;</span></span><span> {
      </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">fetchNotifications</span></span><span>(</span><span><span class="hljs-params"></span></span><span>) {
        </span><span><span class="hljs-keyword">const</span></span><span> res = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">fetch</span></span><span>(</span><span><span class="hljs-string">"/api/admin/notifications"</span></span><span>);
        </span><span><span class="hljs-keyword">const</span></span><span> data = </span><span><span class="hljs-keyword">await</span></span><span> res.</span><span><span class="hljs-title function_">json</span></span><span>();
        </span><span><span class="hljs-title function_">setNotifications</span></span><span>(data);
      }
      </span><span><span class="hljs-title function_">fetchNotifications</span></span><span>();
    }, []);
    </span></span></code></div></div>
    
    
-   **Mapping Data to Components:**  
    For instance, if you have an array of notifications, map over it to render each within a Card component:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span>{notifications.</span><span><span class="hljs-title function_">map</span></span><span>(</span><span><span class="hljs-function">(<span class="hljs-params">notification</span></span></span><span>) =&gt; (
      </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">Card</span></span></span></span><span> </span><span><span class="hljs-attr">key</span></span><span>=</span><span><span class="hljs-string">{notification._id}</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"p-4 border border-foreground"</span></span><span>&gt;
        </span><span><span class="hljs-tag">&lt;<span class="hljs-name">div</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"flex justify-between items-start"</span></span><span>&gt;
          </span><span><span class="hljs-tag">&lt;<span class="hljs-name">div</span></span></span><span>&gt;
            </span><span><span class="hljs-tag">&lt;<span class="hljs-name">h3</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"font-jacquard"</span></span><span>&gt;{notification.title}</span><span><span class="hljs-tag">&lt;/<span class="hljs-name">h3</span></span></span><span>&gt;
            </span><span><span class="hljs-tag">&lt;<span class="hljs-name">p</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"font-kings"</span></span><span>&gt;{notification.message}</span><span><span class="hljs-tag">&lt;/<span class="hljs-name">p</span></span></span><span>&gt;
          </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">div</span></span></span><span>&gt;
          </span><span><span class="hljs-tag">&lt;<span class="hljs-name">Button</span></span></span><span>
            </span><span><span class="hljs-attr">variant</span></span><span>=</span><span><span class="hljs-string">"outline"</span></span><span>
            </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"bg-background border border-foreground text-red-600 font-kings"</span></span><span>
            </span><span><span class="hljs-attr">onClick</span></span><span>=</span><span><span class="hljs-string">{()</span></span><span> =&gt; handleDeleteNotification(notification._id)}
          &gt;
            Delete
          </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">Button</span></span></span><span>&gt;
        </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">div</span></span></span><span>&gt;
      </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">Card</span></span></span><span>&gt;
    ))}
    </span></span></code></div></div>
    
    
-   **Form Components:**  
    For input forms (e.g., search bars, text areas for notifications), combine the Input component with form handlers (using onChange and onSubmit events) to update state and call the corresponding API endpoint.
    
-   **Using Toasts for Feedback:**  
    After actions like sending a motion or deleting a notification, trigger a toast to give immediate feedback. For example:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span><span class="hljs-title function_">toast</span></span><span>({
      </span><span><span class="hljs-attr">title</span></span><span>: </span><span><span class="hljs-string">"Success"</span></span><span>,
      </span><span><span class="hljs-attr">description</span></span><span>: </span><span><span class="hljs-string">"Motion sent successfully!"</span></span><span>,
    });
    </span></span></code></div></div>
    
    

___

## 4\. Best Practices for Organization

-   **Reusable and Modular:**  
    Write your components to be as reusable as possible. For example, build a generic Card component that accepts a title, content, and optional actions.
-   **Consistent Styling:**  
    Use your Tailwind theme settings (colors, fonts) in each component. The classes like `font-jacquard` and `font-kings` ensure consistency.
-   **Separation of Concerns:**  
    Keep your UI components separate from your business logic. API calls and state management should reside in hooks or container components, while the ShadCN UI components focus on display.
-   **Component Documentation:**  
    Write brief comments or documentation for custom components (like MotionHistory or DocumentProcessingTab) to indicate their purpose and API.

___

## Final Recap

-   **Organization:**  
    All reusable UI components are housed in `/components/ui/` with specialized components (like MotionHistory or ReminderList) in separate files.
-   **Usage:**  
    Components like Card, Button, Input, Tabs, and Badge are used throughout your admin and offender pages for grouping, actions, forms, and status indicators.
-   **Data Integration:**  
    Use API endpoints to fetch and update data. Populate components by mapping over fetched data arrays. Use state management (React hooks or a global state solution) to track this data.
-   **Feedback Mechanisms:**  
    Use Toasts for immediate feedback and ConfirmationDialog for sensitive actions.
-   **Styling:**  
    Leverage Tailwind CSS and your defined fonts (`font-jacquard` for headings, `font-kings` for body text) for a unified look.

This comprehensive breakdown should give you a clear picture of which components you need, how to organize and integrate them, and how they interact with your data and API endpoints. If you have further questions or need additional detail on any specific component, feel free to ask!