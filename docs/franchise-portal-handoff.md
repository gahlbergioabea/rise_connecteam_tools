# Handoff: RISE Franchise Portal

Paste the prompt below into a new Claude Code session to continue.

---

I'm continuing work on the RISE franchise candidate portal. Catch up first.

**1. Read the architecture doc.** It's `docs/franchise-portal-architecture.md` on branch `claude/franchisee-portal-architecture-k1buiw` of `gahlbergioabea/rise_connecteam_tools`. It holds every decision so far.

**Where things stand (2026-11-06):**

- **Pipedrive is out as the store of record.** One Postgres database (Neon) owns everything; see §2. The old "Franchise Lead Flow" funnel finishes in Pipedrive, then history is imported once and the seat is cancelled (§12).
- **One Next.js app on Vercel, two sides:** the candidate portal (`/`, `/portal`) and Garrett's admin console (`/admin`), in a new repo `rise-franchise-portal` (§13).
- **The 13 stages are decided** (§5.2). They live in code as `stage_key`s.
- **Garrett runs calls from the admin call screen on his phone** (§6): prep, capture, notes, outcome, book the next meeting.
- **Garrett asks Claude instead of using dashboards,** through a read-only role on reporting views (§9).

**2. Next step: Q1 in §17.** Go meeting by meeting, starting with the Intro Call. For each one, work out what Garrett needs on screen, what he records, and whether each input is a fact (a column on `deals`) or what was said (a `meeting_captures` row). Record it in §6.3 as `content/meetings.ts` definitions and push to the same branch.

**3. Still open:** Q2–Q12 in §17.

**Not done yet:** a progress comment on the ClickUp rock "Franchise sales funnel finished (Q4 rock)". Post it only once the design is final and pushed, and only on Garrett's yes.
