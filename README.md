# Student Expense Tracker (React Native + Expo + SQLite + Charts)

A mobile **Student Expense Tracker** built with **React Native**, **Expo Go**, and **SQLite**.  
The app lets you record expenses, filter them by date, see totals, edit or delete entries, and includes a **Spending by Category bar chart** using real SQLite data.  
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
  - **NEW:** Bar chart visualization of category totals
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
- **react-native-chart-kit** (bar chart)
- JavaScript (functional components + hooks)

---

## 📦 Getting Started

### 1. Prerequisites
- **Node.js**
- **Expo CLI** (via `npx`)
- **Expo Go** mobile app
- Laptop & phone must be on the **same Wi-Fi network**

---

### 2. Install Dependencies
```bash
npm install
```
This installs React Native, Expo, expo-sqlite, and other dependencies.

---

### 3. Run the App

Start the Expo development server:

```bash
npx expo start
```
- You will see a QR code in the terminal or browser.

    - On Android: open Expo Go → tap Scan QR Code → scan the QR.

    - On iOS: open the Camera app → scan the QR → open in Expo Go.

If you run into cache issues, you can try:

```bash
npx expo start -c
```
## 🗂️ Project Structure
```bash
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
    v. Chart data preparation + rendering
```
## How Data Works (SQLite)
Database file: expenses.db (created automatically by Expo/SQLite)

Table: expenses
```bash
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
```
## Spending by Category Chart

- The app now includes a bar chart showing spending by category.

Key Behaviors:

 - Uses real data from categoryTotals

 - Labels = category names

 - Values = total spending per category

 - Chart width uses: Dimensions.get("window").width - 32

 - Automatically updates when:

 - Adding an expense

 - Editing an expense

 - Deleting an expense

 - Changing filters (All / Week / Month)

## GitHub Copilot Reflection
## How I Used Copilot

I used comments as prompts for Copilot. Example:
```bash
// spending chart data preparation:
// REQUIREMENTS:
// - use categoryTotals for labels + totals
// - shorten long labels
// - build chartData for react-native-chart-kit
// - handle empty dataset
// - use Dimensions for responsive width
```

Copilot generated:

- chartLabels

- chartValues

- full chartData structure

- Dimensions sizing logic

For rendering the UI:
```bash
{/* chart UI:
    REQUIREMENTS:
    - render BarChart
    - match dark theme
    - include title
    - maintain spacing
*/}
```

This produced a working chart component I refined.

## Copilot Suggestions I Rejected

Copilot initially suggested dummy values like:
```bash
labels: ['Food','Rent']
datasets: [{ data: [200,350] }]
```

I rejected this because:

- Assignment requires real app data

- I already calculate categoryTotals dynamically

I replaced dummy values with:
``` bash
categoryTotals.map(([cat,total]) => ...)
```
### Where Copilot Saved Time

- Generating chart JSX

- Providing chartConfig structure

- Completing .map() transformations

- Speeding repetitive component patterns

I still manually verified and modified all code.

## ✅ Current Functionality Checklist
 - Base expense tracker runs in Expo Go

 - SQLite table includes a date column

 - Automatically set today’s date for new expenses

 - Filters: All / This Week / This Month

 - Total spending for current filter

 - Category totals for current filter

 - Category bar chart implemented

 - Edit existing expenses (UPDATE)

 - Delete expenses (DELETE)

 - UI updates correctly after add/edit/delete/filter
