# FLOW — UTM Builder

## What this is

A single-page tool that turns a destination + campaign details into one clean UTM link.
No login, no backend, no build step. Open `index.html` and use it.

## Screen layout

- **Sidebar (left):** all saved links, each with copy / edit / remove.
- **Main (right):** the builder form on the left and the live link on the right.
- On smaller screens the sidebar moves below the builder.

## The flow

1. **Pick a destination**
   - BimaScore — `bimascore.com`
   - Bima Clarity — `clarity.bimascore.com`
   - Bima Analyze — `analyze.bimascore.com`

2. **Add an optional page path**
   - Example: `blogs/health-insurance-guide`
   - Left empty → the link points to the homepage.
   - If someone pastes a full URL, only the path is kept.

3. **Fill the required campaign details**
   - Source — where the traffic comes from (google, internal, instagram, newsletter…)
   - Medium — the channel type (cpc, via-team, paid-social, email…)
   - Campaign — the specific push or offer (health-checkup-nov…)

4. **Optional advanced fields**
   - Term — paid keyword
   - Content — which creative/CTA the click came from

5. **The link builds itself**
   - Every keystroke rebuilds the URL in the preview box.
   - Values are auto-cleaned on blur: lowercase, spaces/underscores → hyphens, junk removed.
   - Copy and Save stay disabled until source, medium and campaign are all filled.

6. **Copy / test**
   - **Copy link** copies the URL (does not save).
   - **Test link** opens the URL in a new tab.
   - `Ctrl/Cmd + Enter` copies, `Ctrl/Cmd + S` saves.

7. **Save a link**
   - **Save link** adds the current link to the sidebar.
   - Saving the same URL twice updates the existing entry instead of duplicating it.

8. **Update a saved link**
   - Click a saved link in the sidebar (or its pencil icon) → it loads into the form.
   - A bar appears: *Editing a saved link*.
   - Change anything, then press **Update link** → the same entry is replaced.
   - Press **Save as new instead** in that bar to create a separate link instead.

9. **Remove a saved link**
   - Trash icon on a link → removes it.
   - **Clear all links** at the bottom of the sidebar → removes everything (asks for confirmation).

## Rules baked into the tool

- UTM keys are always `utm_source`, `utm_medium`, `utm_campaign`, `utm_term`, `utm_content`.
- All values are lowercase and hyphenated so reports stay grouped.
- Saved links live in the browser only (`localStorage`) — nothing is sent anywhere.

## Files

| File | Purpose |
|---|---|
| `index.html` | The whole tool (HTML + CSS + JS in one file) |
