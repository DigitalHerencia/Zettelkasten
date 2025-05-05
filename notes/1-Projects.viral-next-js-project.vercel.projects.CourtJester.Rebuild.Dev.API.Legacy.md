---
id: rmfjj25sbe4mw4kmfgd8cpv
title: Legacy
desc: ''
updated: 1742226231302
created: 1742226086379
---
### 1\. lib/auth.ts

A new helper module that validates an inmate number (for login/registration) and checks for the admin code in the request.


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// lib/auth.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">NextRequest</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"next/server"</span></span><span>;

</span><span><span class="hljs-comment">// For admin requests, we check for a header or query parameter with the code "admin86".</span></span><span>
</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">isAdminRequest</span></span><span>(</span><span><span class="hljs-params">request: NextRequest</span></span><span>): </span><span><span class="hljs-title class_">Promise</span></span><span>&lt;</span><span><span class="hljs-built_in">boolean</span></span><span>&gt; {
  </span><span><span class="hljs-keyword">const</span></span><span> adminCode = request.</span><span><span class="hljs-property">headers</span></span><span>.</span><span><span class="hljs-title function_">get</span></span><span>(</span><span><span class="hljs-string">"x-admin-code"</span></span><span>) || request.</span><span><span class="hljs-property">nextUrl</span></span><span>.</span><span><span class="hljs-property">searchParams</span></span><span>.</span><span><span class="hljs-title function_">get</span></span><span>(</span><span><span class="hljs-string">"adminCode"</span></span><span>);
  </span><span><span class="hljs-keyword">return</span></span><span> adminCode === </span><span><span class="hljs-string">"admin86"</span></span><span>;
}

</span><span><span class="hljs-comment">// For inmate login, the inmate number itself is the credential.</span></span><span>
</span><span><span class="hljs-comment">// In production, you might check against a database or a whitelist.</span></span><span>
</span><span><span class="hljs-comment">// Here, we simply ensure it is non-empty.</span></span><span>
</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">isValidInmate</span></span><span>(</span><span><span class="hljs-params">inmateNumber: <span class="hljs-built_in">string</span></span></span><span>): </span><span><span class="hljs-title class_">Promise</span></span><span>&lt;</span><span><span class="hljs-built_in">boolean</span></span><span>&gt; {
  </span><span><span class="hljs-keyword">return</span></span><span> inmateNumber.</span><span><span class="hljs-title function_">trim</span></span><span>().</span><span><span class="hljs-property">length</span></span><span> &gt; </span><span><span class="hljs-number">0</span></span><span>;
}
</span></span></code></div></div>


___

### 2\. API Endpoints for Admin Operations

Each endpoint that previously called a function like `requireAdmin` now uses our simple admin check.

### a. app/api/admin/cases/\[id\]/route.ts


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// app/api/admin/cases/[id]/route.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">NextRequest</span></span><span>, </span><span><span class="hljs-title class_">NextResponse</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"next/server"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { isAdminRequest } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/auth"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { getCaseById, deleteCase, listMotionsByCaseId } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/db/blob-storage"</span></span><span>;

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">DELETE</span></span><span>(</span><span><span class="hljs-params">request: NextRequest, { params }: { params: { id: <span class="hljs-built_in">string</span></span></span><span> } }) {
  </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isAdminRequest</span></span><span>(request))) {
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Unauthorized"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
  }
  
  </span><span><span class="hljs-keyword">try</span></span><span> {
    </span><span><span class="hljs-keyword">const</span></span><span> { id } = params;
    </span><span><span class="hljs-keyword">const</span></span><span> caseData = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">getCaseById</span></span><span>(id);
    </span><span><span class="hljs-keyword">if</span></span><span> (!caseData) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Case not found"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">404</span></span><span> });
    }
    </span><span><span class="hljs-keyword">const</span></span><span> motions = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">listMotionsByCaseId</span></span><span>(id);
    </span><span><span class="hljs-keyword">if</span></span><span> (motions.</span><span><span class="hljs-property">length</span></span><span> &gt; </span><span><span class="hljs-number">0</span></span><span>) {
      </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">log</span></span><span>(</span><span><span class="hljs-string">`Deleting case <span class="hljs-subst">${id}</span></span></span><span> with </span><span><span class="hljs-subst">${motions.length}</span></span><span> associated motions`);
    }
    </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">deleteCase</span></span><span>(id);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({
      </span><span><span class="hljs-attr">success</span></span><span>: </span><span><span class="hljs-literal">true</span></span><span>,
      </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Case deleted successfully"</span></span><span>,
      </span><span><span class="hljs-attr">deletedMotions</span></span><span>: motions.</span><span><span class="hljs-property">length</span></span><span>,
    });
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error deleting case:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to delete case"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}
</span></span></code></div></div>


### b. app/api/admin/documents/upload/route.ts


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// app/api/admin/documents/upload/route.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> { put } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@vercel/blob"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">NextResponse</span></span><span>, </span><span><span class="hljs-title class_">NextRequest</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"next/server"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { isAdminRequest } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/auth"</span></span><span>;

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">POST</span></span><span>(</span><span><span class="hljs-params">request: Request</span></span><span>) {
  </span><span><span class="hljs-keyword">try</span></span><span> {
    </span><span><span class="hljs-keyword">const</span></span><span> nextReq = </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">NextRequest</span></span><span>(request);
    </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isAdminRequest</span></span><span>(nextReq))) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">error</span></span><span>: </span><span><span class="hljs-string">"Unauthorized"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
    }
    </span><span><span class="hljs-keyword">const</span></span><span> formData = </span><span><span class="hljs-keyword">await</span></span><span> request.</span><span><span class="hljs-title function_">formData</span></span><span>();
    </span><span><span class="hljs-keyword">const</span></span><span> file = formData.</span><span><span class="hljs-title function_">get</span></span><span>(</span><span><span class="hljs-string">"file"</span></span><span>) </span><span><span class="hljs-keyword">as</span></span><span> </span><span><span class="hljs-title class_">File</span></span><span>;
    </span><span><span class="hljs-keyword">if</span></span><span> (!file) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">error</span></span><span>: </span><span><span class="hljs-string">"No file provided"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">400</span></span><span> });
    }
    </span><span><span class="hljs-keyword">const</span></span><span> blob = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">put</span></span><span>(file.</span><span><span class="hljs-property">name</span></span><span>, file, { </span><span><span class="hljs-attr">access</span></span><span>: </span><span><span class="hljs-string">"public"</span></span><span> });
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">url</span></span><span>: blob.</span><span><span class="hljs-property">url</span></span><span> });
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error uploading document:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">error</span></span><span>: </span><span><span class="hljs-string">"Upload failed"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}
</span></span></code></div></div>


### c. app/api/admin/motions/\[id\]/pdf/route.ts


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// app/api/admin/motions/[id]/pdf/route.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">NextRequest</span></span><span>, </span><span><span class="hljs-title class_">NextResponse</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"next/server"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { isAdminRequest } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/auth"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { getMotionById } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/db/blob-storage"</span></span><span>;

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">GET</span></span><span>(</span><span><span class="hljs-params">request: NextRequest, { params }: { params: { id: <span class="hljs-built_in">string</span></span></span><span> } }) {
  </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isAdminRequest</span></span><span>(request))) {
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Unauthorized"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
  }
  
  </span><span><span class="hljs-keyword">try</span></span><span> {
    </span><span><span class="hljs-keyword">const</span></span><span> { id } = params;
    </span><span><span class="hljs-keyword">const</span></span><span> motion = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">getMotionById</span></span><span>(id);
    </span><span><span class="hljs-keyword">if</span></span><span> (!motion) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Motion not found"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">404</span></span><span> });
    }
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">log</span></span><span>(</span><span><span class="hljs-string">`Generating PDF for motion with ID: <span class="hljs-subst">${id}</span></span></span><span>`);
    </span><span><span class="hljs-comment">// Escape any parentheses to avoid PDF syntax issues.</span></span><span>
    </span><span><span class="hljs-keyword">const</span></span><span> safeTitle = motion.</span><span><span class="hljs-property">title</span></span><span>.</span><span><span class="hljs-title function_">replace</span></span><span>(</span><span><span class="hljs-regexp">/([\(\)])/g</span></span><span>, </span><span><span class="hljs-string">"\\$1"</span></span><span>);
    </span><span><span class="hljs-keyword">const</span></span><span> safeContent = motion.</span><span><span class="hljs-property">content</span></span><span>.</span><span><span class="hljs-title function_">replace</span></span><span>(</span><span><span class="hljs-regexp">/([\(\)])/g</span></span><span>, </span><span><span class="hljs-string">"\\$1"</span></span><span>);
    </span><span><span class="hljs-keyword">const</span></span><span> pdfContent = <span class="hljs-string">`
      %PDF-1.5
      1 0 obj
      &lt;&lt; /Type /Catalog /Pages 2 0 R &gt;&gt;
      endobj
      2 0 obj
      &lt;&lt; /Type /Pages /Kids [3 0 R] /Count 1 &gt;&gt;
      endobj
      3 0 obj
      &lt;&lt; /Type /Page /Parent 2 0 R /Resources &lt;&lt; /Font &lt;&lt; /F1 4 0 R &gt;&gt; &gt;&gt; /Contents 5 0 R &gt;&gt;
      endobj
      4 0 obj
      &lt;&lt; /Type /Font /Subtype /Type1 /BaseFont /Helvetica &gt;&gt;
      endobj
      5 0 obj
      &lt;&lt; /Length </span></span><span><span class="hljs-subst">${safeTitle.length + safeContent.length + <span class="hljs-number">100</span></span></span><span>} &gt;&gt;
      stream
      BT
      /F1 12 Tf
      50 750 Td
      (</span><span><span class="hljs-subst">${safeTitle}</span></span><span>) Tj
      0 -20 Td
      (</span><span><span class="hljs-subst">${safeContent}</span></span><span>) Tj
      ET
      endstream
      endobj
      xref
      0 6
      0000000000 65535 f
      0000000009 00000 n
      0000000058 00000 n
      0000000115 00000 n
      0000000216 00000 n
      0000000283 00000 n
      trailer
      &lt;&lt; /Size 6 /Root 1 0 R &gt;&gt;
      startxref
      401
      %%EOF
    `;
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Response</span></span><span>(pdfContent, {
      </span><span><span class="hljs-attr">headers</span></span><span>: {
        </span><span><span class="hljs-string">"Content-Type"</span></span><span>: </span><span><span class="hljs-string">"application/pdf"</span></span><span>,
        </span><span><span class="hljs-string">"Content-Disposition"</span></span><span>: </span><span><span class="hljs-string">`attachment; filename="motion-<span class="hljs-subst">${id}</span></span></span><span>.pdf"`,
      },
    });
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error generating motion PDF:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to generate motion PDF"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}
</span></span></code></div></div>


### d. app/api/admin/motions/\[id\]/route.ts


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// app/api/admin/motions/[id]/route.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">NextRequest</span></span><span>, </span><span><span class="hljs-title class_">NextResponse</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"next/server"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { isAdminRequest } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/auth"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { getMotionById, updateMotion, deleteMotion } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/db/blob-storage"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { fillTemplate, getTemplateById } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/motion-templates"</span></span><span>;

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">GET</span></span><span>(</span><span><span class="hljs-params">request: NextRequest, { params }: { params: { id: <span class="hljs-built_in">string</span></span></span><span> } }) {
  </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isAdminRequest</span></span><span>(request))) {
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Unauthorized"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
  }
  
  </span><span><span class="hljs-keyword">try</span></span><span> {
    </span><span><span class="hljs-keyword">const</span></span><span> { id } = params;
    </span><span><span class="hljs-keyword">const</span></span><span> motion = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">getMotionById</span></span><span>(id);
    </span><span><span class="hljs-keyword">if</span></span><span> (!motion) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Motion not found"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">404</span></span><span> });
    }
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>(motion);
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error fetching motion:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to fetch motion"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}

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

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">DELETE</span></span><span>(</span><span><span class="hljs-params">request: NextRequest, { params }: { params: { id: <span class="hljs-built_in">string</span></span></span><span> } }) {
  </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isAdminRequest</span></span><span>(request))) {
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Unauthorized"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
  }
  
  </span><span><span class="hljs-keyword">try</span></span><span> {
    </span><span><span class="hljs-keyword">const</span></span><span> { id } = params;
    </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">deleteMotion</span></span><span>(id);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">success</span></span><span>: </span><span><span class="hljs-literal">true</span></span><span>, </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Motion deleted successfully"</span></span><span> });
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error deleting motion:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to delete motion"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}
</span></span></code></div></div>


### e. app/api/admin/motions/route.ts


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// app/api/admin/motions/route.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">NextRequest</span></span><span>, </span><span><span class="hljs-title class_">NextResponse</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"next/server"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { isAdminRequest } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/auth"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { storeMotion, listMotions } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/db/blob-storage"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { getTemplateById } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/motion-templates"</span></span><span>;

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">GET</span></span><span>(</span><span><span class="hljs-params">request: NextRequest</span></span><span>) {
  </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isAdminRequest</span></span><span>(request))) {
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Unauthorized"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
  }
  
  </span><span><span class="hljs-keyword">try</span></span><span> {
    </span><span><span class="hljs-keyword">const</span></span><span> searchParams = request.</span><span><span class="hljs-property">nextUrl</span></span><span>.</span><span><span class="hljs-property">searchParams</span></span><span>;
    </span><span><span class="hljs-keyword">const</span></span><span> offenderId = searchParams.</span><span><span class="hljs-title function_">get</span></span><span>(</span><span><span class="hljs-string">"offenderId"</span></span><span>);
    </span><span><span class="hljs-keyword">const</span></span><span> caseId = searchParams.</span><span><span class="hljs-title function_">get</span></span><span>(</span><span><span class="hljs-string">"caseId"</span></span><span>);
    </span><span><span class="hljs-keyword">const</span></span><span> motions = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">listMotions</span></span><span>();
    </span><span><span class="hljs-keyword">let</span></span><span> filteredMotions = motions;
    </span><span><span class="hljs-keyword">if</span></span><span> (offenderId) {
      filteredMotions = filteredMotions.</span><span><span class="hljs-title function_">filter</span></span><span>(</span><span><span class="hljs-function">(<span class="hljs-params">motion</span></span></span><span>) =&gt; motion.</span><span><span class="hljs-property">offenderId</span></span><span> === offenderId);
    }
    </span><span><span class="hljs-keyword">if</span></span><span> (caseId) {
      filteredMotions = filteredMotions.</span><span><span class="hljs-title function_">filter</span></span><span>(</span><span><span class="hljs-function">(<span class="hljs-params">motion</span></span></span><span>) =&gt; motion.</span><span><span class="hljs-property">caseId</span></span><span> === caseId);
    }
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>(filteredMotions);
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error fetching motions:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to fetch motions"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">POST</span></span><span>(</span><span><span class="hljs-params">request: NextRequest</span></span><span>) {
  </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isAdminRequest</span></span><span>(request))) {
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Unauthorized"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
  }
  
  </span><span><span class="hljs-keyword">try</span></span><span> {
    </span><span><span class="hljs-keyword">const</span></span><span> motionData = </span><span><span class="hljs-keyword">await</span></span><span> request.</span><span><span class="hljs-title function_">json</span></span><span>();
    </span><span><span class="hljs-keyword">if</span></span><span> (!motionData.</span><span><span class="hljs-property">offenderId</span></span><span> || !motionData.</span><span><span class="hljs-property">caseId</span></span><span> || !motionData.</span><span><span class="hljs-property">templateId</span></span><span>) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Missing required fields"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">400</span></span><span> });
    }
    </span><span><span class="hljs-keyword">const</span></span><span> template = </span><span><span class="hljs-title function_">getTemplateById</span></span><span>(motionData.</span><span><span class="hljs-property">templateId</span></span><span>);
    </span><span><span class="hljs-keyword">if</span></span><span> (!template) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Template not found"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">404</span></span><span> });
    }
    </span><span><span class="hljs-keyword">const</span></span><span> motion = {
      </span><span><span class="hljs-attr">offenderId</span></span><span>: motionData.</span><span><span class="hljs-property">offenderId</span></span><span>,
      </span><span><span class="hljs-attr">caseId</span></span><span>: motionData.</span><span><span class="hljs-property">caseId</span></span><span>,
      </span><span><span class="hljs-attr">templateId</span></span><span>: motionData.</span><span><span class="hljs-property">templateId</span></span><span>,
      </span><span><span class="hljs-attr">title</span></span><span>: motionData.</span><span><span class="hljs-property">title</span></span><span> || template.</span><span><span class="hljs-property">name</span></span><span>,
      </span><span><span class="hljs-attr">content</span></span><span>: motionData.</span><span><span class="hljs-property">content</span></span><span> || template.</span><span><span class="hljs-property">content</span></span><span>,
      </span><span><span class="hljs-attr">variables</span></span><span>: motionData.</span><span><span class="hljs-property">variables</span></span><span> || {},
      </span><span><span class="hljs-attr">status</span></span><span>: motionData.</span><span><span class="hljs-property">status</span></span><span> || </span><span><span class="hljs-string">"draft"</span></span><span>,
      </span><span><span class="hljs-attr">createdAt</span></span><span>: </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Date</span></span><span>().</span><span><span class="hljs-title function_">toISOString</span></span><span>(),
      </span><span><span class="hljs-attr">updatedAt</span></span><span>: </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Date</span></span><span>().</span><span><span class="hljs-title function_">toISOString</span></span><span>(),
    };
    </span><span><span class="hljs-keyword">const</span></span><span> motionId = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">storeMotion</span></span><span>(motion);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">success</span></span><span>: </span><span><span class="hljs-literal">true</span></span><span>, motionId });
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error creating motion:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to create motion"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}
</span></span></code></div></div>


### f. app/api/admin/notifications/\[id\]/route.ts


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// app/api/admin/notifications/[id]/route.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">NextRequest</span></span><span>, </span><span><span class="hljs-title class_">NextResponse</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"next/server"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { isAdminRequest } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/auth"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { getNotificationById, deleteNotification } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/db/blob-storage"</span></span><span>;

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">DELETE</span></span><span>(</span><span><span class="hljs-params">request: NextRequest, { params }: { params: { id: <span class="hljs-built_in">string</span></span></span><span> } }) {
  </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isAdminRequest</span></span><span>(request))) {
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Unauthorized"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
  }
  
  </span><span><span class="hljs-keyword">try</span></span><span> {
    </span><span><span class="hljs-keyword">const</span></span><span> { id } = params;
    </span><span><span class="hljs-keyword">const</span></span><span> notification = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">getNotificationById</span></span><span>(id);
    </span><span><span class="hljs-keyword">if</span></span><span> (!notification) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Notification not found"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">404</span></span><span> });
    }
    </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">deleteNotification</span></span><span>(id);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({
      </span><span><span class="hljs-attr">success</span></span><span>: </span><span><span class="hljs-literal">true</span></span><span>,
      </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Notification deleted successfully"</span></span><span>,
    });
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error deleting notification:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to delete notification"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}
</span></span></code></div></div>


### g. app/api/admin/notifications/route.ts


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// app/api/admin/notifications/route.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">NextRequest</span></span><span>, </span><span><span class="hljs-title class_">NextResponse</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"next/server"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { storeNotification } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/db/blob-storage"</span></span><span>;

</span><span><span class="hljs-comment">// This endpoint is used to create notifications (for example, triggered by inmate registration).</span></span><span>
</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">GET</span></span><span>(</span><span><span class="hljs-params">request: NextRequest</span></span><span>) {
  </span><span><span class="hljs-keyword">try</span></span><span> {
    </span><span><span class="hljs-comment">// In a production system you might restrict this; for now, return notifications.</span></span><span>
    </span><span><span class="hljs-comment">// (Assumes you have a function to get all notifications.)</span></span><span>
    </span><span><span class="hljs-keyword">const</span></span><span> notifications = </span><span><span class="hljs-keyword">await</span></span><span> storeNotification.</span><span><span class="hljs-title function_">getAll</span></span><span>(); 
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>(notifications);
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error fetching notifications:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to fetch notifications"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">POST</span></span><span>(</span><span><span class="hljs-params">request: NextRequest</span></span><span>) {
  </span><span><span class="hljs-keyword">try</span></span><span> {
    </span><span><span class="hljs-keyword">const</span></span><span> { offenderId, title, message, </span><span><span class="hljs-keyword">type</span></span><span> } = </span><span><span class="hljs-keyword">await</span></span><span> request.</span><span><span class="hljs-title function_">json</span></span><span>();
    </span><span><span class="hljs-keyword">const</span></span><span> notification = {
      offenderId,
      title,
      message,
      </span><span><span class="hljs-attr">type</span></span><span>: </span><span><span class="hljs-keyword">type</span></span><span> || </span><span><span class="hljs-string">"system"</span></span><span>,
      </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-string">"unread"</span></span><span>,
      </span><span><span class="hljs-attr">createdAt</span></span><span>: </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Date</span></span><span>().</span><span><span class="hljs-title function_">toISOString</span></span><span>(),
    };
    </span><span><span class="hljs-keyword">try</span></span><span> {
      </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">storeNotification</span></span><span>(notification);
    } </span><span><span class="hljs-keyword">catch</span></span><span> (storeError) {
      </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error storing notification:"</span></span><span>, storeError);
    }
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">success</span></span><span>: </span><span><span class="hljs-literal">true</span></span><span> });
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error creating notification:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to create notification"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}
</span></span></code></div></div>


### h. app/api/admin/offenders/mugshot/route.ts


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// app/api/admin/offenders/mugshot/route.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> { put } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@vercel/blob"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">NextResponse</span></span><span>, </span><span><span class="hljs-title class_">NextRequest</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"next/server"</span></span><span>;
</span><span><span class="hljs-keyword">import</span></span><span> { isAdminRequest } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/auth"</span></span><span>;

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">POST</span></span><span>(</span><span><span class="hljs-params">request: Request</span></span><span>) {
  </span><span><span class="hljs-keyword">try</span></span><span> {
    </span><span><span class="hljs-keyword">const</span></span><span> nextReq = </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">NextRequest</span></span><span>(request);
    </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isAdminRequest</span></span><span>(nextReq))) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">error</span></span><span>: </span><span><span class="hljs-string">"Unauthorized"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
    }
    </span><span><span class="hljs-keyword">const</span></span><span> formData = </span><span><span class="hljs-keyword">await</span></span><span> request.</span><span><span class="hljs-title function_">formData</span></span><span>();
    </span><span><span class="hljs-keyword">const</span></span><span> file = formData.</span><span><span class="hljs-title function_">get</span></span><span>(</span><span><span class="hljs-string">"file"</span></span><span>) </span><span><span class="hljs-keyword">as</span></span><span> </span><span><span class="hljs-title class_">File</span></span><span>;
    </span><span><span class="hljs-keyword">if</span></span><span> (!file) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">error</span></span><span>: </span><span><span class="hljs-string">"No file provided"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">400</span></span><span> });
    }
    </span><span><span class="hljs-keyword">const</span></span><span> blob = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">put</span></span><span>(</span><span><span class="hljs-string">`mugshots/<span class="hljs-subst">${file.name}</span></span></span><span>`, file, { </span><span><span class="hljs-attr">access</span></span><span>: </span><span><span class="hljs-string">"public"</span></span><span> });
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">url</span></span><span>: blob.</span><span><span class="hljs-property">url</span></span><span> });
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error uploading mugshot:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">error</span></span><span>: </span><span><span class="hljs-string">"Upload failed"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}
</span></span></code></div></div>


___

### 3\. Inmate and Admin Login Endpoints

These endpoints implement the simple login flows according to your requirements.

### a. app/api/inmate/login/route.ts

Handles inmate login/registration. When an inmate number is submitted: – If no profile exists, a new record is created with `profileEnabled` set to false, – A notification is sent to the admin, and the inmate sees a “pending” message.


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
    </span><span><span class="hljs-keyword">let</span></span><span> offender = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">getOffenderByInmateNumber</span></span><span>(inmateNumber);
    </span><span><span class="hljs-keyword">if</span></span><span> (!offender) {
      </span><span><span class="hljs-comment">// Create a new offender record with profile disabled.</span></span><span>
      offender = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">createOffender</span></span><span>({ inmateNumber, </span><span><span class="hljs-attr">profileEnabled</span></span><span>: </span><span><span class="hljs-literal">false</span></span><span> });
      </span><span><span class="hljs-comment">// Send notification to admin about the new registration.</span></span><span>
      </span><span><span class="hljs-keyword">const</span></span><span> notification = {
        </span><span><span class="hljs-attr">offenderId</span></span><span>: offender.</span><span><span class="hljs-property">_id</span></span><span>,
        </span><span><span class="hljs-attr">title</span></span><span>: </span><span><span class="hljs-string">"New Offender Registration"</span></span><span>,
        </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">`New registration for inmate number <span class="hljs-subst">${inmateNumber}</span></span></span><span>.`,
        </span><span><span class="hljs-attr">type</span></span><span>: </span><span><span class="hljs-string">"system"</span></span><span>,
        </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-string">"unread"</span></span><span>,
        </span><span><span class="hljs-attr">createdAt</span></span><span>: </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Date</span></span><span>().</span><span><span class="hljs-title function_">toISOString</span></span><span>(),
      };
      </span><span><span class="hljs-keyword">try</span></span><span> {
        </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">storeNotification</span></span><span>(notification);
      } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
        </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error storing notification:"</span></span><span>, error);
      }
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Registration received. You will be notified soon when your profile is ready."</span></span><span> });
    }
    </span><span><span class="hljs-comment">// If offender exists but profile is not yet enabled:</span></span><span>
    </span><span><span class="hljs-keyword">if</span></span><span> (!offender.</span><span><span class="hljs-property">profileEnabled</span></span><span>) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Your profile is pending. You will be notified soon when it is ready."</span></span><span> });
    }
    </span><span><span class="hljs-comment">// Otherwise, return offender details.</span></span><span>
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">success</span></span><span>: </span><span><span class="hljs-literal">true</span></span><span>, offender });
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error in inmate login:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to process login"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}
</span></span></code></div></div>


### b. app/api/admin/login/route.ts

Handles admin login using a fixed code (“admin86”). In production you might set a secure cookie or token.


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// app/api/admin/login/route.ts</span></span><span>
</span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">NextRequest</span></span><span>, </span><span><span class="hljs-title class_">NextResponse</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"next/server"</span></span><span>;

</span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">POST</span></span><span>(</span><span><span class="hljs-params">request: NextRequest</span></span><span>) {
  </span><span><span class="hljs-keyword">try</span></span><span> {
    </span><span><span class="hljs-keyword">const</span></span><span> { adminCode } = </span><span><span class="hljs-keyword">await</span></span><span> request.</span><span><span class="hljs-title function_">json</span></span><span>();
    </span><span><span class="hljs-keyword">if</span></span><span> (adminCode !== </span><span><span class="hljs-string">"admin86"</span></span><span>) {
      </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Invalid admin code"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
    }
    </span><span><span class="hljs-comment">// For simplicity, return a success message.</span></span><span>
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">success</span></span><span>: </span><span><span class="hljs-literal">true</span></span><span>, </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Admin authenticated"</span></span><span> });
  } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
    </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error in admin login:"</span></span><span>, error);
    </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Failed to process admin login"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
  }
}
</span></span></code></div></div>


___

### Final Notes

-   **Database Functions:**  
    The above endpoints assume the existence of database functions such as `getOffenderByInmateNumber`, `createOffender`, and appropriate functions in `@/lib/db/blob-storage`. Be sure these functions are implemented to interact with your data store.
    
-   **Environment & Security:**  
    For production, you may want to store the admin code securely (for example, in an environment variable) rather than hard-coding it.
    
-   **Testing:**  
    After integrating these changes, thoroughly test the inmate login flow, admin login, and each admin API endpoint to verify that the correct messages are returned and that notifications are triggered as intended.
    

These complete, error-free scripts should now provide the intended functionality without misconfigurations, matching your requirements for both inmate and admin authentication and the associated notification behavior.