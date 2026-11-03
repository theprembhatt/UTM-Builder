# MEMORY — UTM Builder

## 03 November 2026

### Worked on
- Started the UTM Builder project (folder was empty).

### Completed
- Built `index.html` — a single-file UTM builder for BimaScore.
- Destinations: `bimascore.com`, `clarity.bimascore.com`, `analyze.bimascore.com`.
- Required fields: source, medium, campaign. Optional: page path, term, content.
- Live URL preview, copy button, "test link", reset, recent links (last 8, in `localStorage`).
- Auto-format: lowercase, spaces → hyphens, invalid characters removed on blur.
- Copy is disabled until all three required fields are filled.
- Brand styling taken from bimascore.com (`#5A2EBF`, `#7544E4`, `#F0F4FF`), mobile responsive.
- Wrote `FLOW.md` describing how the tool works.

### Decisions
- One HTML file with inline CSS/JS — no build step, no framework, easy to host anywhere.
- Term and content are kept but hidden under "Advanced options" so the normal flow stays 3 fields.
- Recent links stored in the browser only; no backend and no tracking.

### Verified
- Tested in Chrome: URL generation, required-field gating, reset, pasted full-URL path handling, no horizontal overflow at desktop and mobile widths.

### Pending
- Deploy target not decided (can go on Vercel as a static page).
- Possible next steps: per-platform presets, short-link service, shareable saved presets for the team.

## 03 November 2026 — follow-up

### Completed
- Added `internal` and `team` to the source suggestions.
- Added `via-team` to the medium suggestions.
- Generated the first real link for Bima Clarity:
  `https://clarity.bimascore.com?utm_source=internal&utm_medium=via-team&utm_campaign=sanitation-testing`
  (the campaign was typed as `snaitaion_testing`; typo corrected to `sanitation-testing`).

### Notes
- No typo was found in the tool's own UI text.
- Underscores are converted to hyphens, so `sanitation_testing` becomes `sanitation-testing`.

## 03 November 2026 — sidebar

### Completed
- Added a **sidebar** listing all saved links.
- Each saved link has three actions: **copy**, **edit/update**, **remove**.
- Clicking a link (or the pencil) loads it back into the form and switches the button to **Update link**.
- "Save as new instead" detaches editing so a second save creates a separate link.
- "Clear all links" with a confirmation.
- Save is explicit now (copy no longer auto-saves). `Ctrl/Cmd + S` saves.
- Duplicate URLs update the existing entry instead of adding a new one.
- Saved values are stored cleaned (lowercase, hyphens) so the sidebar matches the link.
- Old `bimascore_utm_recent` entries are migrated automatically to the new `bimascore_utm_saved` store.
- Sidebar moves below the builder on screens under 1080px.

### Verified in Chrome
- Save → update → detach → save as new → open/edit → remove, all with correct counts.
- Values persist after reload.
- No console errors, no horizontal overflow at 1000px and 556px widths.


## 03 November 2026 — QA of clarity.bimascore.com (pre-ship)

### Tested
- Link: `https://clarity.bimascore.com?utm_source=internal&utm_medium=via-team&utm_campaign=sanitation-testing`
- 5 fresh browser sessions (cookies + storage cleared each time):
  1. Desktop: full funnel to OTP screen (mobile OTP, test number 9069979941).
  2. iPhone viewport 390x844: full funnel to OTP screen.
  3. Desktop: funnel to login modal + form validation (no OTP sent).
  4. Android viewport 390x844: family flow with 2 members (self + spouse).
  5. Desktop: direct visit (no UTM) + odd-case UTM + browser back test, to OTP screen.

### Verified working
- Landing, goal select, members + age, pincode check, coverage, category, plans, plan details, buy plan, login modal, OTP screen.
- OTP SMS sent 3 times to the QA number (auth API returned success each time).
- Browser back keeps entered data. Reload keeps attribution and page state.
- No horizontal overflow at 360, 390, 414, 768, 1024, 1440.
- Tracking: UTM saved in `sessionStorage.bc_attribution` and attached to every event:
  `LandingViewed`, `GoalSelected`, `MembersConfirmed`, `CoverageConfirmed`,
  `CategorySelected`, `PlansViewed`, `PlanDetailsViewed`, `BuyPlanClicked`.
  All `POST /api/events` returned 200. Meta Pixel (PageView/ViewContent), MS Clarity,
  Mixpanel and Zoho PageSense also load. Journey id `CLR-xxxxxx-xx` is created.

### Issues found
- Deep links to `/plan-details` and `/verify-details` redirect to `/` on a cold session.
- UTM values are stored raw: `QA TEAM`, `Via_Team`, spaces and underscores are not
  normalised, so reports can split the same campaign.
- Login form accepts invalid Indian mobiles (`1234567890`, `0000000000`); button enables.
- Desktop `/categories`: cards are not selectable until the "Your analysis is complete →
  VIEW" toast is clicked.
- OTP input differs by device: desktop 1 box (max 6), mobile 6 single-digit boxes.
- `bima-journey-display-id` is set on desktop but not on mobile.
- Site gate (basic auth) is no longer active; site loads publicly.
- No email/phone login option found in UI — mobile OTP only (confirm requirement).
- Minor console/a11y: form fields without id/name/labels, lazy images without dimensions.

### Pending
- Confirm whether deep links, the open site gate and email login are intended.
- Confirm whether UTM normalisation (lowercase + hyphens) should be handled by this app too.

