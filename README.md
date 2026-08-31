# Internix

Internix is a cross-platform internship requirement tracker built with Expo and React Native. It runs on Android, iOS, and the web from one TypeScript codebase.

This repository is a clean, editable rebuild of the shared preview's product idea and four-tab structure. A preview bundle cannot provide Emergent's private editable source or backend secrets, so this project implements the functionality in a GitHub-ready form.

## What works

- 120-hour goal tracking (or any custom requirement)
- Daily work logs with decimal hours, skills, and notes
- Remaining-hours, percentage, and deadline calculations
- NOC, offer letter, attendance, certificate, evaluation, and other documents
- Final internship report generation and sharing
- Local offline persistence with no account required
- Optional Supabase email accounts, multi-device sync, private file storage, and row-level security
- Responsive Expo web build
- Navy Internix app icon with a white lowercase `i`

## Run it locally

Requirements: Node.js 20+ and npm.

```bash
npm install
npx expo install --fix
npm run start
```

Then press `w` for the browser, scan the QR code with Expo Go, or run `npm run android` / `npm run ios`.

The app works immediately in **offline mode**. Cloud accounts are optional.

## Enable accounts and cloud sync

1. Create a Supabase project.
2. In Supabase, open **SQL Editor**, paste `supabase/schema.sql`, and run it once.
3. Copy `.env.example` to `.env`.
4. Add the project URL and **anonymous/publishable** key:

```env
EXPO_PUBLIC_SUPABASE_URL=https://YOUR_PROJECT.supabase.co
EXPO_PUBLIC_SUPABASE_ANON_KEY=YOUR_SUPABASE_ANON_KEY
```

5. Restart Expo with `npx expo start --clear`.

Never put a Supabase service-role key in this app or in GitHub.

## Publish to GitHub

If starting from the downloaded folder:

```bash
git init
git add .
git commit -m "Build Internix internship tracker"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/internix.git
git push -u origin main
```

## Replace the temporary Emergent link

The `app.emergent.sh/share-preview` URL is only a temporary Expo preview and cannot be renamed. A new permanent link comes from deploying this repository.

### Fastest permanent web link: Vercel

1. Import the GitHub repository into Vercel.
2. Vercel will read `vercel.json` and run `npx expo export --platform web`.
3. Add the two Supabase environment variables in Vercel if cloud sync is enabled.
4. Deploy. Vercel gives a permanent `*.vercel.app` address.
5. In Vercel **Project Settings → Domains**, change the project name or connect a custom domain such as `internix.app` if you own it.

### Expo preview and native app builds

```bash
npm install -g eas-cli
eas login
eas init
eas build --platform android
eas build --platform ios
```

`eas init` replaces the placeholder project ID in `app.json`. Android builds can be distributed as APK/AAB files; iOS App Store builds require an Apple Developer account.

## Quality checks

```bash
npm run typecheck
npm run test:logic
npm run export:web
```

## Project map

```text
app/                     Expo Router screens
  (tabs)/                Home, Logs, Docs, Report
src/components/          Shared UI and access gate
src/context/             Authentication and internship data
src/lib/                 Optional Supabase client
src/utils/               Hour, progress, deadline calculations
supabase/schema.sql      Tables, private storage, and security policies
assets/                  Internix icon and splash artwork
```

No license has been selected. Add one before accepting outside contributions or distributing the source under specific terms.
