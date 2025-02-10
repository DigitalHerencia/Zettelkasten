---
id: 459f693osnd6ddwkmcqnqbq
title: dropzonejs
desc: ''
updated: 1733340517745
created: 1733340493078
---

### Lesson 10: **Drag-and-Drop File Uploads with Dropzone.js**

*(Easily integrate drag-and-drop file uploads into your app.)*

* * *

#### What is Dropzone.js?

- **Definition**: A lightweight library for building drag-and-drop file upload functionality.
- **Why Use Dropzone.js?**
    - Simplifies file uploads with drag-and-drop UI.
    - Provides built-in preview handling.
    - Highly customizable for specific use cases.

* * *

#### Installing Dropzone.js

1. Install the Dropzone.js library:

        bashCopy codenpm install dropzone
2. **Optional**: Install a React wrapper for easier integration:

        bashCopy codenpm install react-dropzone

* * *

### Example: Basic Drag-and-Drop Upload

1. **Using React-Dropzone**:

    - Create a new file `components/FileUpload.js`:

            javascriptCopy codeimport { useState } from 'react';import { useDropzone } from 'react-dropzone'; export default function FileUpload() { const [files, setFiles] = useState([]); const onDrop = (acceptedFiles) => { setFiles( acceptedFiles.map((file) => Object.assign(file, { preview: URL.createObjectURL(file), }) ) ); }; const { getRootProps, getInputProps } = useDropzone({ onDrop }); return ( <div {...getRootProps()} className="p-6 border-2 border-dashed rounded-md bg-gray-50 text-center" > <input {...getInputProps()} /> <p className="text-gray-500"> Drag and drop files here, or click to select files. </p> <div className="mt-4 grid grid-cols-3 gap-4"> {files.map((file) => ( <div key={file.name} className="flex flex-col items-center"> <img src={file.preview} alt={file.name} className="w-24 h-24 object-cover rounded" /> <p className="mt-2 text-sm">{file.name}</p> </div> ))} </div> </div> );}
2. **Add the Component to a Page**:

    - Update `pages/index.js`:

            javascriptCopy codeimport FileUpload from '@/components/FileUpload'; export default function Home() { return ( <div className="min-h-screen flex flex-col items-center justify-center bg-gray-100"> <h1 className="text-2xl font-bold mb-4">Upload Your Files</h1> <FileUpload /> </div> );}

* * *

### Explanation of Key Features

| Feature | Description |
| --- | --- |
| **`useDropzone`** | Hook that manages file selection and drop interactions. |
| **`getRootProps`** | Used to bind drag-and-drop behavior to a container. |
| **`getInputProps`** | Applies necessary props to the hidden file input field. |
| **`acceptedFiles`** | Array of files selected or dropped into the area. |

* * *

### Adding File Upload to a Backend

1. **Sending Files to a Server**:

    - Modify `onDrop` to include a POST request:

            javascriptCopy codeconst onDrop = (acceptedFiles) => { const formData = new FormData(); acceptedFiles.forEach((file) => formData.append('files', file)); fetch('/api/upload', { method: 'POST', body: formData, }) .then((res) => res.json()) .then((data) => console.log(data));};
2. **Sample Backend Route** (Next.js API):

    - Create a new file `pages/api/upload.js`:

            javascriptCopy codeexport default function handler(req, res) { if (req.method === 'POST') { // Handle file upload (e.g., save to server or cloud storage) res.status(200).json({ message: 'Files uploaded successfully!' }); } else { res.status(405).json({ message: 'Method not allowed' }); }}

* * *

### Styling with Shadcn

1. Wrap the drag-and-drop area with a **Card Component**:

        javascriptCopy codeimport { Card, CardHeader, CardBody } from 'shadcn/ui'; export default function StyledFileUpload() { return ( <Card className="w-full max-w-lg mx-auto"> <CardHeader> <h2 className="text-xl font-bold">File Upload</h2> </CardHeader> <CardBody> <FileUpload /> </CardBody> </Card> );}

* * *

### Practice Task

1. **Challenge**: Add file type and size restrictions:
    - Accept only images (`image/jpeg`, `image/png`).
    - Limit file size to 2MB.
2. **Bonus**: Display an error message for invalid files.

* * *

### Advanced Features

1. **Progress Bar for Uploads**:
    - Add a progress bar to show upload progress using the `onUploadProgress` event in Axios or Fetch.
2. **Cloud Storage Integration**:
    - Use services like AWS S3, Firebase, or Cloudinary for file storage.

* * *

### Resources

- Dropzone.js Docs
- Using Dropzone with Next.js
- Learn interactively: [Drag-and-Drop Upload Tutorial](https://www.youtube.com/watch?v=YVqMUE8ZzPE)