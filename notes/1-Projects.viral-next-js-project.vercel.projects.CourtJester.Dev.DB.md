---
id: 7pz2nacpynhcldm9l4lrt48
title: DB
desc: ''
updated: 1742100159709
created: 1742099343851
---
# MongoDB Transition Guide

To transition from Vercel Blob storage to MongoDB, you'll need to:

## 1. Setup MongoDB Connection

1. **Install MongoDB Dependencies**:

```shellscript
npm install mongodb mongoose
```

2. **Create MongoDB Connection Utility**:

Create a new file `lib/db/mongodb.ts`:

```typescript
import mongoose from 'mongoose';

const MONGODB_URI = process.env.MONGODB_URI;

if (!MONGODB_URI) {
  throw new Error('Please define the MONGODB_URI environment variable');
}

let cached = global.mongoose;

if (!cached) {
  cached = global.mongoose = { conn: null, promise: null };
}

async function connectToDatabase() {
  if (cached.conn) {
    return cached.conn;
  }

  if (!cached.promise) {
    cached.promise = mongoose.connect(MONGODB_URI).then((mongoose) => {
      return mongoose;
    });
  }
  cached.conn = await cached.promise;
  return cached.conn;
}

export default connectToDatabase;
```

## 2. Create MongoDB Schemas

Replace `lib/db/models.ts` with MongoDB schemas:

```typescript
import mongoose from 'mongoose';

// Offender Schema
const OffenderSchema = new mongoose.Schema({
  inmateNumber: { type: String, required: true, unique: true },
  inmateType: { type: String, required: true },
  name: String,
  status: String,
  facility: String,
  profileEnabled: { type: Boolean, default: false },
  motionsEnabled: { type: Boolean, default: false },
  notificationsEnabled: { type: Boolean, default: false },
}, { timestamps: true });

// Case Schema
const CaseSchema = new mongoose.Schema({
  offenderId: { type: mongoose.Schema.Types.ObjectId, ref: 'Offender', required: true },
  caseNumber: { type: String, required: true },
  court: String,
  judge: String,
  filingDate: String,
  charges: [{
    description: String,
    disposition: String,
    dispositionDate: String
  }],
  hearings: [{
    type: String,
    date: String,
    time: String,
    location: String,
    judge: String
  }]
}, { timestamps: true });

// Motion Schema
const MotionSchema = new mongoose.Schema({
  offenderId: { type: mongoose.Schema.Types.ObjectId, ref: 'Offender', required: true },
  caseId: { type: mongoose.Schema.Types.ObjectId, ref: 'Case', required: true },
  templateId: { type: String, required: true },
  title: { type: String, required: true },
  content: { type: String, required: true },
  variables: { type: Map, of: String },
  status: { type: String, enum: ['draft', 'completed', 'filed', 'deleted'], default: 'draft' }
}, { timestamps: true });

// Notification Schema
const NotificationSchema = new mongoose.Schema({
  offenderId: { type: mongoose.Schema.Types.ObjectId, ref: 'Offender' },
  caseId: { type: mongoose.Schema.Types.ObjectId, ref: 'Case' },
  title: { type: String, required: true },
  message: { type: String, required: true },
  type: { type: String, enum: ['system', 'hearing', 'motion', 'case'], default: 'system' },
  status: { type: String, enum: ['unread', 'read'], default: 'unread' }
}, { timestamps: true });

// Reminder Schema
const ReminderSchema = new mongoose.Schema({
  offenderId: { type: mongoose.Schema.Types.ObjectId, ref: 'Offender', required: true },
  title: { type: String, required: true },
  message: { type: String, required: true },
  scheduledFor: { type: Date, required: true },
  status: { type: String, enum: ['pending', 'sent', 'cancelled'], default: 'pending' },
  caseId: { type: mongoose.Schema.Types.ObjectId, ref: 'Case' },
  hearingId: String,
  motionId: { type: mongoose.Schema.Types.ObjectId, ref: 'Motion' },
  recurring: {
    frequency: { type: String, enum: ['daily', 'weekly', 'monthly'] },
    endDate: Date
  },
  createdBy: { type: String, enum: ['admin', 'offender'], required: true }
}, { timestamps: true });

// Session Schema
const SessionSchema = new mongoose.Schema({
  sessionId: { type: String, required: true, unique: true },
  inmateNumber: { type: String, required: true },
  role: { type: String, enum: ['admin', 'offender'], required: true },
  language: { type: String, enum: ['en', 'es'], default: 'es' },
  expiresAt: { type: Date, required: true }
}, { timestamps: true });

// Create models
export const Offender = mongoose.models.Offender || mongoose.model('Offender', OffenderSchema);
export const Case = mongoose.models.Case || mongoose.model('Case', CaseSchema);
export const Motion = mongoose.models.Motion || mongoose.model('Motion', MotionSchema);
export const Notification = mongoose.models.Notification || mongoose.model('Notification', NotificationSchema);
export const Reminder = mongoose.models.Reminder || mongoose.model('Reminder', ReminderSchema);
export const Session = mongoose.models.Session || mongoose.model('Session', SessionSchema);
```

## 3. Replace Blob Storage Functions

Create a new file `lib/db/mongodb-storage.ts` to replace `lib/db/blob-storage.ts`:

```typescript
import connectToDatabase from './mongodb';
import { Offender, Case, Motion, Notification, Reminder, Session } from './models';
import mongoose from 'mongoose';

// Helper function to convert MongoDB _id to string id
const formatDocument = (doc) => {
  const formatted = doc.toObject();
  formatted._id = formatted._id.toString();
  return formatted;
};

// Offender functions
export async function storeOffender(offenderData) {
  await connectToDatabase();
  const offender = new Offender(offenderData);
  await offender.save();
  return offender._id.toString();
}

export async function getOffenderById(id) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(id)) return null;
  const offender = await Offender.findById(id);
  return offender ? formatDocument(offender) : null;
}

export async function getOffenderByInmateNumber(inmateNumber) {
  await connectToDatabase();
  const offender = await Offender.findOne({ inmateNumber });
  return offender ? formatDocument(offender) : null;
}

export async function listOffenders() {
  await connectToDatabase();
  const offenders = await Offender.find();
  return offenders.map(formatDocument);
}

export async function updateOffender(id, updates) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(id)) return null;
  const offender = await Offender.findByIdAndUpdate(id, updates, { new: true });
  return offender ? formatDocument(offender) : null;
}

export async function deleteOffender(id) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(id)) return false;
  const result = await Offender.deleteOne({ _id: id });
  return result.deletedCount > 0;
}

// Case functions
export async function storeCase(caseData) {
  await connectToDatabase();
  const newCase = new Case(caseData);
  await newCase.save();
  return newCase._id.toString();
}

export async function getCaseById(id) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(id)) return null;
  const caseDoc = await Case.findById(id);
  return caseDoc ? formatDocument(caseDoc) : null;
}

export async function listCases() {
  await connectToDatabase();
  const cases = await Case.find();
  return cases.map(formatDocument);
}

export async function listCasesByOffenderId(offenderId) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(offenderId)) return [];
  const cases = await Case.find({ offenderId });
  return cases.map(formatDocument);
}

export async function updateCase(id, updates) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(id)) return null;
  const caseDoc = await Case.findByIdAndUpdate(id, updates, { new: true });
  return caseDoc ? formatDocument(caseDoc) : null;
}

export async function deleteCase(id) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(id)) return false;
  const result = await Case.deleteOne({ _id: id });
  return result.deletedCount > 0;
}

// Motion functions
export async function storeMotion(motionData) {
  await connectToDatabase();
  const motion = new Motion(motionData);
  await motion.save();
  return motion._id.toString();
}

export async function getMotionById(id) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(id)) return null;
  const motion = await Motion.findById(id);
  return motion ? formatDocument(motion) : null;
}

export async function listMotions() {
  await connectToDatabase();
  const motions = await Motion.find();
  return motions.map(formatDocument);
}

export async function listMotionsByOffenderId(offenderId) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(offenderId)) return [];
  const motions = await Motion.find({ offenderId });
  return motions.map(formatDocument);
}

export async function listMotionsByCaseId(caseId) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(caseId)) return [];
  const motions = await Motion.find({ caseId });
  return motions.map(formatDocument);
}

export async function updateMotion(id, updates) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(id)) return null;
  const motion = await Motion.findByIdAndUpdate(id, updates, { new: true });
  return motion ? formatDocument(motion) : null;
}

export async function deleteMotion(id) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(id)) return false;
  const result = await Motion.deleteOne({ _id: id });
  return result.deletedCount > 0;
}

// Notification functions
export async function storeNotification(notificationData) {
  await connectToDatabase();
  const notification = new Notification(notificationData);
  await notification.save();
  return notification._id.toString();
}

export async function getNotificationById(id) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(id)) return null;
  const notification = await Notification.findById(id);
  return notification ? formatDocument(notification) : null;
}

export async function listNotifications() {
  await connectToDatabase();
  const notifications = await Notification.find();
  return notifications.map(formatDocument);
}

export async function listNotificationsByOffenderId(offenderId) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(offenderId)) return [];
  const notifications = await Notification.find({
    $or: [
      { offenderId },
      { offenderId: null }
    ]
  });
  return notifications.map(formatDocument);
}

export async function updateNotification(id, updates) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(id)) return null;
  const notification = await Notification.findByIdAndUpdate(id, updates, { new: true });
  return notification ? formatDocument(notification) : null;
}

export async function deleteNotification(id) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(id)) return false;
  const result = await Notification.deleteOne({ _id: id });
  return result.deletedCount > 0;
}

// Reminder functions
export async function storeReminder(reminderData) {
  await connectToDatabase();
  const reminder = new Reminder(reminderData);
  await reminder.save();
  return reminder._id.toString();
}

export async function getReminderById(id) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(id)) return null;
  const reminder = await Reminder.findById(id);
  return reminder ? formatDocument(reminder) : null;
}

export async function listReminders() {
  await connectToDatabase();
  const reminders = await Reminder.find();
  return reminders.map(formatDocument);
}

export async function listRemindersByOffenderId(offenderId) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(offenderId)) return [];
  const reminders = await Reminder.find({ offenderId });
  return reminders.map(formatDocument);
}

export async function listDueReminders() {
  await connectToDatabase();
  const now = new Date();
  const reminders = await Reminder.find({
    status: 'pending',
    scheduledFor: { $lte: now }
  });
  return reminders.map(formatDocument);
}

export async function updateReminder(id, updates) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(id)) return null;
  const reminder = await Reminder.findByIdAndUpdate(id, updates, { new: true });
  return reminder ? formatDocument(reminder) : null;
}

export async function deleteReminder(id) {
  await connectToDatabase();
  if (!mongoose.Types.ObjectId.isValid(id)) return false;
  const result = await Reminder.deleteOne({ _id: id });
  return result.deletedCount > 0;
}

// Session functions
export async function storeSession(sessionData) {
  await connectToDatabase();
  const session = new Session(sessionData);
  await session.save();
  return session.sessionId;
}

export async function getSessionById(id) {
  await connectToDatabase();
  const session = await Session.findOne({ sessionId: id });
  return session ? formatDocument(session) : null;
}

export async function deleteSession(id) {
  await connectToDatabase();
  const result = await Session.deleteOne({ sessionId: id });
  return result.deletedCount > 0;
}

// Generate a unique ID (for compatibility with existing code)
export function generateId() {
  return new mongoose.Types.ObjectId().toString();
}
```

## 4. Update Environment Variables

Add the following to your `.env` file:

```plaintext
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/court-jester?retryWrites=true&w=majority
```

## 5. Update Import Statements

Update all import statements in the codebase that reference `lib/db/blob-storage.ts` to use the new MongoDB functions.

## Data Models and Storage

### Data Models

1. **Offender**

1. `_id`: string
2. `inmateNumber`: string
3. `inmateType`: string
4. `name`: string (optional)
5. `status`: string (optional)
6. `facility`: string (optional)
7. `createdAt`: string
8. `updatedAt`: string
9. `profileEnabled`: boolean (optional)
10. `motionsEnabled`: boolean (optional)
11. `notificationsEnabled`: boolean (optional)

2. **Case**

1. `_id`: string
2. `offenderId`: string
3. `caseNumber`: string
4. `court`: string
5. `judge`: string
6. `filingDate`: string
7. `charges`: Array of Charge
8. `hearings`: Array of Hearing
9. `createdAt`: string
10. `updatedAt`: string

3. **Charge**

1. `description`: string
2. `disposition`: string (optional)
3. `dispositionDate`: string (optional)

4. **Hearing**

1. `type`: string
2. `date`: string
3. `time`: string
4. `location`: string (optional)
5. `judge`: string (optional)

5. **Motion**

1. `_id`: string
2. `offenderId`: string
3. `caseId`: string
4. `templateId`: string
5. `title`: string
6. `content`: string
7. `variables`: Record<string, string>
8. `status`: "draft" | "completed" | "filed" | "deleted"
9. `createdAt`: string
10. `updatedAt`: string

6. **Notification**

1. `_id`: string
2. `offenderId`: string | null
3. `caseId`: string (optional)
4. `title`: string
5. `message`: string
6. `type`: "system" | "hearing" | "motion" | "case"
7. `status`: "unread" | "read"
8. `createdAt`: string
9. `updatedAt`: string (optional)

7. **Reminder**

1. `_id`: string
2. `offenderId`: string
3. `title`: string
4. `message`: string
5. `scheduledFor`: string
6. `status`: "pending" | "sent" | "cancelled"
7. `caseId`: string (optional)
8. `hearingId`: string (optional)
9. `motionId`: string (optional)
10. `recurring`: {

1. `frequency`: "daily" | "weekly" | "monthly"
2. `endDate`: string (optional)
} (optional)

11. `createdAt`: string
12. `updatedAt`: string
13. `createdBy`: "admin" | "offender"

8. **Session**

1. `sessionId`: string
2. `inmateNumber`: string
3. `role`: "admin" | "offender"
4. `language`: "en" | "es"
5. `createdAt`: string

### Storage Mechanisms

1. **Vercel Blob Storage**:

1. Used for storing all data models
2. Implemented in `lib/db/blob-storage.ts`
3. Uses JSON files with prefixes for different data types



2. **Local Storage**:

1. Used for storing language preference (`gringoMode`)
2. Implemented in `app/page.tsx`



3. **Cookies**:

1. Used for storing session ID
2. Implemented in `app/api/auth/login/route.ts`



4. **File System**:

1. Used for storing help content (HELP.md)
2. Implemented in `app/api/help-content/route.ts`



