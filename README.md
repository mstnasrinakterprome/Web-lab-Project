# Mess Management System

A modern full-stack **Mess Management System** for managing hostel/mess members, meals, expenses, monthly billing, payment requests, meal preferences, notices, and manager selection.

## ✨ Key Features

### 👨‍💼 Admin Panel
- Secure admin authentication
- Dashboard with mess and financial overview
- Member management
- Daily meal management
- Meal preference management
- Bazar and expense management
- Monthly meal-rate calculation
- Monthly rent, utility, and other cost distribution
- Member due and balance calculation
- Payment request verification
- bKash Transaction ID review
- Payment approval/rejection
- Manager lottery
- Notices and announcements
- Theme/settings management

### 👤 Member Panel
- Secure member authentication
- Personal dashboard
- View meal information
- Submit meal preferences
- View monthly bill
- View meal, rent, utility, and other charges
- View paid amount, due, and advance
- Submit payment requests
- bKash payment with Transaction ID
- Payment status and payment history
- View notices

## 💳 Payment System

The project supports a manual payment verification workflow.

### Member Flow

```text
Member
  ↓
Check Current Due
  ↓
Select Payment Method
  ↓
Enter Amount
  ↓
For bKash → Enter Transaction ID
  ↓
Submit Payment Request
  ↓
Payment Status = Pending
````

### Admin Flow

```text
Pending Payment
  ↓
Admin Reviews
  ├── Member
  ├── Amount
  ├── Payment Method
  └── Transaction ID
  ↓
Approve / Reject
  ↓
Payment Status Updated
  ↓
Member Balance Updated
```

For bKash payments, the member enters the actual **bKash Transaction ID**. The transaction record is stored in the `payment_transactions` table and remains `pending` until the admin verifies it.

## 🍚 Monthly Meal Rate

The monthly meal rate is calculated from the month's bazar expenses and actual meals:

```text
Meal Rate = Total Bazar Expense ÷ Total Actual Meals
```

Example:

```text
Total Bazar = BDT 800
Total Meals = 5

Meal Rate = 800 ÷ 5
          = BDT 160
```

After the monthly rate is calculated:

```text
Meal Charge = Member Meal Count × Meal Rate
```

The member's meal charge is then combined with applicable rent, utility, other charges, and previous outstanding balance.

## 🛒 Bazar / Expense Management

Bazar amounts are entered from:

**Admin Panel → Expenses → Add Expense**

Each expense contains:

* Description
* Amount
* Date
* Category

Expenses categorized as **bazar** are included in the monthly meal-rate calculation.

Example:

```text
Bazar 1 = BDT 300
Bazar 2 = BDT 200
Bazar 3 = BDT 300
--------------------
Total Bazar = BDT 800
```

## 🧮 Billing Logic

### Meal Charge

```text
Meal Charge = Meal Count × Monthly Meal Rate
```

### Member Total

```text
Member Total =
Meal Charge
+ Rent / Utility / Other Charges
+ Previous Outstanding Balance
```

### Payment Balance

```text
Balance = Total Due - Verified Paid Amount
```

Verified payments update the member's payment totals and remaining balance through the database payment logic.

## 🛠️ Technology Stack

### Frontend

* React 18
* TypeScript
* Vite
* Tailwind CSS
* React Router
* Framer Motion
* Lucide React

### Backend / Database

* Supabase
* PostgreSQL
* Supabase Auth
* Row Level Security (RLS)
* PostgreSQL Functions
* PostgreSQL Triggers

## 🏗️ Architecture

```text
React + TypeScript
        │
        ▼
   Supabase Client
        │
        ▼
   Supabase Auth
        │
        ▼
Supabase PostgreSQL
        │
        ├── Members
        ├── Meals
        ├── Meal Records
        ├── Meal Preferences
        ├── Expenses
        ├── Monthly Meal Rates
        ├── Monthly Costs
        ├── Member Dues
        └── Payment Transactions
```

## 📁 Project Structure

```text
Web-lab-Project/
├── src/
│   ├── components/
│   │   ├── admin/
│   │   └── member/
│   ├── context/
│   ├── lib/
│   ├── pages/
│   │   ├── admin/
│   │   └── member/
│   ├── App.tsx
│   └── main.tsx
│
├── supabase/
│   ├── functions/
│   └── migrations/
│
├── package.json
├── postcss.config.js
└── README.md
```

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/mstnasrinakterprome/Web-lab-Project.git
cd Web-lab-Project
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

Create a `.env` file in the project root:

```env
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

Do not commit real environment secrets to GitHub.

### 4. Start the Development Server

```bash
npm run dev
```

Open:

```text
http://localhost:5173
```

## 📦 Available Scripts

```bash
npm run dev
npm run build
npm run lint
npm run typecheck
npm run preview
```

## 🗄️ Supabase Setup

SQL migrations are stored in:

```text
supabase/migrations/
```

They contain the project's database schema and logic for:

* Members and admins
* Meals and meal records
* Meal preferences
* Expenses and bazar
* Monthly meal rates
* Monthly costs and allocations
* Member dues
* Payment transactions
* RLS policies
* Database functions
* Payment triggers

Apply the migrations to the Supabase project before using the application.

## 🔐 Security

* Authentication is handled with Supabase Auth.
* Admin and member routes are protected.
* RLS policies restrict access to authorized hostel/member data.
* Payment records contain a unique transaction ID.
* Payment verification changes the payment status rather than treating a submitted request as automatically paid.
* Environment variables should not be exposed in source control.

## 📌 Main Database Tables

The project includes database support for:

```text
admins
members
meals
meal_records
meal_preferences
expenses
meal_rates
monthly_meal_rates
monthly_costs
monthly_cost_allocations
member_dues
payment_transactions
```

## 🎯 Purpose

The goal of this project is to provide a practical digital solution for hostel and mess management by centralizing:

**Members + Meals + Expenses + Monthly Billing + Payments + Administration**

It reduces manual calculation and provides a clear workflow for monthly meal-rate calculation and payment verification.

## 📜 License

This project is intended for academic and educational use.

## 👨‍💻 Author

**Prome and teams**

Bachelor of Science in Computer Science and Engineering
Southeast University, Dhaka


