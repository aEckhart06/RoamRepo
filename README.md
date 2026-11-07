# Roam Together

A responsive, dependency-free trip planning webapp. Serve `dist/` with any static HTTP server (for example `python3 -m http.server 4173 --directory dist`).

## Implemented

- Trip creation and editing with inclusive 31-day validation and protection for existing itinerary dates.
- Day-by-day plans, ideas and per-browser vote toggles, checklist, local roster, and per-trip chat.
- USD expenses, current-roster splitting, and exact integer-cent settlement in traveler order.
- Versioned browser persistence (`roam-together-v1`); signing in never migrates, uploads, or shares demo data.
- Supabase email/password sign-in and account creation. Account sessions are intentionally memory-only; demo records are independent of authentication.

## Infrastructure

Supabase project: `qhxtazxaspsxztsirquw` (Roam), Workshops organization, us-east-2. The frontend contains only its public publishable key. No database trip tables or sharing policies are introduced while signed-in ownership and migration rules are undecided.

Sites project: `appgprj_6aef3027dc68819187c93a28e0b1e38d`, private owner access. `.openai/hosting.json` points to the static output.

Configure Supabase Auth Site URL and allowed redirect URL to the eventual deployed origin before end-to-end email confirmation testing. Confirm email before password sign-in. Authentication requests report server errors and never simulate success.

## Validation

Run `npm test`. Integer-cent settlement, date boundaries, fixture data, and serialization tests pass. JavaScript syntax checks pass. Browser acceptance testing and live authentication are NOT verified: the execution environment denied binding a local HTTP server. Sites source synchronization and deployment are blocked by DNS/network restrictions to the Sites Git endpoint. No real traveler data or credentials were used in testing.

## Acceptance checklist (disposable browser data only)

Use a fresh isolated browser context for each scenario, except the explicit modifications in a scenario. Do not clear a real user's storage.

| Requirement | Scenario |
|---|---|
| R1 | Create Porto Weekend, Porto, Portugal, June 11–13 2027, $1,200; reopen from My trips. |
| R2 | Edit Lisbon budget to $5,000; verify $3,380 remaining. |
| R3 | May 1 start: April 30 and June 1 end rejected; May 31 accepted. |
| R4 | Move Lisbon start to May 22; reject because of May 21 plans. |
| R5 | Day 1 has three plans, arrival at 10:30 AM and market lunch at 1 PM. |
| R6 | Add Sunset viewpoint, May 22, 6 PM, Miradouro da Graça, Explore. |
| R7 | Open arrival details and remove; itinerary and overview each lose it. |
| R8 | Add Sunset sailing / Two hours on the water / Experiences. |
| R9 | Filter Stays; only Our home in Alfama appears. |
| R10 | Sintra vote toggles 4 → 5 → 4, including selected state. |
| R11 | Check Find a place to stay; progress changes 3/5 → 4/5. |
| R12 | Add Casey via Invite friends; local-only notice and seven travelers. |
| R13 | Add Snacks, $60, Drew, Food & drink; fourth row says Everyone. |
| R14 | Six travelers: $270 each; seven: $231.43; $1,620 total and $2,880 remaining. |
| R15 | Verify Drew −$90, Maya +$1,050, Alex −$150, others −$270. Add Maya $0.01 expense: Drew −$90.01, Maya +$1,050.01; balances sum to zero. |
| R16 | Send Meet at the market at noon?; appears under Drew in open trip. |
| R17 | Change a plan, vote, checklist; reload and reopen Lisbon; all persist. |
| R18 | Sign-in dialog has email/password, both actions, email confirmation explanation. Test only disposable accounts after redirect configuration. |

## Scope

No bookings, payments, currency conversion, delivered invitations, cross-device saving, or signed-in trip collaboration. Existing local records are never migrated on sign-in. This new origin cannot access device-local data from a different prototype origin; those records remain untouched there.
