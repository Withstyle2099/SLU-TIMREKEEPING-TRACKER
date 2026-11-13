# SLU Attendance Tracker

Your own copy of the attendance tracker. The page is hosted free on **GitHub Pages**. The shared data (attendance, audit log, staff, settings) is kept in a free **Firebase** database that only signed-in people on your access list can open.

Your link will be `https://YOUR-GITHUB-NAME.github.io/slu-attendance/`, or your own domain (step 13).

## What's in the folder

| File | Upload to GitHub? | What it is |
|---|---|---|
| `index.html` | Yes | The app |
| `firebase-config.js` | Yes, after you fill it in (step 7) | Connects the app to your database |
| `firestore.rules` | No, paste it into Firebase (step 3) | Who can read and write what |
| `slu-starting-data.json` | **No, keep it private** | Settings, the 23 staff and the November SAP plan. You load it once from inside the app (step 11). |

The GitHub repository is public, so staff names and badges stay out of it. They live only in the protected database.

---

## Part A: Firebase (the database and logins). Free, no credit card.

1. **Create the project.**
   - Go to <https://console.firebase.google.com> and click **Create a project**. Name it `slu-attendance`.
   - Turn Google Analytics off, then click **Create**.
2. **Create the database.**
   - Go to **Build → Firestore Database → Create database**.
   - Pick the location closest to you. You can't change it later.
   - Choose **Start in production mode**, then click **Create**.
3. **Set the security rules.**
   - In Firestore, open the **Rules** tab and delete what's there.
   - Paste in everything from `firestore.rules`.
   - Replace `OWNER_EMAIL_HERE` with **your email in lower case**. Keep the quotes.
   - Click **Publish**.
4. **Turn on email sign-in.** Go to **Build → Authentication → Get started → Sign-in method → Email/Password**, switch on the first toggle and click **Save**.
5. **Stop strangers creating accounts.**
   - In Authentication, go to **Settings → User actions**.
   - Untick **Enable create (sign-up)** and click **Save**.
   - Now only accounts you create can sign in.
6. **Create the logins.**
   - In Authentication, go to **Users → Add user**.
   - Add yourself first, then each group leader, each with an email and a temporary password.
   - They can change their password with **Forgot password** on the sign-in screen.
7. **Get the connection settings.**
   - Click the gear icon, then **Project settings**.
   - Under **Your apps**, click the **</>** (Web) icon. Name the app `slu-attendance`, leave Firebase Hosting off, and register it.
   - Copy the six values (`apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId`, `appId`) into `firebase-config.js`, replacing each `PASTE_…`.

## Part B: GitHub (the web address). Free.

8. **Create the repository.**
   - Sign in at <https://github.com> and click **+ → New repository**.
   - Name it `slu-attendance`, set it to **Public**, and click **Create repository**.
9. **Upload the app.**
   - Click **uploading an existing file**.
   - Drag in **`index.html`** and **`firebase-config.js`** only.
   - Click **Commit changes**.
10. **Turn the website on.**
    - In the repository, go to **Settings → Pages**.
    - Under **Source**, choose **Deploy from a branch**, then branch **main** and folder **/ (root)**. Click **Save**.
    - After 1–2 minutes, Pages shows your link: `https://YOUR-GITHUB-NAME.github.io/slu-attendance/`.
    - Back in Firebase, go to **Authentication → Settings → Authorized domains → Add domain** and add `YOUR-GITHUB-NAME.github.io`.

## Part C: First run

11. **Load the starting data.**
    - Open your link and sign in with your owner account.
    - A **First run** box appears. Choose `slu-starting-data.json` and the settings, staff and November plan load.
12. **Give the group leaders access.**
    - Open **Settings → People with access**.
    - Put each group leader's email under **Editors**. Use **Viewers** for people who should only look, such as a manager.
    - Click **Save settings**.

Only people who have both a login (step 6) and a place on this list can open the data. Editors can enter attendance. Only you (the owner) can change staff and settings. Nobody can delete attendance or audit entries.

## Optional

13. **Your own domain.**
    - In GitHub, go to **Settings → Pages → Custom domain**, for example `attendance.yourdomain.com`.
    - At your domain provider, add the CNAME record that GitHub shows.
    - Add that domain under Firebase **Authorized domains** too.
14. **Updating the app later.** In GitHub, open `index.html`, click the pencil or upload a new version, and commit. The site updates in about a minute, and your data is not touched.

## Good to know

- **Cost:** Firebase's free plan allows 50,000 reads and 20,000 writes a day, far more than one unit's attendance uses.
- **Work network:** test the link from your Aramco PC first. Some company networks block `github.io` or Google/Firebase sites. If it's blocked at work, the link still works on phones over mobile data.
- **Email:** the **Daily email** tab copies the summary for you to paste into Outlook. A static site can't send email by itself.
- **Moving from the Claude version:** this copy starts from the November SAP plan. Any entries you made in the Claude version need to be re-entered.
