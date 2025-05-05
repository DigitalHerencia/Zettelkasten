---
id: odkw5gzuk50kplnw76f52if
title: Registration
desc: ''
updated: 1742226914317
created: 1742226882033
---
## 1\. Workflow Overview

### Step 1: New Offender Registration

-   When an offender logs in using their inmate number (which is both their username and password), your system uses Zod validation to ensure the format is correct.
-   If the inmate number is new (i.e. there’s no existing profile), a new offender record is created (with a flag like `profileEnabled: false`) and a notification is stored in the database to alert you (the admin).

### Step 2: Admin Retrieves Notification and Prepares Profile Data

-   On your admin dashboard, you have a dedicated “Document Parsing” section.
-   Here, you can do two things:
    -   **Upload PDFs:**  
        You open a dialog to select a PDF file from your downloads. These PDFs come from the New Mexico Court Case Lookup website.
    -   **Paste Text:**  
        You also have a text input where you can paste information from a standardized form (from the New Mexico Department of Corrections).

### Step 3: Parsing and Populating Offender Profile

-   **PDF Parsing:**  
    When you upload a PDF:
    -   The file is sent to an API endpoint. Instead of just storing it, your backend uses a PDF parsing library to extract text.
    -   For example, you might use the [pdf-parse](https://www.npmjs.com/package/pdf-parse) package. This library converts the PDF into plain text so that you can then apply custom parsing logic (for example, using regular expressions or a custom parser) to extract fields like case number, hearing dates, judge names, etc.
-   **Text Parsing:**  
    For the pasted text:
    -   You send the text via an API endpoint.
    -   Because the text is always in the same format (coming from a form), you can write a parser that uses string manipulation or regular expressions to extract the offender’s personal information (name, date of birth, height, eye color, etc.).
-   Once parsed, you update the offender’s profile in your MongoDB database with all these fields.

### Step 4: Notifying the Offender

-   After you complete the profile setup on the admin side, you send a notification to the offender.
-   This can be done via an API endpoint that updates the offender’s record (setting `profileEnabled: true`) and creates a new notification in the database.
-   Next time the offender logs in, your frontend logic checks the profile status and, since it’s now enabled, takes them directly to their fully populated profile.

___

## 2\. API Endpoints and Package Usage

### A. PDF Upload and Parsing Endpoint

1.  **Endpoint:**  
    `POST /api/admin/documents/upload-and-parse`  
    This endpoint accepts a PDF file and then extracts the text.
    
2.  **Packages:**
    
    -   **@vercel/blob:** For file uploads (if you want to store a temporary copy).
    -   **pdf-parse:** To extract text from the uploaded PDF.
    -   **Custom Parser:** Code that processes the extracted text into structured data.
3.  **Example Code Snippet:**
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// app/api/admin/documents/upload-and-parse/route.ts</span></span><span>
    </span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">NextRequest</span></span><span>, </span><span><span class="hljs-title class_">NextResponse</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"next/server"</span></span><span>;
    </span><span><span class="hljs-keyword">import</span></span><span> { put } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@vercel/blob"</span></span><span>;
    </span><span><span class="hljs-keyword">import</span></span><span> pdfParse </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"pdf-parse"</span></span><span>;
    </span><span><span class="hljs-keyword">import</span></span><span> { isAdminRequest } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/auth"</span></span><span>;
    </span><span><span class="hljs-keyword">import</span></span><span> { updateOffenderProfile } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/db/offenders"</span></span><span>; </span><span><span class="hljs-comment">// Your function to update offender data</span></span><span>
    
    </span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">POST</span></span><span>(</span><span><span class="hljs-params">request: Request</span></span><span>) {
      </span><span><span class="hljs-keyword">try</span></span><span> {
        </span><span><span class="hljs-keyword">const</span></span><span> nextReq = </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">NextRequest</span></span><span>(request);
        </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isAdminRequest</span></span><span>(nextReq))) {
          </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">error</span></span><span>: </span><span><span class="hljs-string">"Unauthorized"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
        }
        </span><span><span class="hljs-keyword">const</span></span><span> formData = </span><span><span class="hljs-keyword">await</span></span><span> request.</span><span><span class="hljs-title function_">formData</span></span><span>();
        </span><span><span class="hljs-keyword">const</span></span><span> file = formData.</span><span><span class="hljs-title function_">get</span></span><span>(</span><span><span class="hljs-string">"file"</span></span><span>) </span><span><span class="hljs-keyword">as</span></span><span> </span><span><span class="hljs-title class_">File</span></span><span>;
        </span><span><span class="hljs-keyword">const</span></span><span> offenderId = formData.</span><span><span class="hljs-title function_">get</span></span><span>(</span><span><span class="hljs-string">"offenderId"</span></span><span>) </span><span><span class="hljs-keyword">as</span></span><span> </span><span><span class="hljs-built_in">string</span></span><span>;
        </span><span><span class="hljs-keyword">if</span></span><span> (!file || !offenderId) {
          </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">error</span></span><span>: </span><span><span class="hljs-string">"File and offender ID are required"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">400</span></span><span> });
        }
        
        </span><span><span class="hljs-comment">// Optionally, store the file temporarily using Vercel Blob</span></span><span>
        </span><span><span class="hljs-comment">// const blob = await put(file.name, file, { access: "public" });</span></span><span>
        
        </span><span><span class="hljs-comment">// Parse the PDF file</span></span><span>
        </span><span><span class="hljs-keyword">const</span></span><span> buffer = </span><span><span class="hljs-keyword">await</span></span><span> file.</span><span><span class="hljs-title function_">arrayBuffer</span></span><span>();
        </span><span><span class="hljs-keyword">const</span></span><span> data = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">pdfParse</span></span><span>(</span><span><span class="hljs-title class_">Buffer</span></span><span>.</span><span><span class="hljs-title function_">from</span></span><span>(buffer));
        </span><span><span class="hljs-keyword">const</span></span><span> extractedText = data.</span><span><span class="hljs-property">text</span></span><span>;
        
        </span><span><span class="hljs-comment">// Custom parsing logic (example using regex or string splits)</span></span><span>
        </span><span><span class="hljs-keyword">const</span></span><span> parsedData = </span><span><span class="hljs-title function_">parseCourtCaseData</span></span><span>(extractedText);
        
        </span><span><span class="hljs-comment">// Update offender profile with parsed data</span></span><span>
        </span><span><span class="hljs-keyword">const</span></span><span> updatedProfile = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">updateOffenderProfile</span></span><span>(offenderId, parsedData);
        
        </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">success</span></span><span>: </span><span><span class="hljs-literal">true</span></span><span>, </span><span><span class="hljs-attr">profile</span></span><span>: updatedProfile });
      } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
        </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error parsing PDF:"</span></span><span>, error);
        </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">error</span></span><span>: </span><span><span class="hljs-string">"Failed to parse PDF"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
      }
    }
    
    </span><span><span class="hljs-comment">// Example parser function (you will need to customize based on your PDF format)</span></span><span>
    </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">parseCourtCaseData</span></span><span>(</span><span><span class="hljs-params">text: <span class="hljs-built_in">string</span></span></span><span>) {
      </span><span><span class="hljs-comment">// Use regex or string manipulation to extract fields</span></span><span>
      </span><span><span class="hljs-keyword">const</span></span><span> caseNumberMatch = text.</span><span><span class="hljs-title function_">match</span></span><span>(</span><span><span class="hljs-regexp">/Case Number:\s*(\S+)/</span></span><span>);
      </span><span><span class="hljs-keyword">const</span></span><span> caseNumber = caseNumberMatch ? caseNumberMatch[</span><span><span class="hljs-number">1</span></span><span>] : </span><span><span class="hljs-string">""</span></span><span>;
      </span><span><span class="hljs-comment">// Repeat for other fields...</span></span><span>
      </span><span><span class="hljs-keyword">return</span></span><span> { caseNumber };
    }
    </span></span></code></div></div>
    
    

### B. Text Parsing Endpoint for DOC Form Data

1.  **Endpoint:**  
    `POST /api/admin/documents/parse-text`  
    This endpoint accepts pasted text from the DOC form.
    
2.  **Parsing:**  
    Use custom logic to extract structured data from the text. Because the format is consistent, regular expressions can be very effective.
    
3.  **Example Code Snippet:**
    
    
    <div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// app/api/admin/documents/parse-text/route.ts</span></span><span>
    </span><span><span class="hljs-keyword">import</span></span><span> { </span><span><span class="hljs-title class_">NextRequest</span></span><span>, </span><span><span class="hljs-title class_">NextResponse</span></span><span> } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"next/server"</span></span><span>;
    </span><span><span class="hljs-keyword">import</span></span><span> { isAdminRequest } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/auth"</span></span><span>;
    </span><span><span class="hljs-keyword">import</span></span><span> { updateOffenderProfile } </span><span><span class="hljs-keyword">from</span></span><span> </span><span><span class="hljs-string">"@/lib/db/offenders"</span></span><span>;
    
    </span><span><span class="hljs-keyword">export</span></span><span> </span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">POST</span></span><span>(</span><span><span class="hljs-params">request: NextRequest</span></span><span>) {
      </span><span><span class="hljs-keyword">try</span></span><span> {
        </span><span><span class="hljs-keyword">if</span></span><span> (!(</span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">isAdminRequest</span></span><span>(request))) {
          </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">error</span></span><span>: </span><span><span class="hljs-string">"Unauthorized"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">401</span></span><span> });
        }
        </span><span><span class="hljs-keyword">const</span></span><span> { offenderId, formText } = </span><span><span class="hljs-keyword">await</span></span><span> request.</span><span><span class="hljs-title function_">json</span></span><span>();
        </span><span><span class="hljs-keyword">if</span></span><span> (!offenderId || !formText) {
          </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">error</span></span><span>: </span><span><span class="hljs-string">"Offender ID and form text are required"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">400</span></span><span> });
        }
        
        </span><span><span class="hljs-comment">// Custom text parsing logic:</span></span><span>
        </span><span><span class="hljs-keyword">const</span></span><span> parsedData = </span><span><span class="hljs-title function_">parseDOCFormData</span></span><span>(formText);
        
        </span><span><span class="hljs-comment">// Update offender profile with parsed data</span></span><span>
        </span><span><span class="hljs-keyword">const</span></span><span> updatedProfile = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">updateOffenderProfile</span></span><span>(offenderId, parsedData);
        
        </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">success</span></span><span>: </span><span><span class="hljs-literal">true</span></span><span>, </span><span><span class="hljs-attr">profile</span></span><span>: updatedProfile });
      } </span><span><span class="hljs-keyword">catch</span></span><span> (error) {
        </span><span><span class="hljs-variable language_">console</span></span><span>.</span><span><span class="hljs-title function_">error</span></span><span>(</span><span><span class="hljs-string">"Error parsing form text:"</span></span><span>, error);
        </span><span><span class="hljs-keyword">return</span></span><span> </span><span><span class="hljs-title class_">NextResponse</span></span><span>.</span><span><span class="hljs-title function_">json</span></span><span>({ </span><span><span class="hljs-attr">error</span></span><span>: </span><span><span class="hljs-string">"Failed to parse form text"</span></span><span> }, { </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-number">500</span></span><span> });
      }
    }
    
    </span><span><span class="hljs-comment">// Example parser function (customize according to your form format)</span></span><span>
    </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">parseDOCFormData</span></span><span>(</span><span><span class="hljs-params">text: <span class="hljs-built_in">string</span></span></span><span>) {
      </span><span><span class="hljs-keyword">const</span></span><span> nameMatch = text.</span><span><span class="hljs-title function_">match</span></span><span>(</span><span><span class="hljs-regexp">/Name:\s*(.+)/</span></span><span>);
      </span><span><span class="hljs-keyword">const</span></span><span> dobMatch = text.</span><span><span class="hljs-title function_">match</span></span><span>(</span><span><span class="hljs-regexp">/Date of Birth:\s*(\d{2}\/\d{2}\/\d{4})/</span></span><span>);
      </span><span><span class="hljs-keyword">const</span></span><span> name = nameMatch ? nameMatch[</span><span><span class="hljs-number">1</span></span><span>].</span><span><span class="hljs-title function_">trim</span></span><span>() : </span><span><span class="hljs-string">""</span></span><span>;
      </span><span><span class="hljs-keyword">const</span></span><span> dateOfBirth = dobMatch ? dobMatch[</span><span><span class="hljs-number">1</span></span><span>] : </span><span><span class="hljs-string">""</span></span><span>;
      </span><span><span class="hljs-comment">// Continue extracting other fields like height, eye color, etc.</span></span><span>
      </span><span><span class="hljs-keyword">return</span></span><span> { name, dateOfBirth };
    }
    </span></span></code></div></div>
    
    

### C. Sending a Notification to the Offender

Once you have updated the offender’s profile, you need to notify them that their profile is now ready. This happens by calling a separate API endpoint (or as part of the update process) that:

-   Updates the offender’s record to set `profileEnabled: true`.
-   Creates a new notification entry in your database indicating that the profile is now ready.
-   The offender will see this notification (or be redirected directly to their profile on the next login).

Example snippet integrated in your profile update:


<div class="contain-inline-size rounded-md border-[0.5px] border-token-border-medium relative bg-token-sidebar-surface-primary"><div class="flex items-center text-token-text-secondary px-4 py-2 text-xs font-sans justify-between h-9 bg-token-sidebar-surface-primary dark:bg-token-main-surface-secondary select-none rounded-t-[5px]">ts</div><div class="sticky top-9"><div class="absolute bottom-0 right-0 flex h-9 items-center pr-2"><div class="flex items-center rounded bg-token-sidebar-surface-primary px-2 font-sans text-xs text-token-text-secondary dark:bg-token-main-surface-secondary"><span class="" data-state="closed"><button class="flex gap-1 items-center select-none px-4 py-1" aria-label="Copy"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg" class="icon-xs"><path fill-rule="evenodd" clip-rule="evenodd" d="M7 5C7 3.34315 8.34315 2 10 2H19C20.6569 2 22 3.34315 22 5V14C22 15.6569 20.6569 17 19 17H17V19C17 20.6569 15.6569 22 14 22H5C3.34315 22 2 20.6569 2 19V10C2 8.34315 3.34315 7 5 7H7V5ZM9 7H14C15.6569 7 17 8.34315 17 10V15H19C19.5523 15 20 14.5523 20 14V5C20 4.44772 19.5523 4 19 4H10C9.44772 4 9 4.44772 9 5V7ZM5 9C4.44772 9 4 9.44772 4 10V19C4 19.5523 4.44772 20 5 20H14C14.5523 20 15 19.5523 15 19V10C15 9.44772 14.5523 9 14 9H5Z" fill="currentColor"></path></svg>Copy</button></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre language-ts"><span><span><span class="hljs-comment">// In your updateOffenderProfile function (pseudo-code)</span></span><span>
</span><span><span class="hljs-keyword">async</span></span><span> </span><span><span class="hljs-keyword">function</span></span><span> </span><span><span class="hljs-title function_">updateOffenderProfile</span></span><span>(</span><span><span class="hljs-params">offenderId: <span class="hljs-built_in">string</span></span></span><span>, parsedData: </span><span><span class="hljs-built_in">any</span></span><span>) {
  </span><span><span class="hljs-comment">// Update the offender's data in MongoDB with the parsedData</span></span><span>
  </span><span><span class="hljs-keyword">const</span></span><span> updatedProfile = </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">updateOffenderInDB</span></span><span>(offenderId, {
    ...parsedData,
    </span><span><span class="hljs-attr">profileEnabled</span></span><span>: </span><span><span class="hljs-literal">true</span></span><span>, </span><span><span class="hljs-comment">// Mark as active once fully updated</span></span><span>
  });
  </span><span><span class="hljs-comment">// Create a notification for the offender</span></span><span>
  </span><span><span class="hljs-keyword">await</span></span><span> </span><span><span class="hljs-title function_">storeNotification</span></span><span>({
    offenderId,
    </span><span><span class="hljs-attr">title</span></span><span>: </span><span><span class="hljs-string">"Profile Ready"</span></span><span>,
    </span><span><span class="hljs-attr">message</span></span><span>: </span><span><span class="hljs-string">"Your profile has been updated and is now ready for viewing."</span></span><span>,
    </span><span><span class="hljs-attr">type</span></span><span>: </span><span><span class="hljs-string">"system"</span></span><span>,
    </span><span><span class="hljs-attr">status</span></span><span>: </span><span><span class="hljs-string">"unread"</span></span><span>,
    </span><span><span class="hljs-attr">createdAt</span></span><span>: </span><span><span class="hljs-keyword">new</span></span><span> </span><span><span class="hljs-title class_">Date</span></span><span>().</span><span><span class="hljs-title function_">toISOString</span></span><span>(),
  });
  </span><span><span class="hljs-keyword">return</span></span><span> updatedProfile;
}
</span></span></code></div></div>


___

## 3\. UI Integration

### Admin Dashboard

-   **Document Parsing Tab:**  
    Create a tab or section on your admin dashboard for document parsing.
    -   **File Upload Button:**  
        Opens a dialog to select PDF files. On selection, the file is sent to `/api/admin/documents/upload-and-parse`.
    -   **Text Input Area:**  
        Provides a textarea to paste in form data. On submission, the text is sent to `/api/admin/documents/parse-text`.
    -   **Result Preview:**  
        After parsing, display the extracted fields so you can review them before updating the profile.

### Offender Notification and Profile Redirection

-   **Toast Notifications:**  
    Use your Toast component (as part of your UI library) to show immediate feedback like “Profile updated and ready for viewing.”
-   **Session Management:**  
    Once the offender logs in again, check their profile status. If `profileEnabled: true`, redirect them directly to their profile page.

___

## 4\. Putting It All Together

### Vocabulary Recap for Your Application:

-   **Offender (User):**  
    The individual who logs in using their inmate number.
-   **Admin:**  
    You, who reviews new registrations, parses documents, and updates offender profiles.
-   **Profile:**  
    The detailed record of an offender’s personal and court case information.
-   **Dashboard:**  
    The admin interface where you can view notifications, parse documents, and manage data.
-   **Notification:**  
    A persistent record stored in MongoDB to alert either the admin (new registrations) or the offender (profile ready).

### Summary of Steps:

1.  **New Offender Logs In:**  
    Zod validates the inmate number. If it’s new, create a record and store a notification.
2.  **Admin Reviews Notification:**  
    Through the admin dashboard, you upload and parse PDFs or paste text to extract profile data.
3.  **Profile Update:**  
    The extracted data is used to update the offender’s profile in MongoDB.
4.  **Offender Notification:**  
    A notification is created and sent to the offender, updating their status to active.
5.  **Next Login:**  
    The offender, now with an active profile, is taken directly to their profile.

___

## Final Thoughts

By combining a file upload mechanism with PDF parsing (using packages like **pdf-parse**) and custom text parsing logic, you can automate much of the tedious manual data entry. Your API endpoints in Next.js 15 with the new App Router handle these tasks, and the notifications system bridges the admin and offender experiences. This setup leverages TypeScript for type safety, React 19 for a modern UI, and MongoDB for persistent storage.

This overall approach keeps your system simple, ensuring that offenders log in with just their inmate number, while you—the admin—get notified, update profiles, and eventually send back a notification that their profile is ready for use.

Feel free to ask any follow-up questions or request further details on any specific part of this workflow!