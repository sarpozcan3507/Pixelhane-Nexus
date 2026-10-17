# PIXELHANE NEXUS V5

A single-file Turkish-first neon gaming frontend. `index.html` can be uploaded directly to a static HTML host. The site has a local/offline mode and optional Supabase-based cross-device realtime features.

## What works without a backend
- Neon responsive game library with dozens of cards across categories
- Profile/colour customization saved in this browser
- Several local game engines and pass-the-device party mode
- XP and local profile data

## What needs your own Supabase project
- Persistent accounts usable on more than one device
- Cross-device friend requests, follows, private DMs and club chat
- Presence/online status across browsers
- Room chat and multiplayer room broadcasts over Realtime WebSockets

No cloud project is secretly preconfigured. To enable it:

1. Create a Supabase project.
2. In **SQL Editor**, run `pixelhane-v5-backend.sql` once.
3. In **Authentication → Providers / Sign In**, enable Anonymous Sign-Ins if you want guest mode. For cross-device identity, create an email/password account instead.
4. In the HTML app, click **Bağlan**, enter the Project URL and the **publishable key** (`sb_publishable_…`) or legacy `anon` key, then create/sign into an account.
5. Open the same hosted HTML from a second browser/device, sign into the same project with another account, add handles as friends, then create/join a room by code.

**Never put a `service_role` / `sb_secret_…` key in this HTML.** The browser key is public by design; security depends on RLS and the policies in the SQL file. Test RLS and Realtime in your own project before sharing publicly.

## Realtime architecture and limits
- Presence and room/game messages use Supabase Realtime WebSocket channels.
- DMs and club chat are persistent rows protected by row-level security (RLS).
- Casual room topics are not end-to-end encrypted. Room codes are a join secret; share them only with invited players. The sample game's host processes moves in the browser, so it is not cheat-proof or suitable for ranked/real-money play.
- The listed game catalogue includes variations that reuse a smaller set of playable engines; it does not mean every listed card has a unique production-grade game implementation. Start with the supported engine types and expand them independently.
- Anonymous users can be lost when browser data is cleared and won't automatically have the same identity on another device. Use an email/password account for cross-device sign-in. Supabase may require email verification based on project auth settings.
- This is a project package, not yet deployed to a public URL. Static hosting publishes the frontend; Supabase supplies backend services.
