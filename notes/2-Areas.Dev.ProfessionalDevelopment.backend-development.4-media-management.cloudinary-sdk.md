---
id: 8ku0c8wg4q60qloaz589qru
title: cloudinary-sdk
desc: ''
updated: 1733340985328
created: 1733340955278
---

### Lesson 16: **Media Management with Cloudinary SDK**

*(Efficiently store, optimize, and deliver images, videos, and other media in your Next.js app.)*

* * *

#### What is Cloudinary?

- **Definition**: A cloud-based service for managing and optimizing media assets such as images and videos.
- **Key Features**:
    - Media storage and delivery via a global CDN.
    - Automatic image and video optimization.
    - On-the-fly transformations (resizing, cropping, watermarking, etc.).
    - AI-powered features like background removal and auto-tagging.

* * *

#### Why Use Cloudinary?

| Feature | Benefit |
| --- | --- |
| **Performance** | Faster loading with automatic optimization. |
| **Flexibility** | On-the-fly transformations via URL parameters. |
| **Global CDN** | Deliver assets quickly worldwide. |
| **Seamless Integration** | SDKs for JavaScript, Node.js, React, and more. |

* * *

### Step 1: Set Up Cloudinary

1. **Create a Cloudinary Account**:

    - Sign up at [Cloudinary](https://cloudinary.com/).
2. **Get Your Cloud Name and API Credentials**:

    - In the Cloudinary Dashboard, find your **Cloud Name**, **API Key**, and **API Secret**.
3. **Install the Cloudinary Node.js SDK**:

        bashCopy codenpm install cloudinary

* * *

### Step 2: Configure Cloudinary in Your App

1. **Set Up Cloudinary Configuration**:

    - Create a file `lib/cloudinary.js`:

            javascriptCopy codeimport { v2 as cloudinary } from 'cloudinary'; cloudinary.config({ cloud_name: process.env.CLOUDINARY_CLOUD_NAME, api_key: process.env.CLOUDINARY_API_KEY, api_secret: process.env.CLOUDINARY_API_SECRET,}); export default cloudinary;
2. **Add Environment Variables**:

    - Add the following to `.env.local`:

            plaintextCopy codeCLOUDINARY_CLOUD_NAME=your_cloud_nameCLOUDINARY_API_KEY=your_api_keyCLOUDINARY_API_SECRET=your_api_secret

* * *

### Step 3: Upload Media to Cloudinary

1. **Create an API Route for Uploads**:

    - Add a file `pages/api/upload.js`:

            javascriptCopy codeimport cloudinary from '@/lib/cloudinary'; export default async function handler(req, res) { if (req.method === 'POST') { const { file } = req.body; try { const uploadResponse = await cloudinary.uploader.upload(file, { folder: 'uploads', }); res.status(200).json({ url: uploadResponse.secure_url }); } catch (error) { console.error(error); res.status(500).json({ error: 'Upload failed' }); } } else { res.setHeader('Allow', ['POST']); res.status(405).end(`Method ${req.method} Not Allowed`); }}
2. **Use the API in Your Frontend**:

    - Create a file upload form in `pages/index.js`:

            javascriptCopy codeimport { useState } from 'react'; export default function Home() { const [file, setFile] = useState(null); const [url, setUrl] = useState(''); const handleFileChange = (e) => { setFile(e.target.files[0]); }; const handleUpload = async () => { const formData = new FormData(); formData.append('file', file); const res = await fetch('/api/upload', { method: 'POST', body: formData, }); const data = await res.json(); setUrl(data.url); }; return ( <div className="min-h-screen p-6 bg-gray-100"> <h1 className="text-3xl font-bold">Upload Media</h1> <input type="file" onChange={handleFileChange} /> <button onClick={handleUpload} className="px-4 py-2 mt-4 bg-blue-500 text-white rounded hover:bg-blue-600" > Upload </button> {url && ( <div className="mt-4"> <h2 className="text-xl">Uploaded File:</h2> <img src={url} alt="Uploaded File" className="max-w-sm" /> </div> )} </div> );}

* * *

### Step 4: Apply Transformations

1. **Transform Images**:

    - Use URL-based transformations:

            javascriptCopy codeconst optimizedUrl = cloudinary.url('uploads/example.jpg', { width: 300, height: 300, crop: 'fill',});
2. **Example Transformation**:

    - Resize to 300x300 and apply a circular crop:

            javascriptCopy codeconst transformedUrl = cloudinary.url('uploads/example.jpg', { width: 300, height: 300, crop: 'thumb', gravity: 'face', radius: 'max',});

* * *

### Advanced Features

#### Real-Time Video Optimization

1. **Deliver Optimized Videos**:

    - Example: Stream a 720p version of a video:

            javascriptCopy codeconst videoUrl = cloudinary.video('uploads/example.mp4', { transformation: [ { width: 1280, crop: 'scale' }, { format: 'mp4' }, ],});
2. **Embed in Frontend**:

        jsxCopy code<video controls> <source src={videoUrl} type="video/mp4" /></video>

* * *

#### Practice Task

1. **Challenge**: Build a gallery page that:
    - Fetches and displays all media files in a folder.
    - Allows users to click on an image to see its larger version.
2. **Bonus**: Add a button to delete an uploaded image using the `cloudinary.api.delete_resources` method.

* * *

### Additional Features

1. **Watermarking**:

    - Add watermarks dynamically using transformations.

        javascriptCopy codecloudinary.url('uploads/example.jpg', { overlay: 'your_watermark', gravity: 'south_east', x: 10, y: 10,});
2. **AI-Powered Features**:

    - Auto-tagging and background removal:

        javascriptCopy codeconst uploadResponse = await cloudinary.uploader.upload(file, { categorization: 'google_tagging', auto_tagging: 0.8,});

* * *

### Resources

- Cloudinary Documentation
- [Next.js + Cloudinary Example](https://github.com/cloudinary-devs/nextjs-cloudinary-example)
- Learn interactively: [Cloudinary Media Management](https://www.youtube.com/watch?v=lyGZbp0N-G4)