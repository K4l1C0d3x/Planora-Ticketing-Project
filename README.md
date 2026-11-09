# Planora Tickets

A modern, full-stack event management and ticketing platform built with Next.js, TypeScript, Tailwind CSS, Supabase, and Razorpay.

## Overview

Planora is an end-to-end ticketing solution engineered for event organizers and attendees. It facilitates event discovery, online ticket purchases with instant Razorpay checkout, automated generation of tamper-resistant QR-coded PDF tickets, on-site ticket scanning and validation, organizer analytics, and an integrated Gemini-powered AI event concierge.

## Key Features

### Attendee Experience
- **Event Discovery**: Responsive catalog of upcoming conferences, workshops, and meetups with detailed schedules, venue mapping, and ticket tier selection.
- **Secure Online Payments**: Integrated Razorpay checkout workflow with client-side modal integration and server-side cryptographic signature verification.
- **Instant Digital Tickets**: Automated generation of branded PDF tickets containing encrypted QR codes immediately after payment confirmation.
- **Transactional Email Dispatch**: Immediate delivery of tickets and event confirmations with PDF attachments via SMTP / Nodemailer.
- **Ticket Self-Service**: Attendee portal (`/my-tickets`) allowing users to look up and download purchased tickets via passwordless OTP authentication.
- **AI Event Concierge**: Interactive conversational assistant powered by the Google Gemini API (`gemini-1.5-flash`) to answer attendee queries in real time.

### Organizer & Host Management
- **Event Creation & Configuration**: Comprehensive editor for hosting events, setting ticket prices, participant quotas, dates, and locations.
- **Real-Time Analytics**: Visual tracking of ticket sales velocity, revenue generation, attendee demographics, and check-in rates.
- **Attendee Management**: Searchable attendee registries with exportable guest lists and manual check-in overrides.
- **Custom Email Templates**: Interface to configure and preview automated ticket confirmation emails.

### Verification & Check-in Operations
- **On-Site QR Verification Portal**: Camera-based and manual QR code scanner (`/verify`) for gate staff to validate tickets and prevent duplicate entries.
- **Live Check-in Synchronization**: Instant database status updates to record attendance timestamps in Supabase.

### Administration & Platform Security
- **Admin Control Center**: Unified dashboard (`/admin`) for platform-wide metrics, system health auditing, and transaction logs.
- **Role-Based Access Control**: Strict access boundaries separating regular attendees, event organizers, and super administrators.
- **Row-Level Security (RLS)**: Enforced PostgreSQL security policies in Supabase ensuring data isolation across event hosts.

## Technology Stack

- **Frontend**: Next.js 16 (Pages Router), React 18, TypeScript 5
- **Styling & UI**: Tailwind CSS, Framer Motion, Lucide React, React Hot Toast
- **Database & Backend Services**: Supabase (PostgreSQL, Row-Level Security, Supabase Storage)
- **Payment Gateway**: Razorpay Node.js SDK
- **Document & QR Generation**: PDFKit, node-qrcode
- **Email Delivery**: Nodemailer (SMTP / Gmail / Resend compatible)
- **Artificial Intelligence**: Google Gemini API (`@google/generative-ai`)
- **Telemetry**: Vercel Analytics

## Project Structure

```text
Planora-Ticketing-Project/
├── pages/
│   ├── api/                    # Serverless API routes
│   │   ├── admin/              # Administrative analytics & session endpoints
│   │   ├── organizer/          # Event management & template endpoints
│   │   ├── otp/                # One-time passcode generation & verification
│   │   ├── create-order.ts     # Razorpay order generation
│   │   ├── verify-payment.ts   # Cryptographic payment signature validation
│   │   ├── ticket-pdf.ts       # On-the-fly PDF generation
│   │   └── chat.ts             # Google Gemini AI assistant endpoint
│   ├── event/[id].tsx          # Public event details & ticket booking
│   ├── organizer.tsx           # Organizer management console
│   ├── admin.tsx               # Platform admin portal
│   ├── my-tickets.tsx          # Attendee ticket lookup dashboard
│   ├── verify.tsx              # On-site QR ticket scanning terminal
│   └── index.tsx               # Homepage & event catalog
│
├── components/                 # Reusable UI components and layouts
├── lib/                        # Supabase client, Razorpay helper, email service
├── styles/                     # Tailwind CSS and global style definitions
├── supabase/                   # Supabase schema definitions and migrations
├── types/                      # TypeScript interface declarations
├── .env.example                # Environment configuration template
└── package.json                # Project dependencies and run scripts
```

## Getting Started

### Prerequisites

- Node.js 18.x or 20.x
- npm, yarn, or pnpm
- Supabase account and project
- Razorpay account (Test mode or Live)
- Google Gemini API key (for AI assistant)
- SMTP credentials (Gmail, SendGrid, or Resend)

### Installation

1. **Clone the repository**:
   ```bash
   git clone https://github.com/K4l1C0d3x/Planora-Ticketing-Project.git
   cd Planora-Ticketing-Project
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Configure Environment Variables**:
   Copy the example environment configuration:
   ```bash
   cp .env.example .env.local
   ```
   Populate `.env.local` with your service credentials:

   ```env
   # Supabase
   NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
   SUPABASE_SERVICE_KEY=your_supabase_service_role_key

   # Razorpay
   NEXT_PUBLIC_RAZORPAY_KEY_ID=rzp_test_your_key_id
   RAZORPAY_KEY_SECRET=your_razorpay_key_secret

   # Email Service (SMTP)
   EMAIL_PROVIDER=smtp
   EMAIL_FROM=noreply@planora.app
   SMTP_HOST=smtp.gmail.com
   SMTP_PORT=465
   SMTP_USER=your_email@gmail.com
   SMTP_PASS=your_app_password

   # Admin Configuration
   ADMIN_SECRET=your_secure_admin_passphrase
   ADMIN_SESSION_TTL=3600

   # AI Assistant
   GEMINI_API_KEY=your_google_gemini_api_key

   # Application Base URL
   BASE_URL=http://localhost:3000
   ```

4. **Initialize Database Schema**:
   Execute the SQL statements from `supabase_schema.sql` in your Supabase SQL Editor to provision tables, triggers, and Row-Level Security policies.

5. **Run the Development Server**:
   ```bash
   npm run dev
   ```
   Open `http://localhost:3000` in your browser.

## Build and Deployment

To produce an optimized production build:

```bash
npm run build
npm run start
```

### Deploying to Vercel

1. Push your repository to GitHub.
2. Import the project into the [Vercel Dashboard](https://vercel.com/).
3. Add all variables defined in `.env.local` into the Vercel Environment Variables settings.
4. Deploy.

## Author

Developed by **Kalidas KJ**.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
