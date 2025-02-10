---
id: hh71vccq5f51bzhlgocdnv1
title: '192845'
desc: ''
updated: 1738982220158
created: 1738981729146
---
# React.js Wireframes

## Standards and Advanced Functionalities

- Spacing and Layout:
    - Define a baseline grid (e.g., 8px or 16px increments) that applies across all components.
    - Use consistent padding (e.g., 16px internal, 12px between components) and margin conventions.

- Navigation and Buttons:
    - Ensure all buttons (e.g., primary actions like “Save,” “Submit,” “Contribute”) have consistent styling, hover effects, and disabled states.
    - Standardize link names in navigation (e.g., “Home,” “Properties,” “Dashboard,” “Profile”) and place secondary options (e.g., “Edit Profile,” “Logout”) in dropdown menus under the user avatar.

- Advanced Functionalities:
    - Dropdown Menus: Used in TopNavigation for user actions and in PropertyForm for selecting property types.
    - Toast Notifications: Standardize position (top-right) and duration (3 to 5 seconds) for user feedback on actions (e.g., form submission, error messages).
    - Stepper Components: For multi-step forms like user registration or complex property submission processes.
    - Form Design: Inline error messages, clear labeling, and responsive input fields.
    - Calendars/Date Pickers: For fields such as funding deadlines or user birthdates, ensuring mobile-friendly interactions.

---

## Mapping from Atomic UI to Shared, Forms, and Cards to Pages

- Atomic UI (Button, Input, Card, etc.) is the base layer, which is composed into:
    - Shared components (e.g., TopNavigation, Sidebars, SocialShareButtons) that appear on all pages.
    - Reusable forms (e.g., UserForm, PropertyForm, ContributionsForm) used on registration, profile editing, property submission, and contribution pages.
    - Reusable cards (e.g., UserCard, PropertyCard, ContributionsCard) that display summarized data on landing pages, dashboards, and listings.

- Example Flow:
    - A contributor logs in and sees the TopNavigation (with Home, Dashboard, Profile links) and LeftSidebar.
    - On the Dashboard, a UserCard (built with UI Card, Avatar, and Button components) summarizes their profile; a ContributionsCard displays their funding history.
    - If the contributor clicks “Edit Profile,” the UserForm (composed of UI Input, Button, and possibly Modal components) is rendered on a dedicated Profile Edit page.
    - On a Property Detail page, the PropertyCard displays property details at the top, and below it, the ContributionsForm is available to submit a new contribution.
    - SocialShareButtons are integrated within the PropertyCard or as a floating component on the page, using UI Button and Icon elements.

---

## Global Standards & Design System

Below is a detailed, modern wireframe plan that integrates all the reusable components—shared elements, cards, and forms - into a set of clean, consistent page layouts. Each page’s wireframe is presented with annotated ASCII diagrams alongside standards for spacing, layout, typography, and functionality. These specifications help ensure a cohesive design system across the VESTA platform.

- Baseline Grid & Spacing:
    - Base unit: 8px increments (e.g., padding/margin: 8px, 16px, 24px, etc.).
    - Consistent gutter spacing between components: 16px between sections; 12px between individual cards or list items.

- Typography & Colors:
    - Headings use a clear sans-serif (e.g., 24–32px for H1, 18–22px for H2) with ample line-height.
    - Body text set at 16px with 1.5 line-height.
    - Use a consistent color palette for primary actions (brand blue), secondary (gray), and alerts (green/red for success/error).

- Buttons & Interactions:
    - Primary buttons: Filled with brand color, rounded corners (4–8px radius), padding (e.g., 12px 24px).
    - Secondary buttons: Outlined style with hover effects.
    - All interactive elements include clear hover/focus states, accessible keyboard navigation, and subtle shadows.

- Component Hierarchy:
    - Atomic UI (Buttons, Inputs, Avatars, Icons) compose shared components (navigation, sidebars, social share) that are then integrated with higher-level forms and cards.
    - Consistent margins/padding around cards and forms to ensure readability and visual hierarchy.
    
---

## Justification

- Consistency:
    - By mapping atomic UI elements into shared, card, and form components, the application maintains a cohesive look and feel across all pages.
    - Defined spacing, padding, and typography standards ensure that components are visually aligned and accessible.

- Modularity:
    - Reusable components reduce redundancy and improve maintainability. Each component can be updated independently, ensuring scalability as the application evolves.

- Functionality and Usability:
    - Advanced features like dropdowns, steppers, toast notifications, and date pickers enhance the user experience by providing intuitive feedback and smooth interactions.
    - Clearly defined navigation, consistent button placements, and responsive design choices ensure that both desktop and mobile users receive an optimal experience.

- Standards:
    - Establishing naming conventions for navigation links (e.g., Home, Dashboard, Profile) and setting guidelines for where actions (e.g., Logout, Edit Profile) reside in the UI supports an intuitive user journey.
    - Detailed wireframes and ASCII diagrams serve as a design reference for developers and designers, ensuring alignment across the team.

This comprehensive wireframe and standards plan provides a clear blueprint for creating, organizing, and implementing the individual reusable components in the shared, cards, and forms folders—ensuring a robust, consistent, and user-friendly interface for the VESTA real estate crowdfunding platform.

---

## Wireframe Code

### Top Navigation Wireframe

```jsx
import React, { useState } from "react";
import { FaHome, FaBuilding, FaUser, FaCog, FaSearch, FaUserCircle, FaChevronDown, FaBell } from "react-icons/fa";

export const TopNavigation = () => {
  const [showDropdown, setShowDropdown] = useState(false);
  const [showTooltip, setShowTooltip] = useState(false);

  return (
    <nav className="flex items-center justify-between p-4 bg-gray-900 text-white shadow-md h-16">
      <div className="flex items-center gap-4">
        <FaHome className="text-xl" />
        <a href="/" className="font-semibold text-lg">VESTA</a>
        <a href="/home" className="hover:text-gray-400">Home</a>
        <a href="/properties" className="hover:text-gray-400">Properties</a>
        <a href="/dashboard" className="hover:text-gray-400">Dashboard</a>
        <a href="/profile" className="hover:text-gray-400">Profile</a>
      </div>
      <div className="flex items-center gap-4 relative">
        <input type="text" placeholder="Search..." className="border p-2 rounded-md bg-gray-800 text-white placeholder-gray-400" />
        <div className="relative" onMouseEnter={() => setShowTooltip(true)} onMouseLeave={() => setShowTooltip(false)}>
          <FaBell className="text-xl cursor-pointer" />
          {showTooltip && (
            <div className="absolute top-full mt-1 p-2 bg-gray-700 text-white text-sm rounded shadow-md">You have new notifications</div>
          )}
        </div>
        <div className="relative">
          <button onClick={() => setShowDropdown(!showDropdown)} className="flex items-center gap-2">
            <FaUserCircle className="text-2xl" />
            <FaChevronDown className="text-sm" />
          </button>
          {showDropdown && (
            <div className="absolute right-0 mt-2 w-48 bg-gray-800 text-white rounded shadow-md overflow-hidden">
              <a href="/profile" className="block px-4 py-2 hover:bg-gray-700">Edit Profile</a>
              <a href="/settings" className="block px-4 py-2 hover:bg-gray-700">Settings</a>
              <a href="/logout" className="block px-4 py-2 hover:bg-gray-700">Logout</a>
            </div>
          )}
        </div>
      </div>
    </nav>
  );
};

export default TopNavigation;

```

### Left Sidebar (Desktop)

```jsx
import React, { useState, useEffect } from "react";
import { FaHome, FaBuilding, FaUser, FaCog, FaBars } from "react-icons/fa";

export const Sidebar = () => {
  const [isMobile, setIsMobile] = useState(false);
  const [isCollapsed, setIsCollapsed] = useState(false);

  useEffect(() => {
    const handleResize = () => {
      setIsMobile(window.innerWidth <= 768);
    };

    handleResize();
    window.addEventListener("resize", handleResize);
    return () => window.removeEventListener("resize", handleResize);
  }, []);

  if (isMobile) {
    return (
      <nav className="fixed bottom-0 left-0 w-full bg-gray-900 text-white shadow-md flex justify-around p-3">
        <a href="/home" className="text-xl"><FaHome /></a>
        <a href="/properties" className="text-xl"><FaBuilding /></a>
        <a href="/contributions" className="text-xl"><FaUser /></a>
        <a href="/settings" className="text-xl"><FaCog /></a>
      </nav>
    );
  }

  return (
    <aside className={`bg-gray-800 text-white h-screen p-4 transition-all ${isCollapsed ? 'w-16' : 'w-64'}`}>
      <button 
        onClick={() => setIsCollapsed(!isCollapsed)}
        className="text-white mb-4 ml-2 focus:outline-none"
      >
        <FaBars className="text-2xl" />
      </button>
      <nav className="flex flex-col gap-6 ml-3">
        <a href="/dashboard" className="flex items-center gap-2"><FaHome /> {!isCollapsed && "Dashboard"}</a>
        <a href="/properties" className="flex items-center gap-2"><FaBuilding /> {!isCollapsed && "Properties"}</a>
        <a href="/contributions" className="flex items-center gap-2"><FaUser /> {!isCollapsed && "Contributions"}</a>
        <a href="/settings" className="flex items-center gap-2"><FaCog /> {!isCollapsed && "Settings"}</a>
      </nav>
    </aside>
  );
};

export default Sidebar;

```

### Footer

```jsx
import React from "react";

export const Footer = () => {
  return (
    <footer className="text-center p-4 bg-gray-800 text-gray-400 text-sm fixed bottom-0 w-full">
      © 2025 VESTA | 
      <a href="/about" className="text-gray-300 mx-2">About</a> | 
      <a href="/contact" className="text-gray-300 mx-2">Contact</a> | 
      <a href="/terms" className="text-gray-300 mx-2">Terms</a>
    </footer>
  );
};

export default Footer;

```

### Social Share Buttons

```jsx
import React from "react";
import { FaTwitter, FaFacebook, FaLinkedin, FaInstagram } from "react-icons/fa";

export const SocialShareButtons = () => {
  return (
    <div className="flex gap-2">
      <button className="bg-blue-600 text-white p-2 rounded flex items-center justify-center w-10 h-10">
        <FaTwitter className="text-xl" />
      </button>
      <button className="bg-blue-800 text-white p-2 rounded flex items-center justify-center w-10 h-10">
        <FaFacebook className="text-xl" />
      </button>
      <button className="bg-blue-500 text-white p-2 rounded flex items-center justify-center w-10 h-10">
        <FaLinkedin className="text-xl" />
      </button>
      <button className="bg-pink-500 text-white p-2 rounded flex items-center justify-center w-10 h-10">
        <FaInstagram className="text-xl" />
      </button>
    </div>
  );
};

export default SocialShareButtons;

```

### User Card

```jsx
import React from "react";
import { FaUserCircle, FaHandsHelping, FaUserFriends } from "react-icons/fa";

const placeholderUser = {
  name: "John Doe",
  role: "Contributor",
  contributions: 5,
  referrals: 20,
};

export const UserCard = ({ name, role, contributions, referrals }) => {
  return (
    <div className="bg-gray-800 text-white p-4 rounded shadow-md w-64 cursor-pointer hover:shadow-lg transition-shadow">
      <div className="flex items-center gap-4">
        <FaUserCircle className="text-4xl" />
        <div>
          <h2 className="text-lg font-semibold">{name}</h2>
          <p className="text-gray-400">{role}</p>
        </div>
      </div>
      <div className="mt-4">
        <p className="flex items-center gap-2"><FaHandsHelping /> {contributions} Contributions</p>
        <p className="flex items-center gap-2"><FaUserFriends /> {referrals} Referrals</p>
      </div>
    </div>
  );
};

export default function App() {
  return <UserCard {...placeholderUser} />;
}

```

### Property Card

```jsx
import React from "react";

const placeholderProperty = {
  image: "https://placehold.co/600x400",
  title: "Luxury Apartment",
  location: "New York, NY",
  price: "$500,000",
  roi: "12%",
  funding: "85%",
};

export const PropertyCard = ({ image, title, location, price, roi, funding }) => {
  return (
    <div className="bg-gray-800 text-white p-4 rounded shadow-md w-72 cursor-pointer hover:shadow-lg transition-shadow">
      <img src={image} alt={title} className="w-full h-40 object-cover rounded" />
      <div className="mt-4">
        <h2 className="text-lg font-semibold">{title}</h2>
        <p className="text-gray-400">{location}</p>
        <div className="flex justify-between mt-2">
          <p className="text-green-400">ROI: {roi}</p>
          <p className="text-blue-400">Funding: {funding}</p>
        </div>
        <p className="mt-2 font-semibold">Price: {price}</p>
      </div>
      <button className="mt-4 w-full bg-blue-600 text-white py-2 rounded hover:bg-blue-700 transition">Invest Now</button>
    </div>
  );
};

export default function App() {
  return <PropertyCard {...placeholderProperty} />;
}

```

### Contributions Card

```jsx
import React from "react";

const placeholderContribution = {
  amount: "$1,000",
  tier: "Legatus",
  date: "2025-01-15",
  status: "Completed",
};

const statusColors = {
  Pending: "text-yellow-400",
  Completed: "text-green-400",
  Refunded: "text-red-400",
};

export const ContributionsCard = ({ amount, tier, date, status }) => {
  return (
    <div className="bg-gray-800 text-white p-4 rounded shadow-md w-64 cursor-pointer hover:shadow-lg transition-shadow">
      <div className="grid grid-cols-2 gap-2">
        <p className="font-semibold">Amount:</p>
        <p>{amount}</p>
        <p className="font-semibold">Tier:</p>
        <p>{tier}</p>
        <p className="font-semibold">Date:</p>
        <p>{date}</p>
        <p className="font-semibold">Status:</p>
        <p className={statusColors[status]}>{status}</p>
      </div>
      <button className="mt-4 w-full bg-blue-600 text-white py-2 rounded hover:bg-blue-700 transition">Details</button>
    </div>
  );
};

export default function App() {
  return <ContributionsCard {...placeholderContribution} />;
}

```

### User Form

```jsx
import React, { useState } from "react";
import { FaUserCircle, FaUpload, FaCheckCircle, FaTimesCircle } from "react-icons/fa";

const states = [
  "AL", "AK", "AZ", "AR", "CA", "CO", "CT", "DE", "FL", "GA", "HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC", "SD", "TN", "TX", "UT", "VT", "VA", "WA", "WV", "WI", "WY"
];

const placeholderUser = {
  verified: false, // Change to false for unverified users
};

const UserForm = () => {
  const [formData, setFormData] = useState({
    name: "",
    email: "",
    phone: "",
    address: "",
    city: "",
    state: "",
    zip: "",
    bio: "",
  });

  const handleChange = (e) => {
    setFormData({ ...formData, [e.target.name]: e.target.value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log("Form Submitted", formData);
  };

  return (
    <form onSubmit={handleSubmit} className="bg-gray-800 text-white p-6 rounded shadow-md w-96">
      <div className="flex flex-col items-center mb-4">
        <FaUserCircle className="text-6xl" />
        <button type="button" className="mt-2 bg-blue-600 py-2 px-4 rounded hover:bg-blue-700 flex items-center gap-2">
          <FaUpload /> Upload Profile Picture
        </button>
      </div>
      <h2 className="text-lg font-semibold mb-4">User Information</h2>
      <div className="flex flex-col gap-4">
        <input type="text" name="name" placeholder="Name" value={formData.name} onChange={handleChange} className="p-2 rounded bg-gray-700" />
        <input type="email" name="email" placeholder="Email" value={formData.email} onChange={handleChange} className="p-2 rounded bg-gray-700" />
        <input type="tel" name="phone" placeholder="Phone" value={formData.phone} onChange={handleChange} className="p-2 rounded bg-gray-700" />
        <input type="text" name="address" placeholder="Address" value={formData.address} onChange={handleChange} className="p-2 rounded bg-gray-700" />
        <div className="grid grid-cols-2 gap-4">
          <input type="text" name="city" placeholder="City" value={formData.city} onChange={handleChange} className="p-2 rounded bg-gray-700" />
          <select name="state" value={formData.state} onChange={handleChange} className="p-2 rounded bg-gray-700">
            <option value="">Select State</option>
            {states.map((state) => (
              <option key={state} value={state}>{state}</option>
            ))}
          </select>
        </div>
        <input type="text" name="zip" placeholder="ZIP" value={formData.zip} onChange={handleChange} className="p-2 rounded bg-gray-700" />
        <textarea name="bio" placeholder="Bio" value={formData.bio} onChange={handleChange} className="p-2 rounded bg-gray-700"></textarea>
      </div>
      <div className="flex items-center gap-2 mt-4">
        {placeholderUser.verified ? (
          <FaCheckCircle className="text-green-400" />
        ) : (
          <FaTimesCircle className="text-red-400" />
        )}
        <p>{placeholderUser.verified ? "Verified User" : "Unverified User"}</p>
      </div>
      <div className="flex justify-between mt-4">
        <button type="button" className="bg-red-600 py-2 px-4 rounded hover:bg-red-700">Cancel</button>
        <button type="submit" className="bg-blue-600 py-2 px-4 rounded hover:bg-blue-700">Save</button>
      </div>
    </form>
  );
};

export default UserForm;

```

### Property Form

```jsx
import React, { useState, useCallback } from "react";

const states = [
  "AL", "AK", "AZ", "AR", "CA", "CO", "CT", "DE", "FL", "GA", "HI", "ID", "IL", "IN", "IA", "KS", "KY", "LA", "ME", "MD", "MA", "MI", "MN", "MS", "MO", "MT", "NE", "NV", "NH", "NJ", "NM", "NY", "NC", "ND", "OH", "OK", "OR", "PA", "RI", "SC", "SD", "TN", "TX", "UT", "VT", "VA", "WA", "WV", "WI", "WY"
];

const imageCategories = [
  "Hero Shot", "Kitchen", "Backyard", "Living Room", "Bathroom", "Bedroom", "Exterior Front", "Exterior Back", "Garage", "Floor Plan"
];

const featuresList = [
  "Garage", "Pool", "Basement", "Hardwood Floors", "Central Air", "Fireplace", "Fenced Yard", "Balcony", "Walk-in Closet", "Smart Home"
];

const PropertyForm = () => {
  const [formData, setFormData] = useState({
    title: "",
    description: "",
    address: "",
    city: "",
    state: "",
    zip: "",
    price: "",
    size: "",
    bedrooms: "",
    bathrooms: "",
    propertyType: "",
    fundingDeadline: "",
    images: [],
    features: [],
  });

  const [showImageModal, setShowImageModal] = useState(false);
  const [selectedImageType, setSelectedImageType] = useState("");
  const [selectedFile, setSelectedFile] = useState(null);

  const handleFeatureChange = useCallback((feature) => {
    setFormData((prev) => {
      const newFeatures = prev.features.includes(feature)
        ? prev.features.filter((f) => f !== feature)
        : [...prev.features, feature];
      return { ...prev, features: newFeatures };
    });
  }, []);

  const handleImageUpload = useCallback(() => {
    if (selectedFile && selectedImageType) {
      setFormData((prev) => ({
        ...prev,
        images: [...prev.images, { type: selectedImageType, file: selectedFile }],
      }));
      setShowImageModal(false);
      setSelectedFile(null);
      setSelectedImageType("");
    }
  }, [selectedFile, selectedImageType]);

  const handleChange = useCallback((e) => {
    const { name, value } = e.target;
    setFormData((prev) => ({ ...prev, [name]: value }));
  }, []);

  const handleSubmit = useCallback((e) => {
    e.preventDefault();
    console.log("Property Submitted", formData);
  }, [formData]);

  return (
    <form
      onSubmit={handleSubmit}
      className="bg-gray-800 text-white p-6 rounded shadow-md w-[800px] grid grid-cols-2 gap-6"
    >
      <h2 className="text-lg font-semibold col-span-2">Property Information</h2>
      <div className="grid grid-cols-2 gap-4 col-span-2">
        <div>
          <label>Title</label>
          <input
            type="text"
            name="title"
            placeholder="Enter property title"
            value={formData.title}
            onChange={handleChange}
            className="p-2 rounded bg-gray-700 w-full"
          />
        </div>
        <div>
          <label>Funding Deadline</label>
          <input
            type="date"
            name="fundingDeadline"
            value={formData.fundingDeadline}
            onChange={handleChange}
            className="p-2 rounded bg-gray-700 w-full"
          />
        </div>
      </div>
      <div className="grid grid-cols-2 gap-4 col-span-2">
        <div>
          <label>Price (USD)</label>
          <input
            type="number"
            name="price"
            placeholder="$500,000"
            value={formData.price}
            onChange={handleChange}
            className="p-2 rounded bg-gray-700 w-full"
          />
        </div>
        <div>
          <label>Size (sqft)</label>
          <input
            type="text"
            name="size"
            placeholder="Enter property size"
            value={formData.size}
            onChange={handleChange}
            className="p-2 rounded bg-gray-700 w-full"
          />
        </div>
      </div>
      <label>Description</label>
      <textarea
        name="description"
        placeholder="Provide a brief description"
        value={formData.description}
        onChange={handleChange}
        className="p-2 rounded bg-gray-700 col-span-2 w-full"
      ></textarea>
      <label>Address</label>
      <input
        type="text"
        name="address"
        placeholder="Street Address"
        value={formData.address}
        onChange={handleChange}
        className="p-2 rounded bg-gray-700 col-span-2 w-full"
      />
      <div className="grid grid-cols-2 gap-4 col-span-2">
        <div>
          <label>City</label>
          <input
            type="text"
            name="city"
            placeholder="Enter city"
            value={formData.city}
            onChange={handleChange}
            className="p-2 rounded bg-gray-700 w-full"
          />
        </div>
        <div>
          <label>State</label>
          <select
            name="state"
            value={formData.state}
            onChange={handleChange}
            className="p-2 rounded bg-gray-700 w-full"
          >
            <option value="">Select State</option>
            {states.map((state) => (
              <option key={state} value={state}>
                {state}
              </option>
            ))}
          </select>
        </div>
      </div>
      <div className="grid grid-cols-2 gap-4 col-span-2">
        <div>
          <label>ZIP Code</label>
          <input
            type="text"
            name="zip"
            placeholder="Enter ZIP code"
            value={formData.zip}
            onChange={handleChange}
            className="p-2 rounded bg-gray-700 w-full"
          />
        </div>
        <div>
          <label>Property Type</label>
          <select
            name="propertyType"
            value={formData.propertyType}
            onChange={handleChange}
            className="p-2 rounded bg-gray-700 w-full"
          >
            <option value="">Select Type</option>
            <option value="Condo">Condo</option>
            <option value="House">House</option>
            <option value="Apartment">Apartment</option>
            <option value="Commercial">Commercial</option>
          </select>
        </div>
      </div>
      <div className="grid grid-cols-2 gap-4 col-span-2">
        <div>
          <label>Bedrooms</label>
          <select
            name="bedrooms"
            value={formData.bedrooms}
            onChange={handleChange}
            className="p-2 rounded bg-gray-700 w-full"
          >
            <option value="">Select Bedrooms</option>
            {[...Array(10)].map((_, i) => (
              <option key={i} value={i + 1}>
                {i + 1}
              </option>
            ))}
          </select>
        </div>
        <div>
          <label>Bathrooms</label>
          <select
            name="bathrooms"
            value={formData.bathrooms}
            onChange={handleChange}
            className="p-2 rounded bg-gray-700 w-full"
          >
            <option value="">Select Bathrooms</option>
            {[...Array(10)].map((_, i) => (
              <option key={i} value={i + 1}>
                {i + 1}
              </option>
            ))}
          </select>
        </div>
      </div>
      <h3 className="text-md font-semibold col-span-2">Property Features</h3>
      <div className="grid grid-cols-2 gap-4 col-span-2">
        {featuresList.map((feature) => (
          <label key={feature} className="flex items-center gap-2">
            <input
              type="checkbox"
              checked={formData.features.includes(feature)}
              onChange={() => handleFeatureChange(feature)}
            />
            {feature}
          </label>
        ))}
      </div>
      {showImageModal && (
        <div className="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50">
          <div className="bg-gray-800 p-6 rounded shadow-md w-80">
            <h3 className="text-lg font-semibold">Upload Image</h3>
            <select
              name="imageType"
              value={selectedImageType}
              onChange={(e) => setSelectedImageType(e.target.value)}
              className="p-2 rounded bg-gray-700 w-full mt-2"
            >
              <option value="">Select Image Type</option>
              {imageCategories.map((category) => (
                <option key={category} value={category}>
                  {category}
                </option>
              ))}
            </select>
            <input
              type="file"
              onChange={(e) => setSelectedFile(e.target.files[0])}
              className="p-2 rounded bg-gray-700 w-full mt-2"
            />
            <div className="flex justify-between mt-4">
              <button
                type="button"
                onClick={() => setShowImageModal(false)}
                className="bg-red-600 py-2 px-4 rounded hover:bg-red-700"
              >
                Cancel
              </button>
              <button
                type="button"
                onClick={handleImageUpload}
                className="bg-blue-600 py-2 px-4 rounded hover:bg-blue-700"
              >
                Upload
              </button>
            </div>
          </div>
        </div>
      )}
      <div className="grid grid-cols-2 gap-4 col-span-2">
        <button
          type="button"
          onClick={() => setShowImageModal(true)}
          className="bg-green-600 py-2 px-4 rounded hover:bg-green-700 w-full"
        >
          Upload Images
        </button>
        <button type="submit" className="bg-blue-600 py-2 px-4 rounded hover:bg-blue-700 w-full">
          Submit
        </button>
      </div>
    </form>
  );
};

export default PropertyForm;

```

### Contributions Form

```jsx
import React, { useState } from "react";

const placeholderProperties = [
  "Luxury Apartment",
  "Downtown Condo",
  "Suburban House",
  "Lakefront Villa",
  "Penthouse Suite",
];

const contributionTiers = [
  "Basic",
  "Silver",
  "Gold",
  "Platinum",
  "Investor Plus",
];

const ContributionsForm = () => {
  const [formData, setFormData] = useState({
    property: "",
    amount: "",
    tier: "",
  });

  const handleChange = (e) => {
    setFormData({ ...formData, [e.target.name]: e.target.value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log("Contribution Submitted", formData);
  };

  return (
    <form onSubmit={handleSubmit} className="bg-gray-800 text-white p-6 rounded shadow-md w-96">
      <h2 className="text-lg font-semibold mb-4">Contribute to a Property</h2>
      <label>Property</label>
      <select name="property" value={formData.property} onChange={handleChange} className="p-2 rounded bg-gray-700 w-full">
        <option value="">Select a Property</option>
        {placeholderProperties.map((property) => (
          <option key={property} value={property}>{property}</option>
        ))}
      </select>
      <label className="mt-4">Contribution Amount (USD)</label>
      <input type="number" name="amount" placeholder="$1000" value={formData.amount} onChange={handleChange} className="p-2 rounded bg-gray-700 w-full" />
      <label className="mt-4">Select Tier</label>
      <div className="flex flex-col gap-2">
        {contributionTiers.map((tier) => (
          <label key={tier} className="flex items-center gap-2">
            <input type="radio" name="tier" value={tier} checked={formData.tier === tier} onChange={handleChange} />
            {tier}
          </label>
        ))}
      </div>
      <div className="flex justify-between mt-6">
        <button type="button" className="bg-red-600 py-2 px-4 rounded hover:bg-red-700">Cancel</button>
        <button type="submit" className="bg-blue-600 py-2 px-4 rounded hover:bg-blue-700">Contribute</button>
      </div>
    </form>
  );
};

export default ContributionsForm;

```