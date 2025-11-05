AI Powered Fitness & Lift Tracker

This is a powerful, single-file web application designed to help users manage their nutrition (calories and macronutrients) and track their strength training progress (lifts). It features real-time data storage using Google Firestore and leverages the Gemini API for intelligent, camera-based food analysis.

✨ Features

Daily Macro & Calorie Tracking: Set goals and track Calorie and Protein intake in real-time.

AI Food Analysis: Use the Camera Scan or AI Search tab to describe a meal or take a photo, and the AI will estimate the macros.

Manual Entry: Quickly log food manually with detailed macro counts.

Real-Time Lift Recording: Record specific exercises, weights, and reps.

Weekly Progress Summary: Automatically identifies and tracks the user's maximum weight lifted for core exercises each week, encouraging progressive overload.

Historical Progress: View macro and lift trends grouped by week or month.

Persistent Storage: All data (logs, lifts, and goals) is stored securely in Google Firestore.

🛠️ Configuration & Setup (Mandatory)

This application is designed to run entirely client-side (in the browser), but requires two API keys to connect to the backend services.

Prerequisites

Firebase Project: A configured Firebase project with Firestore Database and Anonymous Authentication enabled.

Gemini API Key: A key obtained from Google AI Studio for the AI food analysis feature.

Step 1: Update Firebase Configuration

Your Firebase configuration is already in the Canvas, but you need to ensure the Gemini API Key is added.

Open the index.html file and locate the configuration block around line 17:

// --- YOUR CONFIGURATION START ---
// 1. YOUR FIREBASE CONFIGURATION OBJECT IS PLACED HERE
const YOUR_FIREBASE_CONFIG = {
    // ... (Your Firebase Config details are already here)
};

// 2. PASTE YOUR GEMINI API KEY HERE (If running outside of Canvas)
const GEMINI_API_KEY = ""; // !!! REPLACE "" WITH YOUR ACTUAL GEMINI API KEY for AI features to work. !!!

// --- YOUR CONFIGURATION END ---


Action: Replace the empty quotes ("") on the GEMINI_API_KEY line with your actual key.

Step 2: Set Database Rules (Security)

To prevent the "Auth Error" and ensure only authenticated users can access the database, you must publish the following simple security rules in your Firebase Console (Firestore Database > Rules Tab):

rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      // Allows read and write access only to authenticated users (signed in anonymously).
      allow read, write: if request.auth != null;
    }
  }
}


🚀 Deployment (Hosting)

Since the application uses advanced features like the Camera API and secure external connections, it must be hosted on a secure web server (HTTPS).

The recommended free deployment method is GitHub Pages:

Commit the fully configured index.html file (with both keys) to a GitHub repository.

Go to Settings > Pages in your repository.

Set the deployment source to the main branch and the folder to / (root).

GitHub will provide you with a secure HTTPS link to access your tracker on any device.
