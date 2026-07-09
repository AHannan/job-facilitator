# Job Faciltator

A tiny, token-frugal system for producing role-tailored CVs. One master CV lives in
`index.html`. For each application, Claude Code writes a tuned copy into `roles/`. The
browser converts HTML → PDF for free — no server, no build step, no binary regeneration.

## Why it's built this way

Regenerating a formatted document (DOCX/PDF) from scratch for every application is
expensive and slow. Here, the only per-role work is **editing text in an HTML file**,
which is cheap. Conversion to PDF is done by the browser's own "Save as PDF," which:

- keeps the text **selectable** (so applicant-tracking systems can parse it), and
- costs nothing and needs no dependencies.

So: tailor the words with AI (rarely, cheaply), press "Download PDF" as often as you like.

## How to use it

### Convert any version to PDF
1. Open `index.html` (or any file in `roles/`) in your browser — double-click, or in
   VS Code use "Live Preview" / "Open with Live Server."
2. Click **Download PDF** (top bar, screen only).
3. In the print dialog, set **Destination → Save as PDF**, then Save.
   - Recommended: A4 paper, default margins, "Background graphics" ON (keeps the accent
     colours and section rules).

### Tailor for a new job (in VS Code, with Claude Code)
Tell Claude Code, for example:

> Tune my CV for this role: `<paste the job description or URL>`

It will read `index.html`, follow `CLAUDE.md`, and create `roles/<company>.html`, then
summarise what it changed and flag any gaps. Open that file → Download PDF.

## Repository layout

```
.
├─ index.html        # MASTER CV — the single source of truth. Edit this to update facts.
├─ assets/
│  └─ headshot.png   # circular photo, referenced by the header (toggled per role)
├─ roles/            # one tailored HTML per application, e.g. roles/fujitsu.html
├─ CLAUDE.md         # operating rules Claude Code reads automatically
└─ README.md         # this file
```

## The tailoring method (what actually gets changed per role)

Kept short here; the enforceable version is in `CLAUDE.md`.

- **Master is truth.** Never add a skill, tool, employer, number, or date that isn't
  already in `index.html`. Missing requirements are reported as "gaps to prep," not faked.
- **Per role, tune six things:** the title, the tagline (surface the JD's top ~3 skills),
  the profile's lead sentence (lead with the strongest match / matching domain), the
  ordering and labels of the skills rows, the ordering/phrasing of experience bullets
  (metrics never change), and the relocation line.
- **Domain match is the biggest lever.** Tax → the Taazaa/Civi Tax work; healthcare or
  pharma → the qordata compliance platforms; banking → STC Bank. Foreground it.
- **Two A4 pages, always.** If it spills over, the 2014–2016 role collapses to one line.

## Photo & anonymisation

Set a class on the `<body>` tag of a role file:

| Situation                                             | `<body>` class        |
|-------------------------------------------------------|-----------------------|
| EU/EEA role that expects a headshot (ES, PL, DE, PT)  | *(none — default)*    |
| US role, or AI-recruiter / ATS-screened role          | `no-photo`            |
| Employer asks to exclude pictures/age (e.g. Doctolib) | `no-photo anon`       |

`no-photo` hides the headshot; `anon` also hides the education years.

## Updating your master facts

Edit `index.html` when something real changes (new role, new metric, new skill). Every
future tailored version inherits it. Don't edit files in `roles/` to fix a fact — fix the
master, then re-tailor.

## Deliberately NOT included

- **No `html2pdf.js` / `html2canvas` one-click export.** It turns your text into an image:
  larger files, and ATS can't read it. Browser print-to-PDF is the intended path.
- **No JSON data layer or build script (yet).** The HTML-first approach is simpler and
  cheaper. If you later want structured data, the natural upgrade is
  `data/master.json` + a small template renderer — but only add it if you feel the pain.

## Notes

- Print "Background graphics" must be ON or the navy/blue/teal accents won't appear in the
  PDF (they're intentionally kept subtle for print).
- The headshot is a circular PNG with transparency; replace `assets/headshot.png` to swap
  it (keep it square, ~400×400, for a clean circle).
