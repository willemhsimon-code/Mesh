# Mesh — Product Spec

*Version 0.1 · November 1, 2026 · Status: living document*

This spec is the single source of truth for what Mesh is and what to build. Anything marked **TBD** has not been decided yet. Do not guess at TBD items; ask.

---

## 1. Summary

Mesh connects people who are good with tech with people who aren't. Customers get patient, trusted help with phones, Wi-Fi, TVs, smart home devices and more, either over a secure video call or in person at home. Helpers build a public reputation and earn money. When a job is bigger than a quick fix, Mesh hands it to a vetted IT professional.

**Tagline (working):** "Tech help from people you trust."

**One-line thesis:** Mesh is a reputation-driven network of everyday tech helpers, video-first and nationwide, with local in-person help and pro referrals when needed.

## 2. Problem and positioning

- Many people struggle with everyday tech and have no one patient nearby to ask. Retail tech support (e.g. Geek Squad) is priced and scheduled like a business; DIY tutorials assume confidence people don't have.
- Mesh's angle: **people and patience, not a dispatch service.** You pick and rebook *your* person, see their track record, and learn rather than just get fixed.
- Positioning versus competitors (HelloTech, Geek Squad, senior-focused services like Quincy): video-first and cheaper, relationship-based rebooking, transparent reputation, strong anti-scam safety rules, and a built-in hand-off from video to in-person to pro.
- Mesh deliberately avoids handyman/physical-labor work (previous concept) to reduce liability and avoid direct competition with TaskRabbit and Angi.

## 3. Target customer — TBD

Leading candidate (recommended, not final): **seniors and their adult children/families.** Alternatives under consideration: busy households; small businesses (likely a later phase).

Until decided, build for a general consumer audience but keep these accessibility defaults (they help every audience): large readable type, high contrast, simple language, big touch targets.

## 4. Accounts and roles

- **One account, two modes.** Every user has a single account and can act as a **customer** ("Get help") and/or a **helper** ("Give help").
- At signup the user picks a starting point: "I need tech help" or "I'm good with tech." This is only a starting point, not a permanent role.
- A persistent **Get help / Give help** toggle in the top bar switches mode. Each mode has its own home screen.
- Customer → helper: a "Become a helper" path is always available (profile and Give-help home). It runs helper onboarding on the same account.
- Helper → customer: instant; helpers can request help immediately.
- Customer signup collects only: name, phone, ZIP code. Exact address is collected only when an in-person visit is booked and shared with the helper only after both sides confirm.
- Pro companies (IT businesses) do **not** use the consumer signup. They are onboarded through a separate business portal (see §10). **Business portal is out of MVP scope.**

## 5. Helper onboarding and verification

1. Pick skills: Phones & tablets, Wi-Fi & internet, Computers, TV & streaming, Smart home, Printers, Video calls, Scam & security checks.
2. Pick formats: **Video help** (nationwide) and/or **In-person visits** (local).
3. Verification:
   - ID verification — required for all helpers.
   - Background check — required before any in-person visit.
4. Agree to **the Mesh promise** (see §9).

Skills are self-selected; **badges are earned** from completed, reviewed sessions (e.g. "Wi-Fi Pro · 31 sessions"). Users cannot claim badges.

## 6. Help formats

Three formats exist when a customer posts a request:

| Format | Who can take it | Typical price (placeholder) |
|---|---|---|
| **Video call** | Any eligible helper in the country | From $15 |
| **In person** | Background-checked helpers near the customer | From $40 |
| **Let the helper decide** | Helpers respond with their recommended format; customer approves | $15–$45 |

Rules:
- Each request category has a **suggested format** shown to the customer (e.g. new phone → video; smart TV setup → in person; slow Wi-Fi → helper decides). The customer can override it.
- Helpers can accept the request as posted **or propose a different format** (e.g. "I can do this over video in ~20 min for $15"). The customer must approve a format change before booking.
- **Video help is open nationwide.** In-person help is local only.
- All prices in this spec are placeholders. **Pricing model is TBD.**

## 7. Core flows

### 7.1 Request help (customer)
1. Choose a category (see §11 for list), describe the problem, optionally add photos.
2. Choose format (pre-selected to the suggested format).
3. Choose timing: Right now / Later today / This week.
4. If the category is a **pro category**, skip matching and go to the pro hand-off (§7.6).
5. Otherwise show matched helpers.

### 7.2 Matching
- Video requests: show available helpers nationwide who offer video and have the relevant skill.
- In-person requests: show local helpers who offer visits. Also show video helpers who suggest switching to video, clearly labeled as a suggestion.
- "Helper decides": each helper card shows the format and price that helper proposes.
- Each card shows: name, rating, session count, location (city/state for video, distance for local), tagline, proposed format and price.
- Matching algorithm details: **TBD.** MVP can sort by rating and availability.

### 7.3 Booking
- Customer opens a helper profile and books ("Book a video call with Priya" / "Book a home visit with Jules").
- **Payment is held by Mesh** at booking and released when the customer marks the job done. **Payment provider and dispute rules: TBD** (Stripe Connect recommended).

### 7.4 Video session
- Runs entirely **inside Mesh**: built-in video and screen sharing. No third-party remote-access apps, ever.
- A safety banner is shown at session start: "[Helper] will never ask for your passwords. When a password is needed, you type it yourself."
- Sessions are logged (start/end time, participants, any notes). Whether sessions are recorded: **TBD** (consent and privacy implications).
- End of session: "Problem solved" → review, or "Needs in-person help" → transfer (§7.5).

### 7.5 Video → in-person transfer
1. The video helper flags "Needs in-person help" and writes notes (diagnosis, what was tried, screenshots, device list).
2. If the video helper is local and offers visits, they get first right to take the visit.
3. Otherwise the request goes to local helpers **with the notes attached** so the customer never explains twice.
4. Customer picks a local helper and books.
5. Fairness rules:
   - Customer: part or all of the video fee is credited toward the visit (placeholder: $15 credit).
   - Video helper: paid for the session; optional referral bonus when the visit completes (amount **TBD**).
6. Optional **three-way assist**: customer can keep the video helper on a call during the visit to guide the local helper (placeholder: +$10).
7. If the in-person helper finds the job is beyond a helper (e.g. in-wall network cabling), they escalate to a pro (§7.6) with notes attached.

Escalation chain: **video helper → local helper → vetted pro.**

### 7.6 Pro hand-off
- Triggered by pro categories (Network wiring, Security cameras) or escalation from a helper.
- Shows vetted, licensed, insured IT businesses, marked **SPONSORED** where applicable.
- Customer taps "Request a quote"; the request details and notes are sent to the pro.
- Pro billing model (per referral, sponsored placement, or both): **TBD.**

### 7.7 Reviews
- Both sides review each other after every completed job.
- **Double-blind:** neither side sees the other's review until both submit or a deadline passes (deadline **TBD**, e.g. 7 days).
- Only completed, paid, on-platform jobs can be reviewed.
- Customers can add quick tags: Patient, Explained clearly, Accurate diagnosis.
- In a transfer, the customer reviews each helper separately; good hand-offs count toward an "Accurate diagnosis" badge.

## 8. Profiles and reputation

Reputation is the core retention mechanism: a user's track record lives on Mesh, which discourages taking work off-platform.

**Helper profile (public):**
- Name, photo/initials, city (video) or neighborhood (local), helper since, short bio.
- Stats: rating, sessions completed, number of customers who rebooked them.
- Formats offered (Video · nationwide / Home visits · local).
- Earned badges and verification badges (ID verified, Background checked).
- Recent sessions (title, format, rating) — **never** customer names, addresses or device details.
- Reviews from verified sessions.

**Customer profile:**
- Visible to helpers: rating from helpers, reliability (on time, cancellations), tags (Clear descriptions, Pays promptly, Phone verified), reviews from helpers.
- **Private:** request history, devices, address. Helpers see reputation, never history.
- "Your go-to helpers" list for quick rebooking.

Ratings as customer and as helper are kept **separate**.

## 9. Trust and safety (non-negotiable)

**The Mesh promise** (helpers must agree; shown to customers):
- Helpers never ask for passwords, banking details, one-time codes or gift card codes. The customer always types these.
- All remote help runs through Mesh's built-in video/screen share. Never AnyDesk, TeamViewer or any other remote-access tool.
- Helpers never move conversations or payments off-platform.

Product requirements:
- "A Mesh helper will never ask for your passwords, bank details or gift cards" shown on customer home and at the start of every video session.
- One-tap "Report a problem" during and after sessions.
- ID verification for all helpers; background checks for in-person helpers.
- Addresses revealed only after mutual booking confirmation.
- Privacy: helper portfolios never show customer identities or locations beyond city.

Insurance and liability coverage for in-person visits: **TBD.** Legal review of helper classification (independent contractors) and terms of service: **TBD**, required before launch.

## 10. Revenue model

1. **Commission on each job** (rate **TBD**).
2. **Memberships** — e.g. a monthly "tech check-up" plan, possibly paid by family members for a parent. Details **TBD**.
3. **Pro referrals** — referral fees and/or sponsored placement in the pro hand-off. Details **TBD**.
4. **Brand / retail partnerships** — paid setup for smart home brands, internet providers, retailers. Later phase.

## 11. Request categories (MVP)

| Category | Suggested format | Pro? |
|---|---|---|
| New phone or tablet | Video | No |
| Slow or spotty Wi-Fi | Helper decides | No |
| Smart TV & streaming | In person | No |
| Video calling | Video | No |
| Printer won't connect | Helper decides | No |
| Doorbell or thermostat | In person | No |
| Is this a scam? | Video | No |
| Slow computer | Video | No |
| Network wiring | — | **Yes** |
| Security cameras | — | **Yes** |

## 12. Design

- **Brand name:** Mesh (lowercase "mesh" wordmark with a small pink square mark). Trademark/domain check pending.
- **Colors:**
  - Navy `#14213D` (primary, text, dark surfaces); deep navy `#0E1730` (video session background)
  - Pink `#D81B60` (primary actions, accents; passes contrast with white text); bright pink `#FF5C93` (accents on navy only, with navy text)
  - Light pink `#FDE7EF`, dark pink text `#A3124A`
  - White `#FFFFFF`; page background `#F6F7FB`; light navy `#E8ECF5`; borders `#DDE2EE`; secondary text `#55607A`
- **Typography:** Georgia (system font, with 'Times New Roman', serif fallback) for everything. Chosen for readability and familiarity with older users.
- **Accessibility:** WCAG AA contrast minimum, touch targets ≥ 44px, support system text scaling; consider a "larger text" setting. Plain, friendly language; no jargon in customer-facing copy.
- **Reference prototype:** `docs/prototype/Main.dc.html` (design reference only, not runnable code). Live clickable version: https://claude.ai/artifact/2wwnxAdg8KgaVh8LwHnYgd (private to the owner).

## 13. Technology (recommended, not final)

- Mobile app for iOS and Android from one codebase: React Native with Expo, TypeScript.
- Backend: Supabase (Postgres, auth, storage, realtime) or Firebase. **TBD.**
- Payments: Stripe Connect (hold funds, pay out helpers). **TBD.**
- Video + screen share: Daily, Twilio or LiveKit. **TBD.**
- ID verification / background checks: e.g. Persona, Checkr. **TBD.**

### Core data entities (sketch)
User (shared account, mode flags) · CustomerProfile · HelperProfile (skills, formats, verification status) · Request (category, description, photos, format, timing, status) · Offer (helper, proposed format, price) · Booking · Session (video log) · TransferNote · Review (double-blind) · Badge · ProCompany · QuoteRequest · Payment.

## 14. Build phases

**Phase 1 — MVP (build first):**
- Accounts with two modes and the mode toggle; customer signup; helper onboarding (skills, formats, mock verification).
- Request flow with categories, suggested formats, timing.
- Helper "open requests" list with offers, including format proposals.
- Matching list, helper profiles, booking (mock payment).
- Profiles and double-blind reviews.
- Safety banners and the Mesh promise.

**Phase 2:** real payments, real video/screen share, video → in-person transfer with notes and credit, real ID/background checks.

**Phase 3:** pro hand-off and business portal, memberships, family accounts ("book help for Mom"), partnerships.

## 15. Open questions

- Main customer (seniors and families vs. households vs. small business).
- Pricing, commission rate, referral bonus, credits.
- Payment provider and dispute/refund policy.
- Session recording and consent.
- Insurance, legal structure, helper classification, terms of service.
- Matching algorithm.
- Final name clearance (trademark, domain, app stores).
