---
id: vpiy8ssl2lluvmoh5m4lzh1
title: DesignSystem
desc: ''
updated: 1742227459931
created: 1742227459931
---
## 1\. Design System Foundations

### A. Colors and Typography

Your Tailwind configuration and global CSS set the foundation for colors and fonts:

-   **Colors:**
    
    -   **Background:** `#e8ddca`
    -   **Foreground:** `#292520`  
        These colors are defined in your Tailwind config’s `extend.colors` and applied in your global CSS using CSS variables:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">css</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-css"><span><span><span class="hljs-selector-pseudo">:root</span></span><span> {
      </span><span><span class="hljs-attr">--background</span></span><span>: </span><span><span class="hljs-number">#e8ddca</span></span><span>;
      </span><span><span class="hljs-attr">--foreground</span></span><span>: </span><span><span class="hljs-number">#292520</span></span><span>;
    }
    </span><span><span class="hljs-selector-tag">body</span></span><span> {
      </span><span><span class="hljs-attribute">background-color</span></span><span>: </span><span><span class="hljs-built_in">var</span></span><span>(--background);
      </span><span><span class="hljs-attribute">color</span></span><span>: </span><span><span class="hljs-built_in">var</span></span><span>(--foreground);
    }
    </span></span></code></div></div>
    
    
-   **Fonts:**
    
    -   **Jacquard 24 Charted:** Used for headings and titles
    -   **Kings:** Used for body text and most other UI elements  
        In your Tailwind config, you have:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-attr">fontFamily</span></span><span>: {
      </span><span><span class="hljs-attr">jacquard</span></span><span>: [</span><span><span class="hljs-string">'"Jacquard 24 Charted"'</span></span><span>, </span><span><span class="hljs-string">"serif"</span></span><span>],
      </span><span><span class="hljs-attr">kings</span></span><span>: [</span><span><span class="hljs-string">"Kings"</span></span><span>, </span><span><span class="hljs-string">"serif"</span></span><span>],
    },
    </span></span></code></div></div>
    
    
    And in your global CSS:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">css</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-css"><span><span><span class="hljs-selector-class">.font-jacquard</span></span><span> {
      </span><span><span class="hljs-attribute">font-family</span></span><span>: </span><span><span class="hljs-string">"Jacquard 24 Charted"</span></span><span>, serif;
    }
    </span><span><span class="hljs-selector-class">.font-kings</span></span><span> {
      </span><span><span class="hljs-attribute">font-family</span></span><span>: </span><span><span class="hljs-string">"Kings"</span></span><span>, serif;
    }
    </span></span></code></div></div>
    
    

### B. Design Tokens and Consistency

By centralizing your colors, fonts, spacing, and component variants (e.g., button variants, card styles) in Tailwind’s configuration, you ensure consistency. For example, using your defined classes like `bg-background` and `text-foreground` everywhere creates a uniform look. You should also consider:

-   **Spacing:** Define spacing scales (e.g., `p-4`, `m-4`) consistently.
-   **Component Variants:** Use the variants built into ShadCN UI components (like `variant="outline"`) so that buttons, inputs, etc., share the same look and behavior across the app.

___

## 2\. Organizing UI Components

### A. Component Folder Structure

Place all reusable UI components in a dedicated folder, for instance:


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">bash</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre"><span><span>/src
  /components
    /ui
      Button.tsx
      Card.tsx
      Input.tsx
      Tabs.tsx
      Badge.tsx
      ConfirmationDialog.tsx
      Toaster.tsx
    DocumentProcessingTab.tsx
    MotionHistory.tsx
    ReminderList.tsx
    HelpButton.tsx
</span></span></code></div></div>


Each component should:

-   Be built using ShadCN UI as a base (which in turn uses Radix UI primitives).
-   Accept props that allow for flexibility (e.g., dynamic content, variant options).
-   Use Tailwind CSS classes for spacing, colors, and typography.

### B. Component Usage Examples from Your Codebase

1.  **Cards:**  
    Used extensively in your admin dashboard to group notifications, offender lists, system settings, and more.
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span>&lt;</span><span><span class="hljs-title class_">Card</span></span><span> className=</span><span><span class="hljs-string">"bg-background border border-foreground mb-6"</span></span><span>&gt;
      </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">CardHeader</span></span></span></span><span>&gt;
        </span><span><span class="hljs-tag">&lt;<span class="hljs-name">CardTitle</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"font-jacquard"</span></span><span>&gt;Recent Notifications</span><span><span class="hljs-tag">&lt;/<span class="hljs-name">CardTitle</span></span></span><span>&gt;
      </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">CardHeader</span></span></span><span>&gt;
      </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">CardContent</span></span></span></span><span>&gt;
        {/* Render notifications here */}
      </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">CardContent</span></span></span><span>&gt;
    &lt;/</span><span><span class="hljs-title class_">Card</span></span><span>&gt;
    </span></span></code></div></div>
    
    
2.  **Tabs:**  
    Both the admin dashboard and offender profile use tabbed interfaces to switch between sections like Profile, Notifications, Motions, Offender Services, Help, and Settings.
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span>&lt;</span><span><span class="hljs-title class_">Tabs</span></span><span> defaultValue=</span><span><span class="hljs-string">"notifications"</span></span><span> className=</span><span><span class="hljs-string">"w-full"</span></span><span>&gt;
      </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">TabsList</span></span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"w-full mb-6 bg-background border border-foreground"</span></span><span>&gt;
        </span><span><span class="hljs-tag">&lt;<span class="hljs-name">TabsTrigger</span></span></span><span> </span><span><span class="hljs-attr">value</span></span><span>=</span><span><span class="hljs-string">"notifications"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"flex-1 font-kings"</span></span><span>&gt;
          Notifications
        </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsTrigger</span></span></span><span>&gt;
        </span><span><span class="hljs-tag">&lt;<span class="hljs-name">TabsTrigger</span></span></span><span> </span><span><span class="hljs-attr">value</span></span><span>=</span><span><span class="hljs-string">"offenders"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"flex-1 font-kings"</span></span><span>&gt;
          Offenders
        </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsTrigger</span></span></span><span>&gt;
        {/* Additional tabs */}
      </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsList</span></span></span><span>&gt;
      </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">TabsContent</span></span></span></span><span> </span><span><span class="hljs-attr">value</span></span><span>=</span><span><span class="hljs-string">"notifications"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"scrollable-area"</span></span><span>&gt;
        {/* Content for notifications */}
      </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsContent</span></span></span><span>&gt;
      {</span><span><span class="hljs-comment">/* More TabsContent components */</span></span><span>}
    &lt;/</span><span><span class="hljs-title class_">Tabs</span></span><span>&gt;
    </span></span></code></div></div>
    
    
3.  **Buttons and Inputs:**  
    Buttons (with variants such as outline or primary) and inputs are used for actions (e.g., search, submit forms, delete operations).
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span>&lt;</span><span><span class="hljs-title class_">Input</span></span><span>
      </span><span><span class="hljs-keyword">type</span></span><span>=</span><span><span class="hljs-string">"text"</span></span><span>
      placeholder=</span><span><span class="hljs-string">"Search by number or name"</span></span><span>
      className=</span><span><span class="hljs-string">"bg-background border border-foreground font-kings"</span></span><span>
    /&gt;
    </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">Button</span></span></span></span><span> </span><span><span class="hljs-attr">variant</span></span><span>=</span><span><span class="hljs-string">"outline"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"bg-background border border-foreground font-kings"</span></span><span>&gt;
      Search
    </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">Button</span></span></span><span>&gt;
    </span></span></code></div></div>
    
    

___

## 3\. Responsiveness and Mobile-First Approach

### A. Mobile-First with Tailwind CSS

Tailwind CSS is inherently mobile-first. Your styles should assume a mobile screen by default, then apply responsive utilities (e.g., `sm:`, `md:`, `lg:`) for larger screens. For example:

-   **Container Layout:**  
    Use responsive containers:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span>&lt;div className=</span><span><span class="hljs-string">"container mx-auto p-4"</span></span><span>&gt;
      {</span><span><span class="hljs-comment">/* Your content */</span></span><span>}
    &lt;/div&gt;
    </span></span></code></div></div>
    
    
-   **Tabs and Grid/Flex Layouts:**  
    Use flex or grid for responsive layouts. In your admin dashboard, your tabs automatically adjust because you’re using classes like `flex-1` on each `TabsTrigger`.

### B. Specific Considerations for Admin Dashboard and Offender Profile

1.  **Admin Dashboard:**
    
    -   **Layout:**  
        Use a container that adapts to mobile screens. For example, use `p-4` for padding and ensure that each Card or component stacks vertically on narrow screens.
    -   **Tabs:**  
        Make sure the tab list scrolls horizontally if there are many tabs. Use a class like `overflow-x-auto` on the `TabsList`.
    -   **Action Buttons:**  
        Ensure buttons and inputs are large enough to tap easily on mobile. Tailwind utilities like `py-2 px-4` can help.
2.  **Offender Profile:**
    
    -   **Simple Navigation:**  
        Offender profiles might have fewer options (Profile, Cases, Motions, Reminders, Notifications), so the tabs can be designed similarly but optimized for quick access.
    -   **Responsive Content Areas:**  
        For the offender’s data (text, PDF downloads, etc.), ensure that your content containers scroll properly. Use classes like `scrollable-area` to handle overflow.

### C. Performance and Interactivity

-   **Reactive Components:**  
    ShadCN UI components are built to be reactive and accessible. They are designed to perform well on mobile devices.
-   **Touch-Friendly:**  
    Ensure that interactive elements (buttons, tabs) have sufficient touch targets. Use Tailwind’s spacing utilities (e.g., `p-3`, `m-2`) to maintain proper spacing.
-   **Media Queries and Breakpoints:**  
    Use Tailwind breakpoints to adjust font sizes and spacing. For example:
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">css</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-css"><span><span>&lt;</span><span><span class="hljs-selector-tag">h1</span></span><span> className="text-</span><span><span class="hljs-number">2</span></span><span>xl sm:text-</span><span><span class="hljs-number">3</span></span><span>xl md:text-</span><span><span class="hljs-number">4</span></span><span>xl font-jacquard<span class="hljs-string">"&gt;
      Court Jester Dashboard
    &lt;/h1&gt;
    </span></span></span></code></div></div>
    
    
-   **Scrollability:**  
    The `.scrollable-area` class is defined in your global CSS to handle scrolling for areas with potentially long lists (like notifications or offender lists).

___

## 4\. Putting It All Together

### A. Sample Global Layout (Admin Dashboard)


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">tsx</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-tsx"><span><span><span class="hljs-comment">// app/admin/dashboard/page.tsx</span></span><span>
</span><span><span class="hljs-string">"use client"</span></span><span>;

</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">Tabs</span></span><span>, </span><span><span class="hljs-title class_">TabsContent</span></span><span>, </span><span><span class="hljs-title class_">TabsList</span></span><span>, </span><span><span class="hljs-title class_">TabsTrigger</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/components/ui/tabs"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">Card</span></span><span>, </span><span><span class="hljs-title class_">CardContent</span></span><span>, </span><span><span class="hljs-title class_">CardHeader</span></span><span>, </span><span><span class="hljs-title class_">CardTitle</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/components/ui/card"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">Button</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/components/ui/button"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">Input</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/components/ui/input"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">Badge</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/components/ui/badge"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">HelpButton</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/components/help-button"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">Toaster</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/components/ui/toaster"</span></span><span>;

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">default</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">AdminDashboardPage</span></span><span>(</span><span><span class="hljs-params"></span></span><span>) {
  </span><span><span class="hljs-comment">// State and effects omitted for brevity</span></span><span>
  </span><span><span class="hljs-keyword">return</span></span><span> (
    </span><span><span class="language-xml"><span class="hljs-tag">&lt;<span class="hljs-name">div</span></span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"min-h-screen bg-background text-foreground"</span></span><span>&gt;
      </span><span><span class="hljs-tag">&lt;<span class="hljs-name">div</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"container mx-auto p-4"</span></span><span>&gt;
        </span><span><span class="hljs-tag">&lt;<span class="hljs-name">div</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"flex items-center justify-between mb-6"</span></span><span>&gt;
          </span><span><span class="hljs-tag">&lt;<span class="hljs-name">h1</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"text-3xl font-jacquard"</span></span><span>&gt;Admin Dashboard</span><span><span class="hljs-tag">&lt;/<span class="hljs-name">h1</span></span></span><span>&gt;
          </span><span><span class="hljs-tag">&lt;<span class="hljs-name">HelpButton</span></span></span><span> /&gt;
        </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">div</span></span></span><span>&gt;
        </span><span><span class="hljs-tag">&lt;<span class="hljs-name">Tabs</span></span></span><span> </span><span><span class="hljs-attr">defaultValue</span></span><span>=</span><span><span class="hljs-string">"notifications"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"w-full"</span></span><span>&gt;
          </span><span><span class="hljs-tag">&lt;<span class="hljs-name">TabsList</span></span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"w-full mb-6 bg-background border border-foreground overflow-x-auto"</span></span><span>&gt;
            </span><span><span class="hljs-tag">&lt;<span class="hljs-name">TabsTrigger</span></span></span><span> </span><span><span class="hljs-attr">value</span></span><span>=</span><span><span class="hljs-string">"notifications"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"flex-1 font-kings"</span></span><span>&gt;
              Notifications </span><span><span class="hljs-tag">&lt;<span class="hljs-name">Badge</span></span></span><span>&gt;3</span><span><span class="hljs-tag">&lt;/<span class="hljs-name">Badge</span></span></span><span>&gt;
            </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsTrigger</span></span></span><span>&gt;
            </span><span><span class="hljs-tag">&lt;<span class="hljs-name">TabsTrigger</span></span></span><span> </span><span><span class="hljs-attr">value</span></span><span>=</span><span><span class="hljs-string">"offenders"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"flex-1 font-kings"</span></span><span>&gt;
              Offenders
            </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsTrigger</span></span></span><span>&gt;
            </span><span><span class="hljs-tag">&lt;<span class="hljs-name">TabsTrigger</span></span></span><span> </span><span><span class="hljs-attr">value</span></span><span>=</span><span><span class="hljs-string">"motions"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"flex-1 font-kings"</span></span><span>&gt;
              Motions
            </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsTrigger</span></span></span><span>&gt;
            </span><span><span class="hljs-tag">&lt;<span class="hljs-name">TabsTrigger</span></span></span><span> </span><span><span class="hljs-attr">value</span></span><span>=</span><span><span class="hljs-string">"settings"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"flex-1 font-kings"</span></span><span>&gt;
              Settings
            </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsTrigger</span></span></span><span>&gt;
            </span><span><span class="hljs-tag">&lt;<span class="hljs-name">TabsTrigger</span></span></span><span> </span><span><span class="hljs-attr">value</span></span><span>=</span><span><span class="hljs-string">"help"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"flex-1 font-kings"</span></span><span>&gt;
              Help
            </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsTrigger</span></span></span><span>&gt;
          </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsList</span></span></span><span>&gt;
          </span><span><span class="hljs-tag">&lt;<span class="hljs-name">TabsContent</span></span></span><span> </span><span><span class="hljs-attr">value</span></span><span>=</span><span><span class="hljs-string">"notifications"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"scrollable-area"</span></span><span>&gt;
            {/* Notifications content rendered via Cards */}
          </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsContent</span></span></span><span>&gt;
          </span><span><span class="hljs-tag">&lt;<span class="hljs-name">TabsContent</span></span></span><span> </span><span><span class="hljs-attr">value</span></span><span>=</span><span><span class="hljs-string">"offenders"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"scrollable-area"</span></span><span>&gt;
            {/* Offender list and search */}
          </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsContent</span></span></span><span>&gt;
          </span><span><span class="hljs-tag">&lt;<span class="hljs-name">TabsContent</span></span></span><span> </span><span><span class="hljs-attr">value</span></span><span>=</span><span><span class="hljs-string">"motions"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"scrollable-area"</span></span><span>&gt;
            {/* Motion templates and creation panel */}
          </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsContent</span></span></span><span>&gt;
          </span><span><span class="hljs-tag">&lt;<span class="hljs-name">TabsContent</span></span></span><span> </span><span><span class="hljs-attr">value</span></span><span>=</span><span><span class="hljs-string">"settings"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"scrollable-area"</span></span><span>&gt;
            {/* System settings */}
          </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsContent</span></span></span><span>&gt;
          </span><span><span class="hljs-tag">&lt;<span class="hljs-name">TabsContent</span></span></span><span> </span><span><span class="hljs-attr">value</span></span><span>=</span><span><span class="hljs-string">"help"</span></span><span> </span><span><span class="hljs-attr">className</span></span><span>=</span><span><span class="hljs-string">"scrollable-area"</span></span><span>&gt;
            {/* Help and FAQ content */}
          </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">TabsContent</span></span></span><span>&gt;
        </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">Tabs</span></span></span><span>&gt;
      </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">div</span></span></span><span>&gt;
      </span><span><span class="hljs-tag">&lt;<span class="hljs-name">Toaster</span></span></span><span> /&gt;
    </span><span><span class="hljs-tag">&lt;/<span class="hljs-name">div</span></span></span><span>&gt;
  );
}
</span></span></code></div></div>


### B. Offender Profile Layout

A similar layout applies to the offender profile page but with fewer tabs (e.g., Profile, Cases, Motions, Reminders, Notifications). Use similar container and responsive classes to ensure consistency.

___

## Final Thoughts

1.  **Design System Setup:**
    
    -   Centralize your design tokens (colors, fonts, spacing) in Tailwind config and global CSS.
    -   Use ShadCN UI’s pre‑built components to ensure consistency and accessibility.
2.  **Component Organization:**
    
    -   Organize reusable components in a dedicated folder.
    -   Define specific components for Cards, Tabs, Buttons, Inputs, etc., using your two fonts (Jacquard for headings, Kings for body).
3.  **Responsive, Mobile‑First Approach:**
    
    -   Use Tailwind’s mobile-first classes and breakpoints.
    -   Ensure layouts are fluid using containers, flexbox, or grid.
    -   Use classes like `overflow-x-auto` for horizontal scrolling of tabs on small devices.
4.  **UI Integration with Data:**
    
    -   Populate components by mapping over API-fetched data.
    -   Use Toasts and ConfirmationDialogs for user feedback and interactive actions.

This comprehensive approach should give you a robust, responsive, and consistent design system for both the admin dashboard and offender profile pages, ensuring the app works seamlessly on mobile devices while maintaining a clean, modern look with only two colors and two fonts.

If you have any further questions or need additional detail on specific parts of the design system, let me know!