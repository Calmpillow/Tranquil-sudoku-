# Tranquil Sudoku — mobile-friendly setup (no SQL)

This project uses Firebase for email/password accounts and private cloud saves. GitHub Pages hosts the game. You do **not** need to run SQL or install anything on your phone.

## 1. Create the Firebase project
1. Open https://console.firebase.google.com/ in your phone browser and create a project.
2. In the project, open **Build → Authentication → Get started**.
3. Under **Sign-in method**, enable **Email/Password**, then save.
4. Open **Build → Firestore Database → Create database**. Choose production mode and a nearby region.
5. In Firestore, open the **Rules** tab. Replace the rules with the full contents of `firestore.rules`, then tap **Publish**.

## 2. Add the web app settings
1. In Firebase, open the gear icon → **Project settings** → **General**.
2. Under **Your apps**, tap the web icon (`</>`) to register a web app. Give it a name such as `Tranquil Sudoku`.
3. Firebase shows a configuration object. Copy its values into `firebase-config.js`, replacing each `YOUR_...` value. Keep the quotation marks and property names. Do not use a service-account/private key.
4. In Firebase Authentication → Settings → Authorized domains, make sure your GitHub Pages domain is listed (for example, `YOUR-USERNAME.github.io`). Add it if needed.

## 3. Upload to GitHub from your phone
1. Extract the ZIP on your phone.
2. Open your new GitHub repository in your browser.
3. Upload **all files inside the `tranquil-sudoku` folder** to the repository's root. Do not upload only the ZIP, and do not leave the files nested inside another folder.
4. Make sure `index.html`, `firebase-config.js`, `firestore.rules`, `manifest.webmanifest`, `sw.js`, and `icon.svg` are visible at the repository root.
5. In repository **Settings → Pages**, select deployment from the `main` branch and `/ (root)`.
6. Open the published Pages URL and create an account.

## How saves work
- Every account has a unique Firebase user ID.
- The game saves to `users/{userId}/private/gameState` in Firestore.
- The included Firestore rules restrict each account to its own profile and save.
- Friends can use separate email accounts, even on the same website. Signing in on another device loads that account's progress.

## Important
- Firebase has a free tier, subject to Google's current quotas and terms.
- Email/password accounts and cloud saves will not work until the Firebase project is created, the web config is added, and Firestore rules are published.
- Never upload a Firebase service-account JSON file or private server key. The web config in `firebase-config.js` is intended for browser use; the Firestore rules protect player data.
- An internet connection is required for account sign-in and cloud saving.
