---
id: k3xgbhyf8czfzxmklcw0yok
title: sentry
desc: ''
updated: 1733341447360
created: 1733341426702
---

### Lesson 20: **Monitoring with Sentry**

*(Track and debug errors in your Next.js app with real-time monitoring and performance insights.)*

* * *

#### What is Sentry?

- **Definition**: A tool for real-time error tracking, performance monitoring, and debugging.
- **Key Features**:
    - Captures errors and exceptions in your application.
    - Provides detailed stack traces and contextual data.
    - Tracks performance metrics like API response times and page load times.

* * *

#### Why Use Sentry?

| Feature | Benefit |
| --- | --- |
| **Error Tracking** | Automatically logs and alerts you about app errors. |
| **Performance Monitoring** | Identifies bottlenecks in your app’s performance. |
| **User Feedback** | Allows users to report issues directly from the app. |
| **Integration** | Works seamlessly with Next.js and other frameworks. |

* * *

### Step 1: Set Up Sentry

1. **Create a Sentry Account**:

    - Sign up at [Sentry](https://sentry.io/).
2. **Create a Project**:

    - In the Sentry dashboard, create a new project and select **Next.js** as the platform.
3. **Get Your DSN (Data Source Name)**:

    - The DSN is a unique URL that connects your app to Sentry.

* * *

### Step 2: Install Sentry in Your Project

1. **Install the Sentry SDK**:

        bashCopy codenpm install @sentry/nextjs
2. **Set Up Sentry**:

    - Run the Sentry setup command:

            bashCopy codenpx @sentry/wizard -i nextjs
    - This will:
        - Add a `sentry.server.config.js` and `sentry.client.config.js` file.
        - Update `next.config.js` to include Sentry settings.

* * *

### Step 3: Configure Sentry

1. **Add Your DSN to the Configuration Files**:

    - In `sentry.server.config.js`:

            javascriptCopy codeSentry.init({ dsn: process.env.SENTRY_DSN, tracesSampleRate: 1.0, // Adjust this value in production});
    - In `sentry.client.config.js`:

            javascriptCopy codeSentry.init({ dsn: process.env.SENTRY_DSN, tracesSampleRate: 1.0,});
2. **Add the DSN to `.env.local`**:

        plaintextCopy codeSENTRY_DSN=your_sentry_dsn

* * *

### Step 4: Track Errors and Exceptions

1. **Test Error Tracking**:
    - Add the following code to any page (e.g., `pages/index.js`):

            javascriptCopy codeimport * as Sentry from '@sentry/nextjs'; export default function Home() { const throwError = () => { Sentry.captureException(new Error('Test error from Next.js')); }; return ( <div className="min-h-screen flex flex-col items-center justify-center"> <h1 className="text-3xl font-bold">Sentry Integration</h1> <button onClick={throwError} className="mt-4 px-4 py-2 bg-red-500 text-white rounded hover:bg-red-600" > Trigger Error </button> </div> );}
    - Click the **Trigger Error** button and check your Sentry dashboard for the logged error.

* * *

### Step 5: Track Performance

1. **Enable Performance Monitoring**:

    - Update your Sentry configuration to include performance monitoring:
        - `sentry.server.config.js` and `sentry.client.config.js`:

                javascriptCopy codeSentry.init({ dsn: process.env.SENTRY_DSN, tracesSampleRate: 1.0, // Adjust to 0.1 in production for less sampling integrations: [new Sentry.BrowserTracing()],});
2. **Monitor API Performance**:

    - Add tracing to API routes (e.g., `pages/api/hello.js`):

            javascriptCopy codeimport * as Sentry from '@sentry/nextjs'; export default function handler(req, res) { Sentry.captureMessage('API endpoint accessed'); res.status(200).json({ message: 'Hello from API' });}

* * *

### Step 6: Advanced Features

1. **User Feedback**:

    - Add a feedback widget to your app:

            javascriptCopy codeSentry.showReportDialog({ eventId: 'event_id' });
2. **Breadcrumbs**:

    - Automatically capture logs of user actions leading to an error:

            javascriptCopy codeSentry.addBreadcrumb({ category: 'ui.click', message: 'User clicked on a button', level: 'info',});
3. **Release Tracking**:

    - Track releases by including version information:

            javascriptCopy codeSentry.init({ release: 'my-app@1.0.0',});

* * *

### Practice Task

1. **Challenge**: Log an error whenever a specific API route fails.
2. **Bonus**: Set up a custom breadcrumb trail for user interactions on a form submission page.

* * *

### Monitoring Best Practices

| Tip | Explanation |
| --- | --- |
| **Set Sampling Rates** | Reduce traces in production to avoid unnecessary data. |
| **Use Context** | Attach user and app context to errors for better insights. |
| **Test in Staging** | Test your Sentry integration in a non-production environment. |

* * *

### Resources

- Sentry Documentation
- Learn interactively: [Sentry Setup Guide](https://www.youtube.com/watch?v=NsX9AAh-rpI)
- Best Practices for Error Monitoring