# Lost & Found Verification Platform

A secure web application where users can report lost or found items and verify the real owner before returning the item. The platform provides structured tracking, location tagging via Google Maps API, and private verification questions to prevent fake claims and ensure items are returned to their rightful owners.

## Tech Stack

### Frontend

- **Framework**: [Next.js](https://nextjs.org/) (App Router)
- **Library**: React 19
- **Styling**: Tailwind CSS v4
- **Language**: TypeScript

### Backend

- **Framework**: [Django](https://www.djangoproject.com/) 6.0.5
- **Database**: PostgreSQL (configured via environment variables) / SQLite (local dev default)
- **Language**: Python

---

## Project Structure

The repository follows a clean monorepo structure separating the client application and API services:

```text
LostnFound/
├── .env.example          # Template for environment variables
├── .gitignore            # Root Git ignore configurations
├── README.md             # Project documentation
│
├── backend/              # Django Backend Application
│   ├── config/           # Main Django project settings & routing
│   ├── claims/           # App: Claim requests, verification Q&As, handover tracking
│   ├── moderation/       # App: Admin dashboard, report approval/rejection, fraud prevention
│   ├── reports/          # App: Lost/found item listings, categories, location mapping
│   ├── users/            # App: Authentication, roles (User, Finder, Admin), profiles
│   ├── manage.py         # Django entry point script
│   └── requirements.txt  # Python dependencies
│
└── frontend/             # Next.js Frontend Application
    ├── public/           # Static assets
    ├── src/
    │   └── app/          # Next.js App Router pages and layouts
    ├── package.json      # Node dependencies & scripts
    ├── tailwind.config   # Tailwind CSS setup
    └── tsconfig.json     # TypeScript configuration
```

---

## Backend Architecture & Modules

The backend logic is modularized into distinct Django apps aligning with core system features:

- **`reports`**: Handles the creation and querying of lost and found items. Includes details like item categories, date/time, description, and geographical coordinates.
- **`claims`**: Manages the verification workflow where potential owners answer private verification questions (e.g., hidden item contents, specific visual markers) before approval.
- **`moderation`**: Dedicated toolset for administrators to review flagged posts, verify high-value items, and oversee user activity.
- **`users`**: Handles user authentication, profile data, and access permissions across the platform's user roles.

---

## Getting Started

### Prerequisites

- **Node.js** (v18+ recommended)
- **Python** (v3.10+ recommended)
- **PostgreSQL** (Optional for local testing if using SQLite)

### 1. Environment Setup

Clone the repository and prepare your environment configuration:

```bash
cp .env.example .env
```

Update the `.env` file with your specific database credentials and secret keys.

### 2. Backend Setup

Navigate to the backend directory, set up your virtual environment, and apply migrations:

```bash
cd backend
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Run database migrations
python manage.py migrate

# Start the development server
python manage.py runserver
```

The Django backend API will be accessible at `http://127.0.0.1:8000/`.

### 3. Frontend Setup

Open a new terminal, navigate to the frontend directory, install dependencies, and start the development server:

```bash
cd frontend
npm install

# Start the development server
npm run dev
```

The Next.js application will be running at `http://localhost:3000/`.
