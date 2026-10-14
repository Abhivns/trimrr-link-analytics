# Trimrr — Full-Stack URL Shortener & Analytics Platform

A production-grade, full-stack URL management and analytics web application built with **React.js (Vite)**, **Tailwind CSS**, **Shadcn UI**, and **Supabase (PostgreSQL)**. Users can shorten long URLs, customize back-half slugs, generate downloadable QR codes, and monitor real-time click telemetry (device split and geolocation).

## 🚀 Key Features

- **Seamless Onboarding Flow:** Captures unauthenticated link requests via URL search parameters (`?createNew=`) and automatically resumes link creation post-login.
- **Custom Slugs & Auto-Generated Short Links:** Supports unique user-defined aliases alongside base-36 collision-resistant short codes.
- **Dynamic QR Code Engine:** Renders client-side HTML5 Canvas QR codes, converts them asynchronously into binary `Blob` objects, and uploads them to cloud storage.
- **Real-Time Click Telemetry:** Tracks visitor geolocation (City/Country) and device type (Mobile vs. Desktop via `ua-parser-js`) upon redirection, visualized with responsive **Recharts** line and pie charts.
- **Role-Based Database Security:** Enforces PostgreSQL **Row-Level Security (RLS)** policies and relational `ON DELETE CASCADE` constraints for automated data cleanup.

---

## 🛠️ Tech Stack

| Layer | Technologies |
| :--- | :--- |
| **Frontend** | React 18 (Vite), React Router DOM v6 (`createBrowserRouter`), Context API |
| **Styling & UI** | Tailwind CSS, Shadcn UI, Lucide React Icons, React Spinners |
| **Backend & DB** | Supabase (PostgreSQL, Supabase Auth, Supabase Storage Buckets) |
| **Utilities & Charts** | Recharts, Yup (Schema Validation), `react-qrcode-logo`, `ua-parser-js` |

---

## 🏗️ System Architecture Highlights

1. **Custom Asynchronous Hook (`useFetch`):** Centralizes `data`, `loading`, and `error` state management across all Supabase API interactions to keep UI components declarative.
2. **Database Schema & RLS Policies:**
   - `urls` table: Restricted `SELECT`, `INSERT`, and `DELETE` operations strictly to authenticated resource owners (`auth.uid() = user_id`).
   - `clicks` table: Configured public `INSERT` permissions so anonymous visitors trigger analytics during redirection, while restricting `SELECT` access to authenticated users.
3. **Storage Buckets:** Dedicated public buckets (`profile_pic` and `qrs`) with granular upload and read policies.

---
