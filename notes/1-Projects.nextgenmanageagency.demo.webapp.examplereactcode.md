---
id: 8a5y469wdeyy09k385lvowk
title: examplreactcode
desc: ''
updated: 1739388050938
created: 1739373119931
---

## Landing


```jsx
import React from 'react';

const ImageComponent = ({ src, alt, className }) => (
  <img src={src} alt={alt} className={className} />
);

const LinkComponent = ({ href, children, className }) => (
  <a href={href} className={className}>{children}</a>
);

const ButtonComponent = ({ variant, children }) => (
  <button className={`px-4 py-2 font-bold rounded-lg \${variant === 'default' ? 'bg-pink-500 text-black' : 'bg-gray-700 text-white'}`}>{children}</button>
);

export default function HomePage() {
  return (
    <main className="relative flex items-center justify-center min-h-screen bg-black text-white px-6 md:px-12 lg:px-24">
      {/* Background */}
      <div className="absolute inset-0">
        <ImageComponent
          src="https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/Shapes_Black.png"
          alt="NextGen Management"
          className="object-cover opacity-60 w-full h-full"
        />
      </div>

      {/* Content Container */}
      <div className="relative z-10 w-full max-w-2xl text-center p-10 bg-opacity-80 bg-black rounded-lg shadow-lg">
        {/* Logo */}
        <div className="flex justify-center">
          <ImageComponent
            src="https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/Main_Black.png"
            alt="NextGen Management Logo"
            className="w-48 mb-6"
          />
        </div>

        {/* Text */}
        <div>
          <h1 className="text-2xl tracking-wide md:text-4xl font-bold">
            Take the Next Step to Elevate Your Career with NextGen Management Agency
          </h1>
          <p className="text-lg text-gray-300 mt-4">
            Join a platform designed to streamline talent management, boost
            growth, and deliver outstanding results. Discover how we can help you
            grow your audience and maximize your potential.
          </p>
        </div>

        {/* Buttons */}
        <div className="flex flex-wrap justify-center gap-4 mt-6">
          <LinkComponent href="https://dev-wrf6egs1bskzk7n1.us.auth0.com/u/signup">
            <ButtonComponent variant="default">Create an Account</ButtonComponent>
          </LinkComponent>
          <LinkComponent href="/api/auth/login">
            <ButtonComponent variant="secondary">Login</ButtonComponent>
          </LinkComponent>
        </div>
      </div>

      {/* Footer */}
      <footer className="absolute bottom-4 left-4 right-4 flex justify-center space-x-6 text-sm text-gray-300">
        <LinkComponent href="/contact" className="flex items-center gap-1 hover:text-white">
          <span>📧</span>
          <span>Contact</span>
        </LinkComponent>
        <LinkComponent href="/about" className="flex items-center gap-1 hover:text-white">
          <span>ℹ️</span>
          <span>About</span>
        </LinkComponent>
        <LinkComponent href="/privacy" className="flex items-center gap-1 hover:text-white">
          <span>🔒</span>
          <span>Privacy Policy</span>
        </LinkComponent>
      </footer>
    </main>
  );
}
```

## About Us

```jsx
import React from 'react';
import { motion } from 'framer-motion';

const ImageComponent = ({ src, alt, className }) => (
  <motion.img src={src} alt={alt} className={className} whileHover={{ scale: 1.05 }} transition={{ duration: 0.3 }} />
);

export default function AboutUs() {
  return (
    <main className="relative flex items-center justify-center min-h-screen bg-black text-white px-6 md:px-12 lg:px-24">
      {/* Background */}
      <div className="absolute inset-0">
        <ImageComponent
          src="https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/Shapes_Black.png"
          alt="NextGen Management"
          className="object-cover opacity-60 w-full h-full"
        />
      </div>

      {/* Content Container */}
      <motion.div 
        className="relative z-10 w-full max-w-3xl text-center p-10 bg-opacity-90 bg-black rounded-lg shadow-xl"
        initial={{ opacity: 0, y: 20 }}
        animate={{ opacity: 1, y: 0 }}
        transition={{ duration: 0.8 }}
      >
        {/* Logo */}
        <div className="flex justify-center">
          <ImageComponent
            src="https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/Main_Black.png"
            alt="NextGen Management Logo"
            className="w-32 mb-6"
          />
        </div>

        {/* Executive Summary */}
        <h1 className="text-3xl font-bold mb-4">Our Story & Vision</h1>
        <p className="text-lg text-gray-300">
          At NextGen Management Agency (NGMA), our mission is to empower creators with sustainable growth,
          scalable services, and comprehensive digital management strategies. We provide the tools,
          analytics, and industry expertise to help content creators thrive.
        </p>

        {/* Business Model Overview */}
        <h2 className="text-2xl font-semibold mt-6">Business Model</h2>
        <p className="text-lg text-gray-300 mt-2">
          NGMA operates on a subscription-based model, offering creators access to advanced analytics,
          marketing tools, and full-service management. Additional revenue streams include revenue sharing,
          brand sponsorships, and educational courses.
        </p>

        {/* Brand Identity & Differentiators */}
        <h2 className="text-2xl font-semibold mt-6">Brand Identity</h2>
        <p className="text-lg text-gray-300 mt-2">
          "By Digital Herencia" is more than a tagline—it's our philosophy. We focus on data-driven
          decision-making, seamless onboarding, and community engagement, all within a professional,
          modern ecosystem.
        </p>

        {/* Visual Representation */}
        <div className="grid grid-cols-1 md:grid-cols-2 gap-4 mt-6">
          <ImageComponent
            src="https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/content%20creator%20sitting%20at%20desk%20working%20on%20edting%20content.jpg"
            alt="Content Creator at Work"
            className="rounded-lg shadow-lg w-full"
          />
          <ImageComponent
            src="https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/female%20hero%20shot.jpg"
            alt="Female Hero Shot"
            className="rounded-lg shadow-lg w-full"
          />
        </div>
      </motion.div>
    </main>
  );
}


```

## Services



```jsx
import React from 'react';
import { motion } from 'framer-motion';
import { FaChartLine, FaDollarSign, FaBullhorn, FaBook } from 'react-icons/fa';

const ImageComponent = ({ src, alt, className }) => (
  <motion.img src={src} alt={alt} className={className} whileHover={{ scale: 1.05 }} transition={{ duration: 0.3 }} />
);

export default function Services() {
  return (
    <main className="relative flex items-center justify-center min-h-screen bg-black text-white px-6 md:px-12 lg:px-24">
      {/* Background */}
      <div className="absolute inset-0">
        <ImageComponent
          src="https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/Shapes_Black.png"
          alt="NextGen Management"
          className="object-cover opacity-60 w-full h-full"
        />
      </div>

      {/* Content Container */}
      <motion.div 
        className="relative z-10 w-full max-w-3xl text-center p-10 bg-opacity-90 bg-black rounded-lg shadow-xl"
        initial={{ opacity: 0, y: 20 }}
        animate={{ opacity: 1, y: 0 }}
        transition={{ duration: 0.8 }}
      >
        {/* Heading */}
        <h1 className="text-3xl font-bold mb-4">What We Offer</h1>
        <ImageComponent
          src="https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/onlyfans%20manager%20working%20in%20nice%20office.jpg"
          alt="Content Creator Working"
          className="rounded-lg shadow-lg w-full max-w-lg mx-auto"
        />

        {/* Subscription Plans */}
        <h2 className="text-2xl font-semibold mt-6">Subscription Plans</h2>
        <div className="grid grid-cols-1 md:grid-cols-3 gap-4 mt-4">
          {[
            { title: 'Basic', price: '$50/month', features: 'Analytics & Scheduling Tools' },
            { title: 'Pro', price: '$150/month', features: 'Advanced Analytics & Marketing' },
            { title: 'Enterprise', price: 'Custom Pricing', features: 'Custom Solutions & Management' }
          ].map((plan, index) => (
            <motion.div 
              key={index} 
              className="p-6 bg-gray-900 rounded-lg shadow-md"
              whileHover={{ scale: 1.05 }}
            >
              <h3 className="text-xl font-bold text-pink-400">{plan.title}</h3>
              <p className="text-lg font-semibold mt-2">{plan.price}</p>
              <p className="text-gray-300 mt-2">{plan.features}</p>
            </motion.div>
          ))}
        </div>

        {/* Additional Revenue Streams */}
        <h2 className="text-2xl font-semibold mt-6">Additional Revenue Streams</h2>
        <div className="grid grid-cols-1 md:grid-cols-2 gap-4 mt-4">
          {[
            { icon: <FaDollarSign className="text-4xl text-green-400" />, title: 'Revenue Sharing', description: '20%-30% share from high-performing creators' },
            { icon: <FaBullhorn className="text-4xl text-blue-400" />, title: 'Paid Ads & Branding', description: 'Boost visibility with targeted promotions' },
            { icon: <FaChartLine className="text-4xl text-yellow-400" />, title: 'Sponsorships', description: 'Exclusive brand partnerships for influencers' },
            { icon: <FaBook className="text-4xl text-purple-400" />, title: 'Educational Products', description: 'Courses & workshops for creator growth' }
          ].map((service, index) => (
            <motion.div 
              key={index} 
              className="flex items-center p-4 bg-gray-900 rounded-lg shadow-md"
              whileHover={{ scale: 1.05 }}
            >
              <div className="mr-4">{service.icon}</div>
              <div>
                <h3 className="text-lg font-bold text-pink-400">{service.title}</h3>
                <p className="text-gray-300">{service.description}</p>
              </div>
            </motion.div>
          ))}
        </div>

        {/* Call-to-Action */}
        <motion.button
          className="mt-6 px-6 py-3 bg-pink-500 text-black font-bold rounded-lg hover:bg-pink-400 transition"
          whileHover={{ scale: 1.1 }}
        >
          Get Started
        </motion.button>
      </motion.div>
    </main>
  );
}
```

## ScoutHub

```jsx

import React, { useState } from 'react';
import { motion } from 'framer-motion';
import { FaSearch, FaUserTie, FaPenFancy, FaUsers, FaProjectDiagram, FaImage, FaHeart, FaUserPlus, FaVideo, FaRegNewspaper } from 'react-icons/fa';

const avatars = [
  {
    name: 'Alex Morgan - Talent Agent',
    src: 'https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/example%20profile%20pic.jpg',
  },
];

const tools = [
  { name: 'ScoutHub', icon: <FaSearch />, description: 'Find and connect with top talent.' },
  { name: 'OnboardPro', icon: <FaUserTie />, description: 'Seamless onboarding & branding.' },
  { name: 'CreateFlow', icon: <FaPenFancy />, description: 'Automate content scheduling & analytics.' },
  { name: 'EngageMax', icon: <FaUsers />, description: 'Maximize fan engagement & messaging.' },
  { name: 'SocialBoost', icon: <FaProjectDiagram />, description: 'Optimize ads & social growth strategies.' },
];

export default function ToolsDashboard() {
  const [activeTool, setActiveTool] = useState(tools[0]);
  const [currentUser] = useState(avatars[0]);
  const [searchResult, setSearchResult] = useState(null);
  const [searchInput, setSearchInput] = useState('');

  const handleSearch = () => {
    if (searchInput === '@Kazzandra') {
      setSearchResult(
        <div className="grid grid-cols-1 md:grid-cols-2 gap-4 mt-6">
          <motion.div className="p-6 bg-gray-900 rounded-lg flex flex-col items-center shadow-lg">
            <img 
              src="https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/kazzandraavatar.jpg" 
              alt="Kazzandra Profile" 
              className="rounded-lg shadow-lg w-52 h-52 mb-4"
            />
            <p className="text-lg font-bold text-white">Kazzandra</p>
            <div className="grid grid-cols-2 gap-4 mt-4 text-pink-400 text-sm text-center w-full">
              <div className="flex flex-col items-center bg-gray-800 p-3 rounded-lg"><FaImage size={20} /><span>629 Photos</span></div>
              <div className="flex flex-col items-center bg-gray-800 p-3 rounded-lg"><FaHeart size={20} /><span>5.9K Likes</span></div>
              <div className="flex flex-col items-center bg-gray-800 p-3 rounded-lg"><FaUserPlus size={20} /><span>10.6K Subscribers</span></div>
              <div className="flex flex-col items-center bg-gray-800 p-3 rounded-lg"><FaVideo size={20} /><span>141 Videos</span></div>
              <div className="flex flex-col items-center bg-gray-800 p-3 rounded-lg col-span-2"><FaRegNewspaper size={20} /><span>131 Posts</span></div>
            </div>
          </motion.div>
        </div>
      );
    } else if (searchInput === '@ScarlettAline') {
      setSearchResult(
        <div className="grid grid-cols-1 md:grid-cols-2 gap-4 mt-6">
          <motion.div className="p-6 bg-gray-900 rounded-lg flex flex-col items-center shadow-lg">
            <img 
              src="https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/scarlettavatar.jpg" 
              alt="ScarlettAline Profile" 
              className="rounded-lg shadow-lg w-52 h-52 mb-4"
            />
            <p className="text-lg font-bold text-white">ScarlettAline</p>
            <div className="grid grid-cols-2 gap-4 mt-4 text-pink-400 text-sm text-center w-full">
              <div className="flex flex-col items-center bg-gray-800 p-3 rounded-lg"><FaImage size={20} /><span>90 Photos</span></div>
              <div className="flex flex-col items-center bg-gray-800 p-3 rounded-lg"><FaHeart size={20} /><span>359 Likes</span></div>
              <div className="flex flex-col items-center bg-gray-800 p-3 rounded-lg col-span-2"><FaRegNewspaper size={20} /><span>51 Posts</span></div>
            </div>
          </motion.div>
        </div>
      );
    } else {
      setSearchResult(<p className="text-red-400 mt-4">User not found. Try another username.</p>);
    }
  };

  return (
    <div className="flex min-h-screen bg-black text-white">
      {/* Sidebar */}
      <aside className="w-64 bg-gray-900 p-6 flex flex-col space-y-6">
        <motion.img
          src="https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/Main_Black.png"
          alt="NGMA Logo"
          className="w-40 mx-auto"
          whileHover={{ scale: 1.05 }}
        />
        <nav className="flex flex-col space-y-4">
          {tools.map((tool, index) => (
            <motion.button
              key={index}
              className={`flex items-center space-x-3 px-4 py-2 rounded-lg hover:bg-gray-800 transition ${activeTool.name === tool.name ? 'bg-pink-500 text-black' : 'text-white'}`}
              onClick={() => setActiveTool(tool)}
            >
              <span className="text-xl">{tool.icon}</span>
              <span>{tool.name}</span>
            </motion.button>
          ))}
        </nav>
      </aside>

      {/* Main Content */}
      <main className="flex-1 p-8 overflow-y-auto">
        {/* Top Bar */}
        <header className="flex justify-between items-center pb-6 border-b border-gray-700">
          <h1 className="text-3xl font-bold">{activeTool.name}</h1>
          <div className="flex items-center space-x-4">
            <p className="text-lg font-semibold">{currentUser.name}</p>
            <motion.img
              src={currentUser.src}
              alt="User Avatar"
              className="w-12 h-12 rounded-full border-2 border-pink-500 cursor-pointer"
              whileHover={{ scale: 1.1 }}
            />
          </div>
        </header>

        {/* Search Tool UI */}
        {activeTool.name === 'ScoutHub' && (
          <div className="mt-6">
            <input 
              type="text" 
              className="p-2 rounded bg-gray-800 text-white w-64 border border-gray-700"
              placeholder="Enter OnlyFans username"
              value={searchInput}
              onChange={(e) => setSearchInput(e.target.value)}
            />
            <motion.button
              className="ml-4 px-6 py-2 bg-pink-500 text-black font-bold rounded-lg hover:bg-pink-400 transition"
              whileHover={{ scale: 1.1 }}
              onClick={handleSearch}
            >
              Search
            </motion.button>
            <div className="mt-4">{searchResult}</div>
          </div>
        )}
      </main>
    </div>
  );
}


```

## OnBoarder Pro

```jsx
import React, { useState } from 'react';
import { motion } from 'framer-motion';
import { FaSearch, FaUserTie, FaPenFancy, FaUsers, FaProjectDiagram, FaUpload } from 'react-icons/fa';

const avatars = [
  {
    name: 'Alex Morgan - Talent Agent',
    src: 'https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/example%20profile%20pic.jpg',
  },
];

const tools = [
  { name: 'ScoutHub', icon: <FaSearch />, description: 'Find and connect with top talent.' },
  { name: 'OnboardPro', icon: <FaUserTie />, description: 'Seamless onboarding & branding.' },
  { name: 'CreateFlow', icon: <FaPenFancy />, description: 'Automate content scheduling & analytics.' },
  { name: 'EngageMax', icon: <FaUsers />, description: 'Maximize fan engagement & messaging.' },
  { name: 'SocialBoost', icon: <FaProjectDiagram />, description: 'Optimize ads & social growth strategies.' },
];

const onboardingChecklist = [
  { name: 'Identity Verification', description: 'Upload a valid government-issued ID.' },
  { name: 'Tax Information', description: 'Provide tax forms (W-9 for US, W-8BEN for non-US).' },
  { name: 'Banking Details', description: 'Submit bank account details for payments.' },
  { name: 'Signed Contract', description: 'Upload the signed model agreement.' },
];

export default function ToolsDashboard() {
  const [activeTool, setActiveTool] = useState(tools[0]);
  const [currentUser] = useState(avatars[0]);
  const [modalOpen, setModalOpen] = useState(false);
  const [selectedDocument, setSelectedDocument] = useState(null);

  const handleFileUpload = (docName) => {
    setSelectedDocument(docName);
    setModalOpen(true);
  };

  return (
    <div className="flex min-h-screen bg-black text-white">
      {/* Sidebar */}
      <aside className="w-64 bg-gray-900 p-6 flex flex-col space-y-6">
        <motion.img
          src="https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/Main_Black.png"
          alt="NGMA Logo"
          className="w-40 mx-auto"
          whileHover={{ scale: 1.05 }}
        />
        <nav className="flex flex-col space-y-4">
          {tools.map((tool, index) => (
            <motion.button
              key={index}
              className={`flex items-center space-x-3 px-4 py-2 rounded-lg hover:bg-gray-800 transition ${activeTool.name === tool.name ? 'bg-pink-500 text-black' : 'text-white'}`}
              onClick={() => setActiveTool(tool)}
            >
              <span className="text-xl">{tool.icon}</span>
              <span>{tool.name}</span>
            </motion.button>
          ))}
        </nav>
      </aside>

      {/* Main Content */}
      <main className="flex-1 p-8 overflow-y-auto">
        {/* Top Bar */}
        <header className="flex justify-between items-center pb-6 border-b border-gray-700">
          <h1 className="text-3xl font-bold">{activeTool.name}</h1>
          <div className="flex items-center space-x-4">
            <p className="text-lg font-semibold">{currentUser.name}</p>
            <motion.img
              src={currentUser.src}
              alt="User Avatar"
              className="w-12 h-12 rounded-full border-2 border-pink-500 cursor-pointer"
              whileHover={{ scale: 1.1 }}
            />
          </div>
        </header>

        {/* OnboardPro UI */}
        {activeTool.name === 'OnboardPro' && (
          <div className="mt-6">
            <h2 className="text-xl font-semibold mb-4">Required Onboarding Documents</h2>
            <ul className="space-y-4">
              {onboardingChecklist.map((doc, index) => (
                <li key={index} className="bg-gray-800 p-4 rounded-lg flex justify-between items-center">
                  <div>
                    <p className="text-lg font-bold">{doc.name}</p>
                    <p className="text-sm text-gray-400">{doc.description}</p>
                  </div>
                  <motion.button
                    className="px-4 py-2 bg-pink-500 text-black font-bold rounded-lg hover:bg-pink-400 transition flex items-center space-x-2"
                    onClick={() => handleFileUpload(doc.name)}
                  >
                    <FaUpload />
                    <span>Upload</span>
                  </motion.button>
                </li>
              ))}
            </ul>
          </div>
        )}
      </main>

      {/* Modal for File Upload */}
      {modalOpen && (
        <div className="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
          <div className="bg-gray-900 p-6 rounded-lg shadow-lg w-96">
            <h3 className="text-xl font-semibold mb-4">Upload {selectedDocument}</h3>
            <input type="file" className="mb-4 w-full p-2 bg-gray-800 text-white rounded" />
            <div className="flex justify-end space-x-4">
              <button 
                className="px-4 py-2 bg-gray-600 text-white rounded hover:bg-gray-500"
                onClick={() => setModalOpen(false)}
              >
                Cancel
              </button>
              <button 
                className="px-4 py-2 bg-pink-500 text-black font-bold rounded-lg hover:bg-pink-400"
              >
                Upload
              </button>
            </div>
          </div>
        </div>
      )}
    </div>
  );
}

```

## Create Flow

```jsx
import React, { useState } from 'react';
import { motion } from 'framer-motion';
import { FaSearch, FaUserTie, FaPenFancy, FaUsers, FaProjectDiagram, FaUpload, FaCalendarAlt, FaCamera, FaVideo, FaEdit } from 'react-icons/fa';
import Calendar from 'react-calendar';
import 'react-calendar/dist/Calendar.css';

const avatars = [
  {
    name: 'Alex Morgan - Talent Agent',
    src: 'https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/example%20profile%20pic.jpg',
  },
];

const tools = [
  { name: 'ScoutHub', icon: <FaSearch />, description: 'Find and connect with top talent.' },
  { name: 'OnboardPro', icon: <FaUserTie />, description: 'Seamless onboarding & branding.' },
  { name: 'CreateFlow', icon: <FaPenFancy />, description: 'Content creation scheduling & workflow.' },
  { name: 'EngageMax', icon: <FaUsers />, description: 'Maximize fan engagement & messaging.' },
  { name: 'SocialBoost', icon: <FaProjectDiagram />, description: 'Optimize ads & social growth strategies.' },
];

export default function ToolsDashboard() {
  const [activeTool, setActiveTool] = useState(tools[0]);
  const [currentUser] = useState(avatars[0]);
  const [modalOpen, setModalOpen] = useState(false);
  const [selectedDate, setSelectedDate] = useState(null);
  const [appointments, setAppointments] = useState([
    { title: 'Photoshoot', time: '10:00 AM', type: 'Photography', date: new Date() },
    { title: 'Video Recording', time: '2:00 PM', type: 'Video', date: new Date() },
  ]);
  const [appointmentDetails, setAppointmentDetails] = useState({ title: '', time: '', type: '' });

  const handleDateClick = (date) => {
    setSelectedDate(date);
    setModalOpen(true);
  };

  const handleAppointmentSubmit = () => {
    if (appointmentDetails.title && appointmentDetails.time && appointmentDetails.type) {
      setAppointments([...appointments, { ...appointmentDetails, date: selectedDate }]);
      setModalOpen(false);
      setAppointmentDetails({ title: '', time: '', type: '' });
    }
  };

  return (
    <div className="flex min-h-screen bg-black text-white">
      <aside className="w-64 bg-gray-900 p-6 flex flex-col space-y-6">
        <motion.img
          src="https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/Main_Black.png"
          alt="NGMA Logo"
          className="w-40 mx-auto"
          whileHover={{ scale: 1.05 }}
        />
        <nav className="flex flex-col space-y-4">
          {tools.map((tool, index) => (
            <motion.button
              key={index}
              className={`flex items-center space-x-3 px-4 py-2 rounded-lg hover:bg-gray-800 transition ${activeTool.name === tool.name ? 'bg-pink-500 text-black' : 'text-white'}`}
              onClick={() => setActiveTool(tool)}
            >
              <span className="text-xl">{tool.icon}</span>
              <span>{tool.name}</span>
            </motion.button>
          ))}
        </nav>
      </aside>

      <main className="flex-1 p-8 overflow-y-auto">
        <header className="flex justify-between items-center pb-6 border-b border-gray-700">
          <h1 className="text-3xl font-bold">{activeTool.name}</h1>
          <div className="flex items-center space-x-4">
            <p className="text-lg font-semibold">{currentUser.name}</p>
            <motion.img
              src={currentUser.src}
              alt="User Avatar"
              className="w-12 h-12 rounded-full border-2 border-pink-500 cursor-pointer"
              whileHover={{ scale: 1.1 }}
            />
          </div>
        </header>

        {activeTool.name === 'CreateFlow' && (
          <div className="mt-6">
            <h2 className="text-xl font-semibold mb-4">Content Creation Calendar</h2>
            <Calendar 
              onClickDay={handleDateClick} 
              className="bg-gray-800 p-4 rounded-lg text-white" 
            />

            <h3 className="text-lg font-bold mt-6">At a Glance</h3>
            <ul className="mt-4 space-y-2">
              {appointments.map((appt, index) => (
                <li key={index} className="bg-gray-700 p-3 rounded-lg">
                  <p className="font-bold">{appt.title} ({appt.type})</p>
                  <p className="text-sm text-gray-400">{appt.time} on {appt.date.toDateString()}</p>
                </li>
              ))}
            </ul>
          </div>
        )}
      </main>

      {modalOpen && (
        <div className="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
          <div className="bg-gray-900 p-6 rounded-lg shadow-lg w-96">
            <h3 className="text-xl font-semibold mb-4">Schedule Content for {selectedDate?.toDateString()}</h3>
            <input 
              type="text" 
              placeholder="Title" 
              className="mb-4 w-full p-2 bg-gray-800 text-white rounded"
              value={appointmentDetails.title}
              onChange={(e) => setAppointmentDetails({ ...appointmentDetails, title: e.target.value })}
            />
            <input 
              type="time" 
              className="mb-4 w-full p-2 bg-gray-800 text-white rounded"
              value={appointmentDetails.time}
              onChange={(e) => setAppointmentDetails({ ...appointmentDetails, time: e.target.value })}
            />
            <select 
              className="mb-4 w-full p-2 bg-gray-800 text-white rounded"
              value={appointmentDetails.type}
              onChange={(e) => setAppointmentDetails({ ...appointmentDetails, type: e.target.value })}
            >
              <option value="">Select Type</option>
              <option value="Photography">Photography</option>
              <option value="Video">Video</option>
              <option value="Editing">Editing</option>
            </select>
            <div className="flex justify-end space-x-4">
              <button className="px-4 py-2 bg-gray-600 text-white rounded hover:bg-gray-500" onClick={() => setModalOpen(false)}>Cancel</button>
              <button className="px-4 py-2 bg-pink-500 text-black font-bold rounded-lg hover:bg-pink-400" onClick={handleAppointmentSubmit}>Save</button>
            </div>
          </div>
        </div>
      )}
    </div>
  );
}

```

## engagemax

```jsx
import React, { useState } from 'react';
import { motion } from 'framer-motion';
import { FaSearch, FaUserTie, FaPenFancy, FaUsers, FaProjectDiagram, FaUpload, FaCalendarAlt, FaCamera, FaVideo, FaEdit, FaUsersCog, FaChartPie, FaEnvelope } from 'react-icons/fa';
import Calendar from 'react-calendar';
import 'react-calendar/dist/Calendar.css';

const avatars = [
  {
    name: 'Alex Morgan - Talent Agent',
    src: 'https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/example%20profile%20pic.jpg',
  },
];

const tools = [
  { name: 'ScoutHub', icon: <FaSearch />, description: 'Find and connect with top talent.' },
  { name: 'OnboardPro', icon: <FaUserTie />, description: 'Seamless onboarding & branding.' },
  { name: 'CreateFlow', icon: <FaPenFancy />, description: 'Content creation scheduling & workflow.' },
  { name: 'EngageMax', icon: <FaUsers />, description: 'Maximize fan engagement & messaging.' },
  { name: 'SocialBoost', icon: <FaProjectDiagram />, description: 'Optimize ads & social growth strategies.' },
];

const fanSegments = [
  { name: 'VIP Fans', count: 120, engagement: 'High' },
  { name: 'Casual Followers', count: 340, engagement: 'Medium' },
  { name: 'Inactive Fans', count: 215, engagement: 'Low' }
];

export default function ToolsDashboard() {
  const [activeTool, setActiveTool] = useState(tools[0]);
  const [currentUser] = useState(avatars[0]);
  
  return (
    <div className="flex min-h-screen bg-black text-white">
      <aside className="w-64 bg-gray-900 p-6 flex flex-col space-y-6">
        <motion.img
          src="https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/Main_Black.png"
          alt="NGMA Logo"
          className="w-40 mx-auto"
          whileHover={{ scale: 1.05 }}
        />
        <nav className="flex flex-col space-y-4">
          {tools.map((tool, index) => (
            <motion.button
              key={index}
              className={`flex items-center space-x-3 px-4 py-2 rounded-lg hover:bg-gray-800 transition ${activeTool.name === tool.name ? 'bg-pink-500 text-black' : 'text-white'}`}
              onClick={() => setActiveTool(tool)}
            >
              <span className="text-xl">{tool.icon}</span>
              <span>{tool.name}</span>
            </motion.button>
          ))}
        </nav>
      </aside>

      <main className="flex-1 p-8 overflow-y-auto">
        <header className="flex justify-between items-center pb-6 border-b border-gray-700">
          <h1 className="text-3xl font-bold">{activeTool.name}</h1>
          <div className="flex items-center space-x-4">
            <p className="text-lg font-semibold">{currentUser.name}</p>
            <motion.img
              src={currentUser.src}
              alt="User Avatar"
              className="w-12 h-12 rounded-full border-2 border-pink-500 cursor-pointer"
              whileHover={{ scale: 1.1 }}
            />
          </div>
        </header>

        {activeTool.name === 'EngageMax' && (
          <div className="mt-6">
            <h2 className="text-xl font-semibold mb-4">Fan Segments</h2>
            <ul className="space-y-4">
              {fanSegments.map((segment, index) => (
                <li key={index} className="bg-gray-800 p-4 rounded-lg flex justify-between items-center">
                  <div>
                    <p className="text-lg font-bold">{segment.name}</p>
                    <p className="text-sm text-gray-400">{segment.count} Fans - Engagement: {segment.engagement}</p>
                  </div>
                  <FaUsersCog className="text-pink-500 text-2xl" />
                </li>
              ))}
            </ul>
            <h3 className="text-lg font-bold mt-6">CRM Actions</h3>
            <div className="flex space-x-4 mt-4">
              <motion.button className="px-6 py-2 bg-pink-500 text-black font-bold rounded-lg hover:bg-pink-400 flex items-center space-x-2">
                <FaChartPie />
                <span>Analytics</span>
              </motion.button>
              <motion.button className="px-6 py-2 bg-pink-500 text-black font-bold rounded-lg hover:bg-pink-400 flex items-center space-x-2">
                <FaEnvelope />
                <span>Send Campaign</span>
              </motion.button>
            </div>
          </div>
        )}
      </main>
    </div>
  );
}

```

## socialboost

```jsx
import React, { useState } from 'react';
import { motion } from 'framer-motion';
import { FaSearch, FaUserTie, FaPenFancy, FaUsers, FaProjectDiagram, FaUpload, FaCalendarAlt, FaCamera, FaVideo, FaEdit, FaUsersCog, FaChartPie, FaEnvelope, FaHeart, FaComment, FaUserPlus } from 'react-icons/fa';
import Calendar from 'react-calendar';
import 'react-calendar/dist/Calendar.css';

const avatars = [
  {
    name: 'Alex Morgan - Talent Agent',
    src: 'https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/example%20profile%20pic.jpg',
  },
];

const tools = [
  { name: 'ScoutHub', icon: <FaSearch />, description: 'Find and connect with top talent.' },
  { name: 'OnboardPro', icon: <FaUserTie />, description: 'Seamless onboarding & branding.' },
  { name: 'CreateFlow', icon: <FaPenFancy />, description: 'Content creation scheduling & workflow.' },
  { name: 'EngageMax', icon: <FaUsers />, description: 'Maximize fan engagement & messaging.' },
  { name: 'SocialBoost', icon: <FaProjectDiagram />, description: 'Optimize ads & social growth strategies.' },
];

const fakeActivityFeed = [
  { user: 'JohnDoe23', action: 'subscribed', icon: <FaUserPlus />, time: '2h ago' },
  { user: 'FanGirl99', action: 'liked a post', icon: <FaHeart />, time: '4h ago' },
  { user: 'CreatorX', action: 'commented: "Great content!"', icon: <FaComment />, time: '6h ago' },
  { user: 'SocialBoostFan', action: 'liked a post', icon: <FaHeart />, time: '8h ago' },
  { user: 'NewSub456', action: 'subscribed', icon: <FaUserPlus />, time: '10h ago' },
];

export default function ToolsDashboard() {
  const [activeTool, setActiveTool] = useState(tools[0]);
  const [currentUser] = useState(avatars[0]);

  return (
    <div className="flex min-h-screen bg-black text-white">
      <aside className="w-64 bg-gray-900 p-6 flex flex-col space-y-6">
        <motion.img
          src="https://raw.githubusercontent.com/DigitalHerencia/NextGenManagementAgency/refs/heads/master/public/assets/Main_Black.png"
          alt="NGMA Logo"
          className="w-40 mx-auto"
          whileHover={{ scale: 1.05 }}
        />
        <nav className="flex flex-col space-y-4">
          {tools.map((tool, index) => (
            <motion.button
              key={index}
              className={`flex items-center space-x-3 px-4 py-2 rounded-lg hover:bg-gray-800 transition ${activeTool.name === tool.name ? 'bg-pink-500 text-black' : 'text-white'}`}
              onClick={() => setActiveTool(tool)}
            >
              <span className="text-xl">{tool.icon}</span>
              <span>{tool.name}</span>
            </motion.button>
          ))}
        </nav>
      </aside>

      <main className="flex-1 p-8 overflow-y-auto">
        <header className="flex justify-between items-center pb-6 border-b border-gray-700">
          <h1 className="text-3xl font-bold">{activeTool.name}</h1>
          <div className="flex items-center space-x-4">
            <p className="text-lg font-semibold">{currentUser.name}</p>
            <motion.img
              src={currentUser.src}
              alt="User Avatar"
              className="w-12 h-12 rounded-full border-2 border-pink-500 cursor-pointer"
              whileHover={{ scale: 1.1 }}
            />
          </div>
        </header>

        {activeTool.name === 'SocialBoost' && (
          <div className="mt-6">
            <h2 className="text-xl font-semibold mb-4">Latest Social Media Activity</h2>
            <div className="bg-gray-800 p-6 rounded-lg">
              <ul className="space-y-4">
                {fakeActivityFeed.map((activity, index) => (
                  <li key={index} className="flex items-center space-x-3 p-4 bg-gray-700 rounded-lg">
                    <span className="text-pink-500 text-xl">{activity.icon}</span>
                    <p className="text-white"><strong>{activity.user}</strong> {activity.action}</p>
                    <span className="text-gray-400 text-sm">{activity.time}</span>
                  </li>
                ))}
              </ul>
            </div>
          </div>
        )}
      </main>
    </div>
  );
}

```