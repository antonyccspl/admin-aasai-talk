# React + TypeScript + Vite

This template provides a minimal setup to get React working in Vite with HMR and some Oxlint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Oxc](https://oxc.rs)
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/)

## React Compiler

The React Compiler is not enabled on this template because of its impact on dev & build performances. To add it, see [this documentation](https://react.dev/learn/react-compiler/installation).

## Expanding the Oxlint configuration

If you are developing a production application, we recommend enabling type-aware lint rules by installing `oxlint-tsgolint` and editing `.oxlintrc.json`:

```json
{
  "$schema": "./node_modules/oxlint/configuration_schema.json",
  "plugins": ["react", "typescript", "oxc"],
  "options": {
    "typeAware": true
  },
  "rules": {
    "react/rules-of-hooks": "error",
    "react/only-export-components": ["warn", { "allowConstantExport": true }]
  }
}
```

See the [Oxlint rules documentation](https://oxc.rs/docs/guide/usage/linter/rules) for the full list of rules and categories.

## Instagram Host enrollment

Super Admins can create a Host record from **Hosts → New Instagram Host** for a
woman who contacts the team directly. The form collects the same profile,
preferences, photo, and private KYC documents as the in-app Host application,
plus payout details and required admin attestations. PAN/Aadhaar numbers are
sent only for verification; the backend stores their final four characters.
The profile is prepared for app use, but the Host must still verify the phone
number with the app's OTP flow before signing in.

Before using this flow in production, apply
`../aasai-talk/supabase/migrations/20261013000100_admin_instagram_host_enrollment.sql`
and deploy the updated `admin-portal` Edge Function from the app repository.
Deploy both `admin-portal` and `content-moderation` so they use the shared
photo-safety scanner. Rejected photos cannot be overridden; photos needing
manual review can be published only after the Super Admin confirms that the
photo meets the Host photo-safety rules.

## Live online members

The Overview page reports Hosts and male members whose app has sent a presence
heartbeat within the last 60 seconds. It refreshes every 30 seconds and shows
member-level details only to administrators with the corresponding Hosts or
Users page access. The Hosts and Users workspaces also show each account's
current online state and last active time, refresh automatically, and support
online/offline filtering. The Users workspace can be filtered to Hosts or male
members.

Before deploying this feature, apply
`../aasai-talk/supabase/migrations/20261019000100_track_male_member_online_presence.sql`,
deploy the updated `host-presence` and `admin-portal` Edge Functions from the
app repository, and deploy this admin portal. Male-member status is refreshed
while the app is active; the migration also updates the in-app Privacy Policy.
