# Friends Auction — multiplayer foundation

A mobile-first starter for Friends Auction. This version provides email/password authentication, secure room creation, joining by room code, and a live room member list. It is a foundation, not yet the finished auction game: auction item management, bid validation, timers, and team analysis are subsequent modules.

## Setup

1. In Supabase SQL Editor, confirm the four tables from the earlier foundation setup exist.
2. Run `supabase_setup.sql` in Supabase SQL Editor.
3. In Supabase Dashboard → Project Settings → API, copy the Project URL and the **publishable/anon public key**. Never use the `service_role` key.
4. Edit `index.html` and replace `PASTE_YOUR_SUPABASE_PROJECT_URL_HERE` and `PASTE_YOUR_SUPABASE_PUBLISHABLE_OR_ANON_KEY_HERE` with those public values.
5. In Supabase Authentication settings, enable Email signups. For easy testing, either configure email delivery/confirmation properly or disable email confirmation temporarily for this private test project. Do not use a real production app with insecure email settings.
6. Deploy the static site with a host that serves `index.html` (for example, Vercel). Configure the deployed URL in Supabase Authentication URL settings as the Site URL / allowed redirect URL if required.

## Security notes

- The browser only receives the public Supabase key. Database access is governed by Row Level Security and restricted RPC functions.
- Never commit database passwords, service-role keys, or other secrets.
- The SQL uses `ALTER PUBLICATION ... ADD TABLE`; if the tables are already in the publication, Supabase may report a duplicate-table error. If that happens, remove those two `ALTER PUBLICATION` statements and enable Realtime for `auction_rooms` and `auction_members` from the Supabase dashboard instead.
- This starter does not yet implement auction bidding or timer settlement. Do not advertise it as the complete game until those modules are implemented and tested.
