---
id: 5a9xpiltoqubquo68kv5qi8
title: TODO
desc: ''
updated: 1738282193791
created: 1738281707326
---
# TODO: Fix Like Feature & TypeScript Errors in Drama🎭Drops

## **1️⃣ Fix Undefined Properties in TypeScript**
### 📍 Files Affected:
- `/app/(root)/activity/page.tsx`
- `/app/(root)/page.tsx`
- `/app/(root)/profile/[id]/page.tsx`
- `/app/(root)/thread/[id]/page.tsx`

### 🔧 Steps to Fix:
- [ ] Update `fetchUser()` in `user.actions.ts` to return missing properties:
  - `_id`, `onboarded`, `id`, `username`, `image`
- [ ] Ensure `userInfo` contains `onboarded` before checking it.
- [ ] Modify the **MongoDB schema** for `User` to persist missing fields.

---

## **2️⃣ Implement Proper Like Feature for Threads**
### 📍 Files Affected:
- `/app/(root)/thread/[id]/page.tsx`
- `/components/cards/ThreadCard.tsx`
- `/lib/actions/thread.actions.ts`

### 🔧 Steps to Fix:
- [ ] Update **`Thread` model** in `thread.model.ts`:
  ```ts
  likes: [
    {
      type: mongoose.Schema.Types.ObjectId,
      ref: "User",
    },
  ],
  ```
- [ ]  Ensure `fetchThread()` returns `likes` in `thread.actions.ts`.
- [ ]  Implement `likeThread()` in `thread.actions.ts`:
    
  ```ts
  export async function likeThread(threadId: string, userId: string) { ... }
  ```
- [ ]  Modify **API routes** to handle likes properly.

___

## **3️⃣ Fix Merge Conflicts in `ThreadCard.tsx`**

### 📍 File Affected:

-   `/components/cards/ThreadCard.tsx`

### 🔧 Steps to Fix:

-   [ ]  Remove unresolved **Git merge markers** (`<<<<`, `====`, `>>>>`).
-   [ ]  Ensure component structure is valid.
-   [ ]  Check that `ThreadCard.tsx` properly **renders likes, reactions, and comments**.

___

## **4️⃣ Fix Broken Imports in `ThreadsTab.tsx` & `thread.actions.ts`**

### 📍 Files Affected:

-   `/components/shared/ThreadsTab.tsx`
-   `/lib/actions/thread.actions.ts`

### 🔧 Steps to Fix:

-   [ ]  Verify `@/lib/actions/community.actions.ts` exists and has exports.
-   [ ]  Check `thread.actions.ts` for missing **function exports**.
-   [ ]  Ensure `ThreadsTab.tsx` imports `fetchCommunityPosts()` and `fetchUserPosts()` correctly.

___

## **5️⃣ Ensure Like Counts Display Correctly**

### 📍 Files Affected:

-   `/components/cards/ThreadCard.tsx`
-   `/components/shared/ThreadsTab.tsx`

### 🔧 Steps to Fix:

-   [ ]  Update `ThreadCard.tsx` to receive:
    
    ```ts
    likesCount={thread.likes.length}
    likedByCurrentUser={thread.likes.includes(currentUserId)}
    ```
    
-   [ ]  Modify `ThreadsTab.tsx` to **fetch like counts** from the API.

___

## **6️⃣ Update `ThreadValidation` to Include Likes**

### 📍 File Affected:

-   `/lib/validations/thread.ts`

### 🔧 Steps to Fix:

-   [ ]  Modify `ThreadValidation`:
    
    ```ts
    export const ThreadValidation = z.object({
    thread: z.string().nonempty().min(3, { message: "Minimum 3 characters." }),
    accountId: z.string(),
    likes: z.array(z.string()).optional(),
    });
    ```
___

## **7️⃣ Fix Profile Page Thread Count**

### 📍 File Affected:

-   `/app/(root)/profile/[id]/page.tsx`

### 🔧 Steps to Fix:

-   [ ]  Ensure `userInfo.threads.length` is correctly calculated.
-   [ ]  Update UI to correctly render the thread count.

___

## **8️⃣ Ensure `thread/[id]/page.tsx` Displays Likes**

### 📍 File Affected:

-   `/app/(root)/thread/[id]/page.tsx`

### 🔧 Steps to Fix:

-   [ ]  Ensure thread data includes `likes` from API.
-   [ ]  Pass `likesCount` and `likedByUser` to `ThreadCard.tsx`.

___

## **Next Steps**

-   [ ]  Test all changes.
-   [ ]  Verify likes are stored and retrieved properly in MongoDB.
-   [ ]  Confirm UI updates properly when liking/unliking a thread.
-   [ ]  Fix any UI bugs in `ThreadCard.tsx` related to reactions.

___

## **Priority Order**

1️⃣ **Fix `fetchUser()` & `thread.model.ts`** (Ensure missing fields are present).  
2️⃣ **Resolve `ThreadCard.tsx` & `ThreadsTab.tsx` Issues** (Make sure UI displays likes).  
3️⃣ **Implement `likeThread()` in `thread.actions.ts`** (Ensure like functionality is working).  
4️⃣ **Fix `profile/[id]/page.tsx` & `thread/[id]/page.tsx`** (Ensure thread details display correctly).

🚀 **After completing these steps, test the Like Feature thoroughly!**
