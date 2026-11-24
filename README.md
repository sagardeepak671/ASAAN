# ASAAN (HandyHive)

> **On-Demand Home Services Platform** — Connect with trusted local professionals for plumbing, electrical, cleaning, and painting services.

[![Deploy ASAAN to GitHub Pages](https://github.com/sagardeepak671/ASAAN/actions/workflows/pages.yml/badge.svg)](https://github.com/sagardeepak671/ASAAN/actions/workflows/pages.yml)
[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-brightgreen)](https://sagardeepak671.github.io/ASAAN/)

## 🚀 Live Demo — Run Anywhere from Your Browser

You can run and test ASAAN directly on your phone, tablet, or desktop browser with zero installation:

🔗 **[https://sagardeepak671.github.io/ASAAN/](https://sagardeepak671.github.io/ASAAN/)**

- **Customer Experience:** Browse verified local service providers by PIN code (e.g. `110075`), request visits, simulate quotes, and test checkout.
- **Worker Experience:** Sign in to view and accept incoming jobs, share live arrival estimates, manage service areas, and acknowledge payments.
- **Offline & Cross-Platform:** Powered by Expo and React Native Web with an interactive client-side demo state that runs entirely in the browser.

---

## 🌐 Deploy to GitHub Pages (Automated via GitHub Actions)

This repository includes a pre-configured GitHub Actions workflow in [`.github/workflows/pages.yml`](.github/workflows/pages.yml) that builds and deploys the web app automatically.

### One-Time Setup in Your GitHub Repository:
1. Go to your repository on GitHub: **[https://github.com/sagardeepak671/ASAAN](https://github.com/sagardeepak671/ASAAN)**
2. Click **Settings** (top tab).
3. On the left sidebar, click **Pages** (under *Code and automation*).
4. Under **Build and deployment** → **Source**, select **GitHub Actions**.
5. Every push to the `main` branch will automatically trigger the build and deploy pipeline.
6. Your live link will always be: **`https://sagardeepak671.github.io/ASAAN/`**

To trigger a manual deployment at any time:
- Go to the **Actions** tab on GitHub → select **Deploy ASAAN to GitHub Pages** → click **Run workflow**.

---

## 📱 Open on Your Phone (Local or Hosted)

### Production Hosting (Full Stack with API & Database)

[Deploy ASAAN to Render](https://render.com/deploy?repo=https://github.com/sagardeepak671/ASAAN). Review the Starter service and persistent disk before approving. Enter your Twilio API key SID, API secret, and Verify service SID in the secret fields. The Docker build serves the website and API at one HTTPS origin. SQLite stores accounts and bookings in the attached disk.

After deployment, open the Render URL on your phone. Choose **Customer** or **Worker** and sign in by SMS. Workers must complete the verification process and publish their service PINs before customers can book them. See the [operator guide](SECURITY_AND_LAUNCH.md). To check a deployment, set `EXPO_PUBLIC_HANDYHIVE_API_URL` to its HTTPS origin followed by `/api/v1` and run `node scripts/check-api.js`.

### Connected Preview on the Same Wi-Fi

1. Connect your computer and phone to the same Wi-Fi. On Windows, double-click `START_HANDYHIVE_WEB.cmd`. You can also run `npm run start:phone` or `node scripts/start-web.js --phone` from the project folder. The first setup requires Node.js 24 and `npm --prefix mobile ci`.
2. Wait for **HandyHive connected preview**. Open the printed `http://` address on your phone and keep the server running. You can use your browser’s **Add to Home Screen** option to open HandyHive again from a shortcut.
3. Choose **Try demo location** to browse sample workers. Create a preview account with fictional details to try booking, chat and test checkout. The phone preview saves its own data in `handyhive-phone-web.sqlite`.

If there are multiple network adapters, set `HANDYHIVE_HOST` to the computer’s IPv4 address on the phone’s network and run the launcher again. If the phone can’t load the page, check that the address is current and try a private Wi-Fi network or a hotspot that allows connected devices to reach each other. Use locality search or enter a PIN code for this HTTP preview. A permanent HTTPS setup is described in [SECURITY_AND_LAUNCH.md](SECURITY_AND_LAUNCH.md#permanent-hosting).

---

## 💻 Develop in the Browser

Use Node.js 24. From this project folder:

```powershell
npm --prefix mobile ci
npm run dev
```

Open http://127.0.0.1:4174. The command builds the website, starts its API, and watches the shared source. After saving a change, wait for **Website updated**, then refresh the browser. Stop with Ctrl+C. Stop any other server on port 4174 before starting.

- Edit `mobile/app/` for screens and navigation.
- Edit `mobile/src/` for shared UI, styles, language, and app behavior.
- Edit `mobile/assets/` for images and `mobile/shared/` for shared marketplace rules.
- Edit `server.js` and its supporting modules for API behavior.

The website uses the API on the same origin. Android-specific offline demo and pilot settings do not carry into website builds. The local preview starts with bookable demo workers in all four service categories. Choose **Try demo PIN · 110075**, sign in with a preview account, and book any demo worker using fictional visit details. The booking’s **Demo visit** controls simulate the worker’s steps. Use **Open payment** to try test checkout and unlock **Leave a review**.

Customers enter the six-digit PIN code of the visit address. Workers add their exact service PIN codes in their profile. Coverage, appointments, and new bookings use these codes. Locality labels are optional. Existing profiles need service PIN codes before taking new bookings. Saved addresses from earlier versions can be updated under **Account → Saved places**.

Explore shows matching workers after the PIN is selected. Open a worker profile to see their rating, customer reviews, and work number if they publish one. The booking form carries the selected PIN forward and offers saved places with that PIN. Customers can leave a rating and optional public review after a completed visit is paid in full.

To try the worker workspace separately, sign in as `worker-demo`, `electric-demo`, `cleaning-demo`, or `painting-demo` with `HandyHive-local-demo`. The phone pilot also provides these workers. Set `HANDYHIVE_DEMO_WORKERS=0` before starting a local server when you need a directory with only your own profiles.

---

## 🛠️ Build or Run

```powershell
npm run build:pages  # Export static web demo for GitHub Pages (dist-pages/)
npm run build:web    # Create mobile/dist without starting a server
npm start            # Build the website and run it with the API
npm run typecheck    # Run TypeScript check
```

`node server.js` serves the last website build by default. Docker builds the same shared website. The original HTML/JavaScript prototype is retained for reference; set `HANDYHIVE_APP_PREVIEW=0` only if you need to run it. Opening the old root `index.html` directly does not show the shared app.

See [mobile/README.md](mobile/README.md) for Android builds and app testing. Browser edits to shared files already apply to the app source; an installed APK needs a new build to display them. Check native behavior on a phone before release, especially navigation, permissions, storage, keyboard layout, and accessibility.

Image provenance for the existing photographs is listed in [ASSET_LICENSES.md](ASSET_LICENSES.md). Verify rights before a commercial launch.

Review [LAUNCH_CHECKLIST.md](LAUNCH_CHECKLIST.md) before deployment. The public service pages have descriptive metadata and a sitemap; account, booking, worker, and admin pages are marked out of search indexing.

Operations access and the account deletion request queue are described in [ADMIN_SETUP.md](ADMIN_SETUP.md).

---

## 🔑 Google Sign-In

The connected website supports Google sign-in through an ASAAN-specific Firebase project when its public web config is configured. A server Admin credential enables additional token revocation checks. See [FIREBASE_SETUP.md](FIREBASE_SETUP.md). Phone sign-in remains available; the GitHub Pages build remains an offline demo. Google identity is linked to an existing phone account only through an explicit action while signed in to that account.

---

## 💳 Payments and Provider Safety

- Open a completed booking with an outstanding final bill to try checkout. The local preview simulates the payment and labels the receipt as a test. For Razorpay staging, set `HANDYHIVE_PUBLIC_ORIGIN` to the staging HTTPS URL and configure `RAZORPAY_KEY_ID` (test key), `RAZORPAY_KEY_SECRET`, and `RAZORPAY_WEBHOOK_SECRET` on the API server. Subscribe to `payment_link.paid`, `payment_link.expired`, and `payment_link.cancelled` at `/api/payments/razorpay-webhook`. Live collection requires merchant approval, worker settlements, and refund handling. Direct cash and UPI receipts remain available.
- Customers can open payment from a completed booking and leave a rating once the full bill is confirmed. Provider profiles and bookings offer a Report menu. Account shows private report status and lets customers unblock providers.
- Reports go to the existing private operator queue. See [SECURITY_AND_LAUNCH.md](SECURITY_AND_LAUNCH.md) for verification, report review, and marketplace-wide suspension.
- Customer Support accepts private requests from Home, Account, and the booking Report menu. Operators with access to the server database can see them with `node scripts/trust-admin.js queue` and reply and close a ticket with `node scripts/trust-admin.js support-resolve input.json`. Set `HANDYHIVE_DB` to the server database and include `id`, `owner`, `reviewer`, and `response` in the input file. Customers see the reply on the Customer Support screen.
