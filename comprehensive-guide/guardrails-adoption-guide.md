# Guardrails Adoption Guide

## 1. Introduction

The civic safety guardrails framework helps public-interest projects stay grounded in care, consent, and harm reduction. Every implementation should highlight the four pillars that anchor the framework:

- **Evidence, Not Invention** – publish only what you can point to directly; leave gaps instead of speculating.
- **Privacy & Minimal Data** – collect and display only the minimum information needed to serve your community.
- **Non-Carceral Ethos** – “we clean trash, not people”; avoid surveillance, policing, or stigmatizing language.
- **Safety & Consent First** – center human safety, seek consent before sharing stories or images, and de-escalate whenever possible.

The canonical HTML/CSS snippet in `templates/ui-guardrails-snippet.md` is the shared building block behind live projects like the [park-cleanup-site](https://ai-village-agents.github.io/park-cleanup-site/). The sections below walk through how to re-use, customize, validate, and troubleshoot that snippet in your own projects.

## 2. Technical Implementation Guide

### 2.1 Repository baseline

Before adding UI elements, align your repo with the launch checklist from `docs/repo-setup-guardrails.md`:

1. `LICENSE` – MIT is the default for this ecosystem.
2. `CODE_OF_CONDUCT.md` – include a clear reporting channel.
3. README safety language – start from `templates/readme-safety-snippet.md` and adapt the examples.
4. Decide where sensitive data lives – public repos hold code, guidance, and aggregate stats; PII belongs in private tools.

### 2.2 Static or traditional HTML sites

1. **Copy the snippet**  
   - Paste the HTML block from `templates/ui-guardrails-snippet.md` into your page `<body>`.  
   - Add the CSS block to a `<style>` tag or your primary stylesheet.
2. **Anchor your navigation** (optional)  
   - Use the provided jump link to add `Safety & Guardrails` to your site header.
3. **Confirm accessibility**  
   - The `<section>` already uses `aria-labelledby`. Keep heading levels consistent with your page hierarchy.
4. **Example integration**

```html
<!-- park-cleanup-site style guardrails -->
<section class="guardrails" aria-labelledby="guardrails-title">
  <h2 id="guardrails-title">Safety, Privacy & Guardrails</h2>
  <p>Our cleanup stays grounded in consent, respect, and transparency.</p>
  <div class="guardrails-grid">
    <!-- reuse the four <article> pillars verbatim or customize copy -->
    <!-- ... -->
  </div>
</section>
```

### 2.3 Component frameworks (React, Vue, Svelte)

Wrap the snippet in a component so the guardrails can appear on multiple pages or layouts.

```tsx
// components/Guardrails.tsx
export function Guardrails() {
  return (
    <section className="guardrails" aria-labelledby="guardrails-title">
      <h2 id="guardrails-title">Safety, Privacy & Guardrails</h2>
      <p>
        We follow the Evidence, Privacy, Non-Carceral, and Safety pillars for every deployment.
      </p>
      <div className="guardrails-grid">
        <article className="guardrail-card">
          <h3>Evidence, Not Invention</h3>
          <p>Use source-verified transcripts, logs, and artifacts. Leave gaps when records end.</p>
        </article>
        {/* Repeat the remaining pillars */}
      </div>
    </section>
  );
}
```

Import the CSS into your bundle (e.g., within `App.css` or a module stylesheet). For frameworks with scoped styles, keep the class names intact or alias them via CSS modules.

### 2.4 Content management systems (WordPress, Squarespace, Notion embeds)

1. Create a reusable block or snippet entry for the guardrails HTML.
2. Add the CSS to the theme’s custom CSS panel.
3. Reference the block in CMS templates and ensure default typography resembles your site’s body copy.
4. Store instructions in your team wiki so non-technical editors can drop the block into new pages.

### 2.5 README and docs usage

Use the text-first snippet (`templates/readme-safety-snippet.md`) side-by-side with the visual block:

```markdown
## Safety, Privacy, and Guardrails

We publish code and aggregate insights only. Volunteer PII, consent records, and sensitive photos stay in private systems. We clean trash, not people.
```

Cross-link to the live guardrails component so contributors can see how the norms surface in public artifacts.

### 2.6 Real-world example: park-cleanup-site

- The site embeds the HTML snippet directly in `index.html`, using the default color palette.
- The guardrails grid appears above volunteer call-to-action buttons, reinforcing expectations before sign-ups.
- Photos focus on tools and landscapes; captions echo the four pillars, modeled on `docs/privacy-redaction-checklist.md`.
- The repo references the privacy checklist in its README, mirroring the “Quick version (2-minute check)” guidance.

## 3. Visual Implementation Examples

- ![Guardrails component on a homepage](../assets/placeholder-homepage-guardrails.png)  
  *Placement:* Directly below the hero content, as seen in the park-cleanup-site.  
  *Why it works:* Visitors understand safety norms before clicking “Volunteer”.

- ![Guardrails in a volunteer portal sidebar](../assets/placeholder-portal-sidebar.png)  
  *Placement:* Sticky sidebar on authenticated dashboards.  
  *Notes:* Replace the intro paragraph with portal-specific language (e.g., “These rules apply to dispatch notes.”).

- ![Guardrails as a mobile accordion](../assets/placeholder-mobile-accordion.png)  
  *Placement:* Collapsible accordion on mobile to preserve vertical space.  
  *Implementation hint:* Switch `.guardrails-grid` to `display: block;` under 480 px and use `details/summary`.

Add real screenshots to `../assets/` (or your project’s asset directory) once ready; ensure any people or locations respect the privacy checklist before publishing.

## 4. Customization Reference

### 4.1 Color schemes

Override custom properties to align with your brand while keeping contrast accessible:

```css
:root {
  --green-light: #4caf50;
  --green-mid: #1b5e20;
  --gray-mid: #444;
  --white: #fdfdfd;
}
.guardrail-card {
  border-left-color: var(--green-mid);
  background: color-mix(in srgb, var(--white) 90%, var(--green-light));
}
```

- **Warm palette:** swap greens for amber (`#ffb300`) and rust (`#bf360c`) when working with wildfire relief projects.
- **High-contrast mode:** add `[data-theme="high-contrast"] .guardrails` variations that raise text contrast to WCAG AAA.

### 4.2 Layout options

- **Two-column emphasis:** `grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));` balances readability on tablets.
- **Card icons:** add SVG icons per pillar with `display: flex; gap: 0.75rem; align-items: flex-start;`.
- **Accordion pattern:** use `<details class="guardrail-card">` with summary headings when space is limited.

### 4.3 Responsiveness tweaks

```css
@media (max-width: 600px) {
  .guardrails {
    padding: 1.5rem 1.25rem;
  }
  .guardrails-grid {
    grid-template-columns: 1fr;
  }
  .guardrail-card {
    border-left-width: 3px;
    font-size: 0.98rem;
  }
}
```

- **Dark mode:** pair with a `.guardrails.dark` class that flips background to `rgba(255,255,255,0.08)` while preserving border contrast.
- **Print mode:** add `@media print` rules to remove box shadows and ensure headings remain hierarchical.

## 5. Testing & Validation

Use `docs/privacy-redaction-checklist.md` as your validation backbone.

1. **Content audit**  
   - Run the full checklist for major releases.  
   - For quick updates, follow the “2-minute check” to scan for `@`, phone numbers, faces, and identifying details.
2. **Accessibility**  
   - Verify heading order (`<h2>` followed by `<h3>`).  
   - Test keyboard focus and screen-reader landmarks (`aria-labelledby` points to a visible heading).
3. **Visual regression**  
   - Capture screenshots at 320 px, 768 px, and 1280 px widths.  
   - Confirm cards do not overflow or overlap call-to-action elements.
4. **Repository hygiene**  
   - `rg --files -g '*.png'` to list new images and ensure filenames do not include personal names.  
   - `rg '@' docs/ -g '*.md'` to catch stray email addresses before commit.
5. **Approval workflow**  
   - Require PR reviewers to check a box confirming the privacy checklist ran (mirrors `docs/repo-setup-guardrails.md`, section 4).  
   - If using CI, add placeholder steps to call future scripts in `checks/`.

### 5.6 Pre-flight launches (optional but recommended)

For major public launches (new repos, substantial site updates, or long-form reports), pair this implementation guide with the upstream checklist in `civic-safety-guardrails`:

- **Pre-flight Safety, Privacy & Non-carceral Checklist** — reusable end-to-end launch checklist that consolidates repo basics, PII checks, image/log redaction, non-carceral framing, hazard guidance, and approximate stats/stories into one pre-publish pass. See: [templates/pre-flight-safety-privacy-checklist.md](https://github.com/ai-village-agents/civic-safety-guardrails/blob/main/templates/pre-flight-safety-privacy-checklist.md).

Run the pre-flight checklist when you are about to make something *new* public (or significantly expand its audience); use this adoption guide to handle the *how* of wiring the guardrails snippet into your implementation.

## 6. Common Pitfalls & Solutions

- **PII sneaking into issues or PRs**  
  - *Solution:* Add a “No PII” template checkbox (see `docs/repo-setup-guardrails.md`, section 4). Point contributors to private intake forms instead of GitHub comments.

- **Over-customizing pillar language**  
  - *Solution:* Keep the four pillar headings intact. Tailor body copy, but maintain the core meaning so downstream materials stay consistent.

- **Publishing identifying photos**  
  - *Solution:* Apply the Step 2 rules from `docs/privacy-redaction-checklist.md`. Blur or replace images with tool/landscape shots and document consent in private folders.

- **CSS conflicts with existing design systems**  
  - *Solution:* Namespace classes (e.g., `.civic-guardrails`) while preserving structural roles. Confirm CSS variables do not overwrite global tokens.

- **Missing license or code of conduct in forks**  
  - *Solution:* Re-run the launch checklist when cloning or forking. Fork-specific README updates should restate guardrails expectations to avoid drift.

- **Guardrails buried too deep in navigation**  
  - *Solution:* Follow the park-cleanup-site pattern: surface guardrails on the homepage or key dashboard view, then cross-link from README and volunteer onboarding docs.

## 7. Governance & Cross-Repo Map

The canonical source of truth for what can or cannot change in the UI snippet is `civic-safety-guardrails/docs/ui-guardrails-snippet-governance.md`. This adoption guide covers implementation patterns; the governance doc defines the non-negotiable guardrails, required pillars, and versioning rules.

The canonical HTML/text for the UI snippet lives in `civic-safety-guardrails/templates/ui-guardrails-snippet.md` on the `main` branch. Treat that file—not this guide—as the source of truth for the four pillar headings and core semantics; this guide should track, not fork, those norms.

When you embed or adapt the snippet:
- In cleanup, safety, or policing-adjacent contexts, the non-carceral pillar (including “We clean trash, not people”) is not optional; wording can be localized or clarified, but the non-carceral commitments must not be removed or watered down.
- If local practice does not yet fully match a claim in the snippet (e.g., de-escalation training that is planned but not yet live), that text must be clearly marked as aspirational with a brief note and concrete next steps, or omitted until it becomes true.
- Teams that make improvements (accessibility tweaks, clearer copy, better examples) should upstream those changes back to `civic-safety-guardrails` so the canonical snippet and governance docs can incorporate them.

- `civic-safety-guardrails` – upstream owner of the snippet and governance.
- `park-cleanup-site` – live implementation consuming the snippet.
- `community-cleanup-toolkit` and `community-action-framework` – organizer playbooks that depend on the same four pillars.
- `village-time-capsule` – archive that documents the shared architecture and decisions.

When you discover better patterns or fixes, open a PR to `civic-safety-guardrails` so the governance and adoption guidance stay aligned and everyone benefits from the improvement.

---

By combining the drop-in snippet, the repo setup checklist, and the privacy redaction workflow, teams can make guardrails visible, durable, and easy to maintain. Treat the guardrails component as a living contract with your community—update it alongside new programs, and document any deviations so future collaborators understand the rationale.
