# ⚡ Mwangaza Electricals & Hardware — Point of Sale (POS) System

A full-featured, Kenyan-friendly **Point of Sale web application** built for electrical hardware retail stores. Designed around the real-world workflow of Nairobi electrical shops (River Road, Kirinyaga Road, Luthuli Avenue), with **Lipa na M-Pesa checkout simulation**, **Fundi (technician) commission tracking**, **KRA eTIMS-style fiscal receipts**, **multi-cashier PIN login**, and **downloadable stock valuation reports (PDF & Excel)**.

![Tech Stack](https://img.shields.io/badge/Next.js-16-black) ![React](https://img.shields.io/badge/React-19-blue) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Drizzle%20ORM-336791) ![Tailwind](https://img.shields.io/badge/Tailwind-CSS%204-38B2AC) ![TypeScript](https://img.shields.io/badge/TypeScript-5.9-3178C6)

---

## ✨ Core Features

| Module | Description |
|---|---|
| 🛒 **POS Terminal** | Searchable product catalog (cables, lighting, switches, breakers, conduits), category filters, stock-level progress meters, cart with quantity controls, discounts & VAT |
| 📱 **M-Pesa Checkout** | STK Push simulation, M-Pesa transaction code entry (e.g. `RKS928SDJ4`), customer phone capture, Paybill/Till configuration — plus a **live Safaricom SMS stream simulator** with click-to-autofill transaction referrals |
| 🔐 **Multi-User Login** | Role-based cashier/manager accounts with 4-digit POS PIN lock screen, instant shift-switch sign-out, and operator names printed on receipts |
| 👷 **Fundi Loyalty Program** | Register local electricians ("fundis"), attach them to sales, auto-calculate referral commissions (default 3%), track pending balances and record M-Pesa/cash payouts |
| 📦 **Inventory Management** | Full product CRUD, quick restock, low-stock alerts, wholesale cost vs retail price tracking, live stock valuation |
| 📊 **Stock Reports** | One-click **PDF** (jsPDF + autotable) and **Excel `.xlsx`** (SheetJS) downloads of the complete stock audit & valuation report |
| 🧾 **eTIMS-Style Receipts** | KRA PIN on receipts, fiscal signature block, SD serial number, invoice numbering, print simulation, Swahili thank-you tagline |
| 💸 **Expenses Ledger** | Track daily overheads — transport, KPLC utilities, staff meals, KRA permits, stationery |
| 🏦 **Payment Modes** | M-PESA, Cash (with change calculator), Bank transfer slip, and Store Credit (debt ledger) |
| ⚙️ **Store Settings** | Customize store name, branch, address, phone, KRA PIN, receipt tagline, currency symbol, VAT rate & toggle, M-Pesa Paybill/Till defaults, fundi commission rate, and voice feedback prompts |
| 📜 **Sales History** | Full invoice ledger with operator attribution, payment mode badges, and receipt reprint |
| 🔊 **Voice Confirmations** | Optional Text-to-Speech payment confirmations via the Web Speech API |

---

## 🛠️ Tech Stack

- **Framework:** Next.js 16 (App Router, Turbopack) + React 19
- **Language:** TypeScript 5.9
- **Database:** PostgreSQL + Drizzle ORM 0.45 (drizzle-kit push)
- **Styling:** Tailwind CSS 4
- **Icons:** Lucide React
- **Reports:** jsPDF + jspdf-autotable (PDF), SheetJS xlsx (Excel)

---

## 🚀 Getting Started

### 1. Clone & Install

```bash
git clone https://github.com/<your-username>/mwangaza-pos.git
cd mwangaza-pos
npm install
```

### 2. Configure the Database

Create a PostgreSQL database, then copy the environment template:

```bash
cp .env.example .env
```

Edit `.env` with your connection string:

```env
DATABASE_URL=postgresql://postgres:postgres@127.0.0.1:5432/app_db
```

> Works with local Postgres, Supabase, Neon, Railway, or any hosted PostgreSQL.

### 3. Push the Schema

```bash
npx drizzle-kit push
```

This creates all tables: `users`, `products`, `fundis`, `sales`, `sale_items`, `expenses`, `settings`.

### 4. Run the App

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000). On first load, the app **auto-seeds** the database with 17 realistic electrical products, 4 fundis, 3 cashiers, expenses, and a sample sale via `/api/setup`.

### 5. Log In with Demo Accounts

| Name | Role | Username | PIN |
|---|---|---|---|
| James Mwangi | Admin / Manager | `mwangi` | **1234** |
| Amina Omondi | Cashier | `amina` | **5555** |
| Josphat Kamau | Cashier | `josphat` | **8888** |

> 💡 Use **"Reset Mock Data"** in Settings/Header anytime to wipe and re-seed the demo dataset.

---

## 📂 Project Structure

```
src/
├── app/
│   ├── api/
│   │   ├── products/route.ts   # Product CRUD + restock
│   │   ├── sales/route.ts      # Checkout: stock deduction, invoice gen, fundi commission
│   │   ├── fundis/route.ts     # Technician CRUD + commission payouts
│   │   ├── expenses/route.ts   # Overhead logging
│   │   ├── users/route.ts      # Staff accounts & PINs
│   │   ├── settings/route.ts   # Singleton store settings row (GET/PUT)
│   │   ├── setup/route.ts      # Auto-seed + demo reset endpoint
│   │   └── health/route.ts     # Healthcheck
│   ├── layout.tsx
│   ├── page.tsx                # Full POS client (login lock, tabs, checkout, modals)
│   └── globals.css
└── db/
    ├── index.ts                # pg Pool + drizzle client (DATABASE_URL)
    └── schema.ts               # 7 tables: users, products, fundis, sales, sale_items, expenses, settings
```

---

## 🌩️ Deployment

### Vercel (recommended)

1. Push this repo to GitHub.
2. Import into [Vercel](https://vercel.com/new).
3. Add the `DATABASE_URL` environment variable (e.g. Neon/Supabase connection string).
4. Deploy — then run `npx drizzle-kit push` locally against your production DB once.

---

## ✅ Quality Checks

```bash
npx next typegen        # Route types
npm exec tsc -- --noEmit --pretty false   # TypeScript
npm run build           # Production build
```

---

## 📄 License

MIT — see [LICENSE](./LICENSE). Built with ❤️ for Kenyan retail businesses 🇰🇪.

*Asante kwa biashara yako! Karibu tena!* ⚡
