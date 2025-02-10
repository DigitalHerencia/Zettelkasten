---
id: s6ksflwya2cxsahsbj7fm5d
title: lighthouse
desc: ''
updated: 1733341484621
created: 1733341456111
---

### Lesson 21: **Performance Audits with Lighthouse**

*(Optimize your Next.js app for speed, accessibility, and SEO.)*

* * *

#### What is Lighthouse?

- **Definition**: An open-source tool by Google that analyzes web app performance, accessibility, best practices, SEO, and more.
- **Key Features**:
    - Provides actionable metrics for improving app performance.
    - Audits accessibility and SEO compliance.
    - Supports Progressive Web App (PWA) audits.

* * *

#### Why Use Lighthouse?

| Feature | Benefit |
| --- | --- |
| **Performance Analysis** | Identifies slow-loading resources and areas to optimize. |
| **Accessibility Checks** | Ensures your app is usable by everyone. |
| **SEO Insights** | Improves visibility in search engines. |
| **Easy Integration** | Available in Chrome DevTools and CI/CD pipelines. |

* * *

### Step 1: Run Lighthouse in Chrome DevTools

1. **Open Your App**:

    - Start your Next.js app locally and open it in Chrome (e.g., `http://localhost:3000`).
2. **Access Lighthouse**:

    - Open DevTools (right-click → Inspect → DevTools).
    - Go to the **Lighthouse** tab.
3. **Run an Audit**:

    - Select categories (Performance, Accessibility, SEO, etc.).
    - Choose device type (Mobile or Desktop).
    - Click **Generate Report**.

* * *

### Step 2: Analyze the Results

1. **Performance Metrics**:

    - **First Contentful Paint (FCP)**: Time to render the first piece of content.
    - **Largest Contentful Paint (LCP)**: Time to render the largest visible element.
    - **Cumulative Layout Shift (CLS)**: Measures visual stability during loading.
2. **Accessibility Metrics**:

    - Highlights ARIA issues, color contrast problems, and missing labels.
3. **SEO Metrics**:

    - Ensures meta tags, titles, and descriptions are present.

* * *

### Step 3: Optimize Your App Based on Lighthouse Recommendations

#### Common Recommendations:

| Issue | Solution |
| --- | --- |
| **Large Images** | Use the `next/image` component for optimized images. |
| **Unused CSS/JS** | Remove unused code or use code-splitting techniques. |
| **Render-Blocking Resources** | Use lazy loading and prefetch critical resources. |
| **Missing Alt Text** | Add `alt` attributes to all images. |

* * *

### Step 4: Automate Lighthouse Audits

1. **Install Lighthouse CI**:

        bashCopy codenpm install -g @lhci/cli
2. **Set Up a Config File**:

    - Create a `lighthouserc.js` file:

            javascriptCopy codemodule.exports = { ci: { collect: { startServerCommand: 'npm run start', url: ['http://localhost:3000'], }, assert: { assertions: { 'categories:performance': ['warn', { minScore: 0.9 }], 'categories:accessibility': ['error', { minScore: 1 }], }, }, },};
3. **Run Lighthouse CI**:

        bashCopy codelhci autorun

* * *

### Step 5: Integrate Lighthouse into CI/CD

1. **Add Lighthouse to GitHub Actions**:

    - Create a `.github/workflows/lighthouse.yml` file:

            yamlCopy codename: Lighthouse CI on: [push] jobs: lighthouse: runs-on: ubuntu-latest steps: - name: Checkout code uses: actions/checkout@v2 - name: Install dependencies run: npm install - name: Run Lighthouse CI run: npx lhci autorun
2. **Monitor Results**:

    - View Lighthouse scores for every deployment.

* * *

### Step 6: Best Practices for Performance Optimization

#### Images

- Use the `next/image` component:

        javascriptCopy codeimport Image from 'next/image'; export default function Home() { return <Image src="/example.jpg" width={600} height={400} alt="Example" />;}

#### Fonts

- Load custom fonts efficiently:

        javascriptCopy codeimport { Roboto } from '@next/font/google'; const roboto = Roboto({ subsets: ['latin'], weight: '400' }); export default function Home() { return <h1 className={roboto.className}>Hello, World!</h1>;}

#### Lazy Loading

- Lazy load non-critical content:

        javascriptCopy codeimport dynamic from 'next/dynamic'; const LazyComponent = dynamic(() => import('./LazyComponent'), { ssr: false }); export default function Home() { return <LazyComponent />;}

* * *

### Practice Task

1. **Challenge**: Run Lighthouse on your Next.js app and fix at least two performance issues.
2. **Bonus**: Automate Lighthouse checks using GitHub Actions.

* * *

### Advanced Features

1. **Custom Audits**:
    - Extend Lighthouse with custom metrics or assertions.
2. **CI Integration**:
    - Use services like Google Cloud Build or Jenkins for automated audits.

* * *

### Resources

- Lighthouse Documentation
- [Using Lighthouse CI](https://github.com/GoogleChrome/lighthouse-ci)
- Learn interactively: [Lighthouse Tutorial](https://www.youtube.com/watch?v=NoRYn6gOtVo)