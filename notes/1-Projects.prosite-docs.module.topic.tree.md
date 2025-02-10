---
id: 94ekeac2bhd26xadm9xywh7
title: tree
desc: ''
updated: 1729322157316
created: 1729322157316
---


### Directory Structure

```bash
ProSiteDocs/
│
├── backend/
│   ├── api/
│   │   ├── controllers/
│   │   ├── models/
│   │   ├── routes/
│   │   ├── services/
│   ├── config/
│   ├── db/
│   ├── middlewares/
│   ├── tests/
│   ├── package.json
│   └── server.js
│
├── frontend/
│   ├── mobile/
│   │   ├── src/
│   │   │   ├── components/
│   │   │   ├── screens/
│   │   │   ├── services/
│   │   │   └── App.js
│   │   ├── android/
│   │   ├── ios/
│   │   ├── package.json
│   │   └── index.js
│   ├── web/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── package.json
│   │   └── next.config.js
│
├── infra/
│   ├── aws/
│   │   ├── s3/
│   │   ├── lambda/
│   │   ├── cloudformation/
│   └── ci-cd/
│       ├── github-actions/
│       ├── codepipeline/
│
├── docs/
│   ├── project-plan.md
│   ├── requirements.md
│   ├── design.md
│   ├── test-plan.md
│   ├── deployment-plan.md
│   └── security-plan.md
│
└── scripts/
    ├── data-seeding/
    ├── deployment/
    └── backup/
```

### Backend Initial Setup (Node.js with Express and AWS S3)

In the `backend/server.js`, we set up the API and include basic services like photo upload and S3 integration.

```javascript
// backend/server.js
const express = require('express');
const AWS = require('aws-sdk');
const multer = require('multer');
const bodyParser = require('body-parser');
const { v4: uuidv4 } = require('uuid');
const app = express();

// Load environment variables
require('dotenv').config();

// Configure S3
const s3 = new AWS.S3({
    accessKeyId: process.env.AWS_ACCESS_KEY_ID,
    secretAccessKey: process.env.AWS_SECRET_ACCESS_KEY,
    region: process.env.AWS_REGION
});

// Multer setup for file uploads
const storage = multer.memoryStorage();
const upload = multer({ storage: storage });

app.use(bodyParser.json());

// Upload photo route
app.post('/upload', upload.single('photo'), (req, res) => {
    const { projectName, metadata } = req.body;
    const file = req.file;
    const key = `${projectName}/${uuidv4()}-${file.originalname}`;

    const params = {
        Bucket: process.env.S3_BUCKET_NAME,
        Key: key,
        Body: file.buffer,
        ContentType: file.mimetype,
        Metadata: { metadata }
    };

    s3.upload(params, (err, data) => {
        if (err) {
            return res.status(500).json({ error: "Failed to upload file." });
        }
        res.status(200).json({ message: "File uploaded successfully!", url: data.Location });
    });
});

// Start server
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```

### Frontend Mobile (React Native Basic Setup)

In the `frontend/mobile/src/screens/UploadScreen.js`, we build a simple photo upload screen with React Native.

```javascript
// frontend/mobile/src/screens/UploadScreen.js
import React, { useState } from 'react';
import { View, Button, Text, Image, Platform } from 'react-native';
import * as ImagePicker from 'expo-image-picker';
import axios from 'axios';

export default function UploadScreen() {
    const [image, setImage] = useState(null);

    const pickImage = async () => {
        let result = await ImagePicker.launchImageLibraryAsync({
            mediaTypes: ImagePicker.MediaTypeOptions.Images,
            allowsEditing: true,
            quality: 1,
        });

        if (!result.canceled) {
            setImage(result.uri);
        }
    };

    const uploadImage = async () => {
        const formData = new FormData();
        formData.append('photo', {
            uri: image,
            type: 'image/jpeg',
            name: `photo_${Date.now()}.jpg`,
        });
        formData.append('projectName', 'SampleProject');

        try {
            const response = await axios.post('http://localhost:3000/upload', formData, {
                headers: {
                    'Content-Type': 'multipart/form-data',
                },
            });
            alert('Photo uploaded successfully!');
        } catch (err) {
            console.error(err);
            alert('Failed to upload photo.');
        }
    };

    return (
        <View>
            <Button title="Pick an image" onPress={pickImage} />
            {image && <Image source={{ uri: image }} style={{ width: 200, height: 200 }} />}
            <Button title="Upload Image" onPress={uploadImage} />
        </View>
    );
}
```

### AWS Infrastructure Setup (CloudFormation for S3 Bucket and IAM Policies)

In `infra/aws/cloudformation/s3-bucket.yaml`, we define a CloudFormation template to create the S3 bucket and assign necessary policies.

```yaml
Resources:
  ProSiteDocsBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: prosite-docs-${AWS::AccountId}
      VersioningConfiguration:
        Status: Enabled

  BucketPolicy:
    Type: AWS::S3::BucketPolicy
    Properties:
      Bucket: !Ref ProSiteDocsBucket
      PolicyDocument:
        Statement:
          - Effect: Allow
            Principal: '*'
            Action:
              - s3:GetObject
              - s3:PutObject
            Resource: !Sub "arn:aws:s3:::prosite-docs-${AWS::AccountId}/*"
```

### Security Configuration (AWS KMS and IAM Roles)

You can add a KMS configuration to ensure that all photos are encrypted at rest, and you can use IAM roles to restrict access to only the authorized services. These would be managed within the AWS console or added to the CloudFormation templates.

### CI/CD Setup (GitHub Actions for Continuous Integration)

In `infra/ci-cd/github-actions/deploy.yml`, set up GitHub Actions to automate deployment to AWS.

```yaml
name: Deploy to AWS

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      
      - name: Set up Node.js
        uses: actions/setup-node@v1
        with:
          node-version: '14'
      
      - name: Install dependencies
        run: npm install
      
      - name: Deploy to AWS
        run: |
          aws s3 sync ./build s3://${{ secrets.S3_BUCKET_NAME }}
          aws cloudfront create-invalidation --distribution-id ${{ secrets.CLOUDFRONT_ID }} --paths "/*"
```