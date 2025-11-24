# Student Expense Tracker (React Native + Expo + SQLite)

A mobile **Student Expense Tracker** built with **React Native**, **Expo Go**, and **SQLite**.  
The app lets you record expenses, filter them by date, see totals, and edit or delete entries.  
All data is saved locally on the device using SQLite.

---

## 📱 Features

- Add expenses with:
  - **Amount**
  - **Category** (e.g., Food, Books, Rent)
  - **Note** (optional)
- Each expense automatically gets today’s **date** (`YYYY-MM-DD`).
- **Date filters**:
  - **All** – show every expense
  - **This Week** – only expenses from the current calendar week
  - **This Month** – only expenses from the current calendar month
- **Analytics**:
  - Total spending for the current filter  
    (e.g., “Total Spending (This Month): $325.40”)
  - Spending **by category** for the current filter  
    (e.g., Food: $120, Books: $80.50, etc.)
- **Edit existing expenses**:
  - Tap **Edit** on a row to change amount, category, or note
  - Save changes or cancel
- **Delete expenses** with the ✕ button
- Data **persists** between app restarts using SQLite

---

## 🛠️ Tech Stack

- **React Native** (via Expo)
- **Expo Go**
- **expo-sqlite** (modern async API with `SQLiteProvider` and `useSQLiteContext`)
- JavaScript (functional components + hooks)

---

## 📦 Getting Started

### 1. Prerequisites

- **Node.js** (LTS version recommended)
- **Expo CLI tools** (used via `npx`)
- **Expo Go** app on your phone:
  - iOS: App Store → search **“Expo Go”**
  - Android: Google Play → search **“Expo Go”**

Your **laptop and phone must be on the same Wi-Fi network**.

---

### 2. Install Dependencies

From the project folder:

npm install

This installs React Native, Expo, expo-sqlite, and other dependencies.

---

### 3. Run the App

Start the Expo development server:


npx expo start

- You will see a QR code in the terminal or browser.

    - On Android: open Expo Go → tap Scan QR Code → scan the QR.

    - On iOS: open the Camera app → scan the QR → open in Expo Go.

If you run into cache issues, you can try:


npx expo start -c

## 🗂️ Project Structure

STUDENT-EXPENSE-TRACKER-MASTER
│
├── .expo
├── assets
├── node_modules
├── .gitignore
├── App.js
├── app.json
├── ExpenseScreen.js
├── index.js
├── package-lock.json
├── package.json
└── README.md

1. App.js

  a. Uses <SQLiteProvider databaseName="expenses.db">

  b. Renders <ExpenseScreen />

2. ExpenseScreen.js

  a. Connects to SQLite using useSQLiteContext()

  b. Creates the expenses table if it does not exist: 
     id, amount, category, note, date

  c. Handles:
    i. Adding, loading, updating, deleting expenses
    ii. Date filters
    iii. Totals and category totals
    iv. Edit form state

## ow Data Works (SQLite)
Database file: expenses.db (created automatically by Expo/SQLite)

Table: expenses

Columns:

id – INTEGER PRIMARY KEY AUTOINCREMENT

amount – REAL NOT NULL

category – TEXT NOT NULL

note – TEXT (optional)

date – TEXT NOT NULL (YYYY-MM-DD string)

Main SQLite methods (via expo-sqlite async API):

execAsync() – create table

runAsync() – INSERT, UPDATE, DELETE

getAllAsync() – SELECT all rows

## ✅ Current Functionality Checklist
 - Base expense tracker runs in Expo Go

 - SQLite table includes a date column

 - Automatically set today’s date for new expenses

 - Filters: All / This Week / This Month

 - Total spending for current filter

 - Category totals for current filter

 - Edit existing expenses (UPDATE)

 - Delete expenses (DELETE)

 - UI updates correctly after add/edit/delete/filter
