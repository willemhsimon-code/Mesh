# CLAUDE.md — Mesh

Mesh is a mobile app connecting people who are good with tech with people who need tech help, over secure video or in person. The full product spec is in `docs/spec.md`. Read it before starting any task.

## Ground rules

- **Build only what the spec describes.** If a task needs something the spec doesn't cover, or touches an item marked **TBD**, stop and ask instead of guessing.
- Follow the build phases in `docs/spec.md` §14. Do not start Phase 2 or 3 work unless asked.
- The spec owner makes product decisions in a separate planning conversation. If you find a gap or contradiction in the spec, list it in your summary so it can be resolved there.
- Keep changes small and focused, one feature at a time. Explain what you built in plain language; the owner is not necessarily a developer.

## Non-negotiables (from spec §9)

- Never build any flow where a helper can request or see a customer's passwords, one-time codes, banking details or gift card codes.
- Remote help happens only through Mesh's built-in video/screen share. No integrations with third-party remote-access tools.
- Never expose a customer's address before a booking is confirmed by both sides, and never show customer identities, addresses or devices on helper profiles.
- Reviews are double-blind and only for completed on-platform jobs.

## Design

- Colors and type are defined in `docs/spec.md` §12. Use them as design tokens in one place (e.g. a theme file), not hard-coded throughout.
- Font: Georgia (fallback 'Times New Roman', serif) everywhere.
- Accessibility: WCAG AA contrast, touch targets ≥ 44px, respect system text size.
- `docs/prototype/Main.dc.html` is a visual and flow reference only. Do not copy its code; rebuild screens properly in the app's framework.

## Tech

- Recommended stack: React Native + Expo + TypeScript. Backend, payments and video providers are TBD; use mocks/interfaces for them in Phase 1 so real providers can be swapped in later.
- Never commit secrets or API keys. Use environment variables and keep `.env` files out of git.
