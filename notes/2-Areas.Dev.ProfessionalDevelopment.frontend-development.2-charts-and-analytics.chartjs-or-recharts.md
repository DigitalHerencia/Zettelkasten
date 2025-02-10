---
id: 3ik9r800sc3bnycqriv1hjs
title: chartjs-or-recharts
desc: ''
updated: 1733340449326
created: 1733340424806
---

### Lesson 9: **Data Visualization with Shadcn Charts**

*(Create modern, interactive charts in your application.)*

* * *

#### What Are Shadcn Charts?

Shadcn charts integrate accessible and customizable chart components using libraries like **Chart.js** or **Recharts**. They follow modern design principles and are styled with **Tailwind CSS**, making them easy to customize for your needs.

* * *

#### Why Use Shadcn Charts?

| Feature | Benefit |
| --- | --- |
| **Tailwind Integration** | Seamless customization to match your app's design. |
| **Responsive** | Automatically adjusts for different screen sizes. |
| **Accessible** | Designed with WAI-ARIA standards for better usability. |
| **Supports Various Types** | Line, bar, pie, and more charts. |

* * *

### Installing Dependencies

1. **Install Chart.js** (or the charting library you want):

        bashCopy codenpm install chart.js
2. **Optional**: Add helper libraries if required for advanced use cases (e.g., `react-chartjs-2` for React wrappers).

* * *

### Example: Simple Line Chart

1. **Add the Chart Component**:

    - Create a new file `components/LineChart.js`:

            javascriptCopy codeimport { Line } from 'react-chartjs-2'; export default function LineChart() { const data = { labels: ['January', 'February', 'March', 'April', 'May'], datasets: [ { label: 'Sales', data: [12, 19, 3, 5, 2], borderColor: 'rgba(75, 192, 192, 1)', backgroundColor: 'rgba(75, 192, 192, 0.2)', borderWidth: 2, }, ], }; const options = { responsive: true, plugins: { legend: { position: 'top', }, }, }; return ( <div className="w-full max-w-lg mx-auto"> <Line data={data} options={options} /> </div> );}
2. **Use the Chart in a Page**:

    - Update `pages/index.js`:

            javascriptCopy codeimport LineChart from '@/components/LineChart'; export default function Home() { return ( <div className="min-h-screen bg-gray-100 flex flex-col items-center justify-center"> <h1 className="text-3xl font-bold mb-4">Sales Data</h1> <LineChart /> </div> );}

* * *

### Adding Shadcn Styling

To style the chart with Shadcn principles:

1. Wrap the chart in a **Card Component**:

        javascriptCopy codeimport { Card, CardHeader, CardBody } from 'shadcn/ui';import { Line } from 'react-chartjs-2'; export default function StyledLineChart() { const data = { /* same as above */ }; const options = { /* same as above */ }; return ( <Card className="w-full max-w-lg mx-auto"> <CardHeader> <h2 className="text-xl font-bold">Sales Chart</h2> </CardHeader> <CardBody> <Line data={data} options={options} /> </CardBody> </Card> );}

* * *

### Interactive Practice

1. **Task**: Add a bar chart showing "Monthly Expenses".

    - Use Chart.js and the `Bar` component.
    - Include the chart inside a styled **Card**.
2. **Challenge**: Add buttons to toggle between datasets (e.g., Sales vs. Expenses).

* * *

### Advanced Features

1. **Dynamic Data Loading**:  
Fetch data from an API and update the chart dynamically:

        javascriptCopy codeimport { useState, useEffect } from 'react';import { Line } from 'react-chartjs-2'; export default function DynamicLineChart() { const [chartData, setChartData] = useState({ labels: [], datasets: [] }); useEffect(() => { fetch('/api/sales') .then((res) => res.json()) .then((data) => { setChartData({ labels: data.months, datasets: [ { label: 'Sales', data: data.values, borderColor: 'rgba(75, 192, 192, 1)', backgroundColor: 'rgba(75, 192, 192, 0.2)', }, ], }); }); }, []); return ( <div className="w-full max-w-lg mx-auto"> <Line data={chartData} /> </div> );}
2. **Animations**:  
Use Chart.js animations for smoother transitions between datasets.

* * *

### Resources

- Chart.js Documentation
- [Shadcn UI Library](https://shadcn.dev)
- React Chart.js 2