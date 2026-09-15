# Sartors Central

A static GitHub Pages family planner using Firebase Anonymous Authentication and Firestore.

## Files

- `index.html` — application entry page
- `styles.css` — responsive production UI
- `app.js` — Firebase app, real-time Firestore data, calendar, meals, lists, requests
- `firebase-rules.txt` — Firestore Security Rules to publish

## Run locally

The app uses JavaScript modules, so serve the directory through a local web server rather than opening `index.html` as a file.

```bash
cd sartors-central
python -m http.server 8080
```

Then open `http://localhost:8080`. You can also use VS Code Live Server or any static development server.

## Firebase setup

1. Open the Firebase Console for project `sartors-central`.
2. Go to **Authentication → Sign-in method** and enable **Anonymous**.
3. Go to **Firestore Database** and create a database in production mode, choosing the region closest to the family.
4. Go to **Firestore Database → Rules**, paste all contents of `firebase-rules.txt`, and publish.
5. In **Authentication → Settings → Authorized domains**, add your GitHub Pages host, such as `YOUR-USERNAME.github.io`. Add `localhost` for local testing if it is not already present.

The supplied Firebase web configuration is already included in `app.js`.

## Deploy to GitHub Pages

This is a plain static app, so no build step or base-path configuration is required.

1. Create a GitHub repository, for example `sartors-central`.
2. Upload the contents of this folder to the repository root: `index.html`, `styles.css`, and `app.js` (the README and rules file are useful to keep too).
3. In GitHub, open **Settings → Pages**.
4. Under **Build and deployment**, choose **Deploy from a branch**, select `main`, and select `/ (root)`.
5. Save. The site will be available at `https://YOUR-USERNAME.github.io/sartors-central/`.
6. Add `YOUR-USERNAME.github.io` to Firebase Authentication's authorized domains before using sign-in on the deployed site.

## Important security note

Anonymous authentication and client-side identity choice provide practical household-level access control, not strong identity verification. Anyone who can use a previously enrolled browser can act as that selected person; someone technically sophisticated could also manipulate client requests. This is appropriate for a trusted private family planner, but it is not suitable for sensitive or high-security records.

The first device that chooses a role registers its anonymous Firebase UID under that role. The rules then distinguish Charlie from the three editing roles. For a stronger setup, replace anonymous authentication with individual passwordless or email accounts.
