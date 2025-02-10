---
id: hfu65lf3prjiyv9w0jl23z8
title: stripe-sdk
desc: ''
updated: 1733341047165
created: 1733341022821
---

### Lesson 17: **Payment Integration with Stripe SDK**

*(Learn to securely process payments and manage subscriptions in your Next.js app.)*

* * *

#### What is Stripe?

- **Definition**: A powerful, developer-friendly platform for online payment processing and subscription management.
- **Key Features**:
    - Simple APIs for integrating payments.
    - Supports one-time payments, subscriptions, and invoicing.
    - Built-in fraud prevention and compliance with PCI standards.
    - Multi-currency and international payment support.

* * *

#### Why Use Stripe?

| Feature | Benefit |
| --- | --- |
| **Ease of Integration** | SDKs for various platforms with comprehensive docs. |
| **Secure** | Handles PCI compliance and sensitive payment details. |
| **Scalability** | Supports businesses of all sizes, from startups to enterprises. |
| **Global Support** | Accepts payments from over 135 currencies. |

* * *

### Step 1: Set Up Stripe

1. **Create a Stripe Account**:

    - Sign up at [Stripe](https://stripe.com/).
2. **Get Your API Keys**:

    - Go to the Stripe Dashboard → Developers → API keys.
    - Note the **Publishable Key** and **Secret Key**.
3. **Install the Stripe Node.js SDK**:

        bashCopy codenpm install stripe

* * *

### Step 2: Configure Stripe in Your App

1. **Set Up a Stripe Instance**:

    - Create a file `lib/stripe.js`:

            javascriptCopy codeimport Stripe from 'stripe'; const stripe = new Stripe(process.env.STRIPE_SECRET_KEY, { apiVersion: '2022-11-15',}); export default stripe;
2. **Add Environment Variables**:

    - Add the following to `.env.local`:

            plaintextCopy codeSTRIPE_SECRET_KEY=your_secret_keySTRIPE_PUBLISHABLE_KEY=your_publishable_key

* * *

### Step 3: Create a Payment Session

1. **Add an API Route for Checkout**:

    - Add a file `pages/api/checkout.js`:

            javascriptCopy codeimport stripe from '@/lib/stripe'; export default async function handler(req, res) { if (req.method === 'POST') { try { const session = await stripe.checkout.sessions.create({ payment_method_types: ['card'], mode: 'payment', success_url: `${req.headers.origin}/success?session_id={CHECKOUT_SESSION_ID}`, cancel_url: `${req.headers.origin}/cancel`, line_items: req.body.items, }); res.status(200).json({ url: session.url }); } catch (error) { res.status(500).json({ error: error.message }); } } else { res.setHeader('Allow', ['POST']); res.status(405).end(`Method ${req.method} Not Allowed`); }}
2. **Create Checkout Items on the Frontend**:

    - Update `pages/index.js`:

            javascriptCopy codeexport default function Home() { const handleCheckout = async () => { const res = await fetch('/api/checkout', { method: 'POST', headers: { 'Content-Type': 'application/json' }, body: JSON.stringify({ items: [ { price_data: { currency: 'usd', product_data: { name: 'T-Shirt', }, unit_amount: 2000, }, quantity: 1, }, ], }), }); const { url } = await res.json(); window.location.href = url; }; return ( <div className="min-h-screen flex flex-col items-center justify-center"> <h1 className="text-3xl font-bold mb-4">Purchase a T-Shirt</h1> <button onClick={handleCheckout} className="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600" > Checkout </button> </div> );}

* * *

### Step 4: Handle Success and Cancellations

1. **Create a Success Page**:

    - Add a file `pages/success.js`:

            javascriptCopy codeexport default function Success() { return ( <div className="min-h-screen flex items-center justify-center"> <h1 className="text-3xl font-bold">Payment Successful!</h1> <p>Thank you for your purchase.</p> </div> );}
2. **Create a Cancellation Page**:

    - Add a file `pages/cancel.js`:

            javascriptCopy codeexport default function Cancel() { return ( <div className="min-h-screen flex items-center justify-center"> <h1 className="text-3xl font-bold">Payment Cancelled</h1> <p>You can try again when you're ready.</p> </div> );}

* * *

### Step 5: Add Webhooks (Optional)

1. **Set Up Webhooks to Handle Payment Events**:
    - Add a file `pages/api/webhook.js`:

            javascriptCopy codeimport { buffer } from 'micro';import stripe from '@/lib/stripe'; export const config = { api: { bodyParser: false, },}; export default async function handler(req, res) { const sig = req.headers['stripe-signature']; try { const event = stripe.webhooks.constructEvent( await buffer(req), sig, process.env.STRIPE_WEBHOOK_SECRET ); if (event.type === 'checkout.session.completed') { console.log('Payment succeeded:', event.data.object); } res.status(200).json({ received: true }); } catch (error) { res.status(400).send(`Webhook Error: ${error.message}`); }}
    - **Add Webhook Secret**:

        - Generate a webhook secret from the Stripe Dashboard and add it to `.env.local`:

                plaintextCopy codeSTRIPE_WEBHOOK_SECRET=your_webhook_secret

* * *

### Advanced Features

1. **Subscriptions**:

    - Use Stripe's subscription API to handle recurring payments.
    - Change the `mode` in the checkout session to `subscription` and link products to pricing plans.
2. **Customer Portal**:

    - Redirect users to the Stripe customer portal for managing billing details:

            javascriptCopy codeconst portalSession = await stripe.billingPortal.sessions.create({ customer: 'customer_id', return_url: `${req.headers.origin}/account`,}); res.json({ url: portalSession.url });

* * *

### Practice Task

1. **Challenge**: Add multiple products with different prices to the checkout.
2. **Bonus**: Fetch products dynamically from Stripe using the `stripe.products.list` API.

* * *

### Resources

- [Stripe Documentation](https://stripe.com/docs)
- [Next.js + Stripe Example](https://github.com/vercel/nextjs-subscription-payments)
- Learn interactively: [Stripe Payment Integration](https://www.youtube.com/watch?v=ZvvpXrQKJ5Y)