# Handoff: RISE Franchise Portal × Pipedrive (Pipeline 2.0)

Paste the prompt below into a new Claude Code session on the Mac where Pipedrive access is set up (keychain).

---

I'm continuing work on the RISE franchise candidate portal. Catch up first, then start the Pipedrive audit.

**1. Read the architecture doc.** It's `docs/franchise-portal-architecture.md` on branch `claude/franchisee-portal-architecture-k1buiw` of `gahlbergioabea/rise_connecteam_tools`. Clone or fetch it if it isn't local. It holds every decision so far. The short version:

- **Stack:** one Next.js app on Vercel at `franchise.risemodernwellness.com`, in a new repo `rise-franchise-portal`. Pipedrive owns the deal stage; an app database holds the finer detail. Cal.com handles booking. Every page view reads from the app database, which a Pipedrive webhook keeps in sync. The browser never talks to Pipedrive directly.
- **The candidate's link** carries a private sign-in token, never a deal or person ID.
- **Stage vs field rule:** a stage is a place a deal *waits* for the next thing on the calendar. Event outcomes such as showed or no-show go on the meeting's activity. Milestones go in date fields. Checklists and homework are tracked in the portal, with one summary field on the deal.
- **Meetings are discussions.** Before each course meeting the candidate watches a video and submits homework. Garrett reads it ahead of time and gets one prep sheet on the meeting activity about 24h before the call.
- **Proposed Pipeline 2.0 (13 stages):**
  1. Territory Check
  2. Intro Call Booked (no homework)
  3. Meeting 1 Booked · Business Overview
  4. Meeting 2 Booked · Marketing
  5. Meeting 3 Booked · Sales
  6. Meeting 4 Booked · Delivery (FDD delivered here; 14-day clock starts)
  7. Meeting 5 Booked · Leadership
  8. Territory Meeting Booked
  9. Pre-Confirmation Meeting Booked
  10. Confirmation Day Booked
  11. Preparing To Accept Award
  12. Franchise Agreement Signed
  13. Franchise Fee Collected → Won

  Garrett books the next meeting live on each call, and the Cal.com webhook moves the deal.
- **Deal lifecycle:**
  - If the person has an open deal, a re-opt-in adds a note to it. If all earlier deals are won or lost, a new deal opens.
  - Net-worth gate fails → Lost, reason "Below net worth minimum". There's no nurture stage.
  - 14 days in Territory Check with no booking → Lost, reason "No response".
  - Lost reasons come from a fixed list.
  - Value-first emails go out during the 14-day window. Each one links back to the booking section of the portal.
- **Compliance:** neither the agreement nor any fee can happen until 14+ days after the FDD receipt.
- **Open questions:**
  - Is FDD Review its own meeting, or folded into Meeting 5?
  - Is the Territory meeting placed right?
  - Is homework written answers or set forms?
  - Is Confirmation Day booked via Cal.com?
  - How long after a no-show before the deal is marked Lost?
  - What length should each call be?

**2. Verify Pipedrive access.** Tell me which operations you can and can't do. Can you:
- read pipelines, stages, deal fields and lost reasons?
- read and update deals, persons, activities and notes?
- create or rename stages and custom fields, or only read them?

Make **no changes** in this step.

**3. Run a read-only audit of Pipeline 2.0 against the doc:**
- the current stages, with their IDs, in order
- the existing deal custom fields, with their keys and types
- the lost reasons, and whether free-text reasons are allowed
- the rotting settings
- 3–5 recent deals, to see which fields are actually used

Then give me a gap list of what to add, rename or remove to match the doc. Wait for my go-ahead before changing anything in Pipedrive.

**4. As I change stages or fields live,** help me decide the right custom field, the right moment to set it, and what each one should trigger in the portal. Record the decisions in the architecture doc and push to the same branch.
