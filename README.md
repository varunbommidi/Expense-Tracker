Expense Tracker

<h6 align="center">Made by Varun</h6>

A web-based personal finance application designed to track and analyze your expenses. This app uses Firebase Firestore for secure, real-time data storage, allowing you to manage your finances from any browser.

Features

Add Transactions: Quickly add new expenses with details like amount, date, category, payment method, and the person who made the purchase.

Manage Settings: Easily add or delete custom categories, payment methods (e.g., "HDFC Card", "PayTM"), and people (e.g., "Varun", "Friend").

Detailed Transactions: View all your transactions in a filterable list. You can filter by a date range, specific payment method, or person to see exactly where your money is going.

Analytics Dashboard: Get a clear visual breakdown of your spending. The app provides summaries "By Category", "By Payment", and "By Person". Clicking on any summary item shows a detailed list of just those transactions.

Persistent Data: All your data is securely saved to your personal Firebase Firestore database, so it's always available and up-to-date.

Tech Stack

Frontend: HTML5, Tailwind CSS, JavaScript (ES6 Modules)

Database: Google Firebase (Firestore for data, Firebase Auth for user handling)

Icons: Lucide Icons

How to Set Up and Run

To run this project, you must connect it to your own Firebase database.

1. Get the Code

Download or copy the expense-tracker.html file to your local computer.

2. Create a Firebase Project

Go to the Firebase Console.

Click "Add project" and give it a name (e.g., "My-Expense-Tracker").

(Optional) You can disable Google Analytics to speed up the setup.

Once your project is created, you need to add a Firestore database.

3. Set Up Firestore Database

In your Firebase project, go to Build > Firestore Database (from the left-side menu).

Click "Create database".

Select "Start in production mode".

Choose a location for your database (e.g., asia-south1 for Mumbai) and click "Enable".

4. Add Security Rules

Your database needs rules to allow you (and only you) to write data.

In the Firestore Database section, click the "Rules" tab.

Delete all the existing text (the default rules).

Copy and paste the following rules into the editor:

rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow users to read and write only their own data
    match /artifacts/{appId}/users/{userId}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}


Click "Publish".

5. Get Your Firebase Config Keys

Go back to your Project Overview by clicking the Gear icon next to "Project Overview" and selecting "Project settings".

In the "Your apps" card, click the Web icon (</>) to register a new web app.

Give it a nickname (like "Tracker Web App") and click "Register app".

Firebase will show you a const firebaseConfig = { ... } object. Copy this entire object.

6. Add Config to expense-tracker.html

Open your expense-tracker.html file in a code or text editor.

Find the section that looks like this (around line 430):

// --- !!! IMPORTANT !!! ---
// PASTE YOUR FIREBASE CONFIG OBJECT HERE
// ...
const userFirebaseConfig = {
    // apiKey: "YOUR_API_KEY",
    // authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    // ...
};


Paste your firebaseConfig object from Step 5 into the userFirebaseConfig variable.

Save the file. You can now open expense-tracker.html directly in Chrome, and it will connect to your database!

How to Deploy to Netlify

You can host this app for free on Netlify in just a few steps.

On your computer, create a new folder (e.g., expense-app).

Move your expense-tracker.html file into this new folder.

Rename the file from expense-tracker.html to index.html.

Go to your Netlify dashboard.

Drag and drop the entire expense-app folder onto the "Sites" page.

Netlify will automatically build and deploy your site, giving you a live, shareable URL.
