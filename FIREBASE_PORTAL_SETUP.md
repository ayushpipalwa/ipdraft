# Reskills learner portal — Firebase setup

The portal in `portal/` is limited to course-only files: assignments, worksheets, projects and permitted learning evidence. Do not upload PAN, Aadhaar, bank information, GST returns, tax filings, invoices or other personal financial documents.

## Enable Firebase services

In project `reskill-5ed6e`:

1. Authentication → Sign-in method → enable Email/Password.
2. Firestore Database → create in Production mode.
3. Storage → create the default bucket.
4. Hosting → Get started.

## Deploy

```bash
npm install -g firebase-tools
firebase login
firebase use reskill-5ed6e
firebase deploy --only hosting,firestore:rules,storage
```

## Custom domain

Firebase Console → Hosting → Add custom domain → `portal.reskills.in`. Add exactly the DNS records Firebase supplies, then add `portal.reskills.in` to Authentication → Settings → Authorized domains.

## First administrator

Create an account through the portal. In Firestore Console, open `users/{UID}` for that account and change `role` from `student` to `admin`. Do not allow users to assign themselves the admin role.

## Checks before launch

Test authentication, password reset, per-student document visibility, file type/size rejection and student inability to alter roles. Keep course-only upload restrictions in place.
