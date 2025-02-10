---
id: 3ffrnnnv5gmnaz1eujjyvrc
title: DataModeling
desc: ''
updated: 1733455737999
created: 1733453762541
---

# Data Modeling for a Next.js MongoDB Web App
#### React 19 | TypeScript | Prisma | Auth0 

___

This data model is designed for an OnlyFans Management Agency app with dashboards for Admin, Creators, and Fans. It supports:

- **Content Uploads:** Images, videos, and posts.
- **Fan Engagement:** Comments, likes, subscriptions.
- **Metrics**: Analytics for performance tracking.
- **Admin Communication:** Coaching creators and gathering feedback from fans.

## Core Entities and Relationships

### 1. User Model

**Purpose:** Represents all users (Admin, Creators, Fans).

**Roles:** Differentiates between Admin, Creator, and Fan.

#### Key Relationships:

- Creators manage posts and fans.
- Admins oversee creators and provide feedback.
- Fans subscribe to creators and interact with their content.

```prisma
model User {
  id             String      @id @default(auto()) @map("_id") @db.ObjectId
  auth0Id        String      @unique // Auth0's user identifier
  name           String
  email          String      @unique
  profilePicture String?
  role           Role        @default(FAN) // FAN, CREATOR, ADMIN
  isActive       Boolean     @default(true)
  createdAt      DateTime    @default(now())
  updatedAt      DateTime    @updatedAt

  // Relationships
  posts          Post[]      // For creators
  subscriptions  Subscription[] // For fans
  messagesSent   Message[]   @relation("Sender")
  messagesReceived Message[] @relation("Receiver")
  comments       Comment[]   // For fans interacting with posts
}

enum Role {
  FAN
  CREATOR
  ADMIN
}

```

### 2. Post Model

**Purpose:** Represents content (photos, videos, text) uploaded by creators.

#### Key Features:

- Supports media uploads (via Cloudinary).
- Tracks likes, comments, and views for engagement metrics.

```prisma
model Post {
  id          String      @id @default(auto()) @map("_id") @db.ObjectId
  creatorId   String
  creator     User        @relation(fields: [creatorId], references: [id])
  title       String
  description String?
  mediaUrl    String      // Cloudinary URL
  mediaType   MediaType   // IMAGE, VIDEO, OTHER
  likes       Int         @default(0)
  views       Int         @default(0)
  isPublished Boolean     @default(true)
  createdAt   DateTime    @default(now())
  updatedAt   DateTime    @updatedAt

  // Relationships
  comments    Comment[]
}

enum MediaType {
  IMAGE
  VIDEO
  OTHER
}

```

### 3. Subscription Model

**Purpose:** Tracks fans subscribing to creators.

#### Key Features:

- Supports tiered subscriptions (e.g., basic, premium).
- Tracks the start and expiration of subscriptions.

```prisma
model Subscription {
  id          String      @id @default(auto()) @map("_id") @db.ObjectId
  fanId       String
  fan         User        @relation("FanSubscriptions", fields: [fanId], references: [id])
  creatorId   String
  creator     User        @relation("CreatorSubscribers", fields: [creatorId], references: [id])
  tier        SubscriptionTier
  startDate   DateTime    @default(now())
  endDate     DateTime
  isActive    Boolean     @default(true)
}

enum SubscriptionTier {
  BASIC
  PREMIUM
  VIP
}

```

### 4. Comment Model

**Purpose:** Allows fans to comment on creators' posts.

#### Key Features:

- Tracks which user made the comment.
- Supports nested replies.

```prisma
model Comment {
  id          String      @id @default(auto()) @map("_id") @db.ObjectId
  postId      String
  post        Post        @relation(fields: [postId], references: [id])
  userId      String
  user        User        @relation(fields: [userId], references: [id])
  content     String
  parentId    String?     // For replies
  createdAt   DateTime    @default(now())
}

```

### 5. Analytics Model

**Purpose:** Tracks engagement metrics for posts, creators, and fans.

#### Key Features:

- Provides detailed stats for admins and creators.

```prisma
model Analytics {
  id          String      @id @default(auto()) @map("_id") @db.ObjectId
  postId      String?
  post        Post?       @relation(fields: [postId], references: [id])
  creatorId   String?
  creator     User?       @relation(fields: [creatorId], references: [id])
  views       Int         @default(0)
  likes       Int         @default(0)
  comments    Int         @default(0)
  timestamp   DateTime    @default(now())
}

```

### 6. Message Model

**Purpose:** Facilitates admin-to-creator coaching and feedback from fans.

#### Key Features:

- Tracks sender, receiver, and message content.

```prisma
model Message {
  id          String      @id @default(auto()) @map("_id") @db.ObjectId
  senderId    String
  sender      User        @relation("Sender", fields: [senderId], references: [id])
  receiverId  String
  receiver    User        @relation("Receiver", fields: [receiverId], references: [id])
  content     String
  isRead      Boolean     @default(false)
  createdAt   DateTime    @default(now())
}

```

### Relationships Overview

Entity | Related Entities
-------|-----------------
User | Post, Subscription, Message, Comment
Post | User (Creator), Comment, Analytics
Subscription | User (Fan), User (Creator)
Comment | User, Post, Comment (Parent)
Analytics | Post, User (Creator)
Message | User (Sender), User (Receiver)

## Additional Features

### 1. Content Uploads (Cloudinary)

- Field: Post.mediaUrl
- Setup: Integrate Cloudinary for image/video storage and transformation.
- Use next/image for optimized images.

### 2. Engagement Metrics

Tracked by:

- Post.likes, Post.views
- Analytics table for detailed tracking.

### 3. Fan Feedback

Fans can submit feedback via:

- Message (direct).
- Comment (post-specific).

### 4. Admin Features

- Dashboard: Aggregate stats using the Analytics table.
- Communication: Direct messaging with creators using the Message model.

## Example Queries

### 1. Fetch Creator’s Dashboard Data

```typescript
const creatorDashboard = await prisma.user.findUnique({
  where: { id: creatorId },
  include: {
    posts: {
      include: { comments: true, _count: { select: { likes: true, views: true } } },
    },
    subscriptions: { where: { isActive: true } },
  },
});

```

### 2. Fan Subscription Status

```typescript
const isSubscribed = await prisma.subscription.findFirst({
  where: { fanId: fanId, creatorId: creatorId, isActive: true },
});
## 3. Post Engagement Metrics
typescript
Copy code
const metrics = await prisma.analytics.findMany({
  where: { creatorId: creatorId },
  orderBy: { timestamp: "desc" },
});

```
## Next Steps

#### Prisma Migration:

- Run npx prisma db push to sync schema with MongoDB.
- Add seed data for users, posts, and subscriptions.

#### Dashboard UI:

Create dashboards for Admin, Creator, and Fan using Tailwind and Shadcn.

#### Deployment:

Set environment variables in Vercel for MongoDB, Cloudinary, and Auth0.

#### Testing:

Write unit tests for CRUD operations with Jest and integration tests with Cypress.







