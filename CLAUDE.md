# Operating rules — Job Facilitator

You tailor Abdul Hannan's CV for specific roles. `index.html` is the **master** and the
**single source of truth**. Each application gets one tuned copy in `roles/<company>.html`.

## Never read `DO-NOT-READ/`
**Never open, read, or search the `DO-NOT-READ/` folder.** It holds PDFs that waste tokens.
Do not Read, Grep, Glob into, or otherwise access anything inside it — skip it entirely.

## The one rule that overrides everything
**Master is truth. Never invent.** Do not add a skill, tool, employer, client, metric, date,
title, or claim that is not already present in `index.html`. If the job needs something that
isn't in the master, do **not** fake it — list it under **"Gaps to prep"** in your summary so
Abdul can prepare (talking points, a quick project, a course) or decide to update the master.

Numbers and metrics are frozen: `8M+ users`, `~25%`, `~90%`, `~20 seconds`, `70–80%`,
`100+ rules`, etc. never change. You may reorder or rephrase around them, never rewrite them.

## How to tailor (the workflow)
1. Read the job description (JD). Identify: the domain (tax / banking-fintech / healthcare-
   pharma / consumer-scale / AI), the top ~3–5 must-have skills, seniority, and location/visa.
2. `cp index.html` → `roles/<company>.html` (lowercase, kebab-case company name).
3. Edit **only** the six levers below. Leave structure, metrics, and every fact intact.
4. Set the right `<body>` class for the photo/anonymisation situation (see table).
5. **Register it on the home page.** Add one `<a class="card">` inside the `#roles` grid in
   `home.html` (remove the `.empty` placeholder once the first real card exists). Mirror the
   master card's shape: `.role` = the targeted title, `.file` = `roles/<company>.html`, `.desc`
   = one line (company + domain lever pulled), and `.tags` for the top skills / body-class.
6. Reply with: what you changed (per lever), the domain lever you pulled, and **Gaps to prep**.

## The six levers you may tune per role
1. **Title** (`.title`) — mirror the JD's title when honest (e.g. "Senior Backend Engineer",
   "Java Technical Lead", "Staff Java Engineer"). Stay within what the master supports.
2. **Tagline** (`.tagline`) — surface the JD's top ~3 skills first; keep it to one line.
3. **Profile lead sentence** (`.profile`) — open by leading with the strongest match or the
   matching **domain**. Keep the rest of the paragraph; only re-front the opening.
4. **Skills rows** (`.skill-row`) — reorder rows and reorder items *within* a row so the JD's
   priorities appear first. You may relabel a row header. Do not add tools not in the master.
5. **Experience** — reorder bullets *within* a role and rephrase them toward the JD's language.
   Do not reorder the roles themselves (they are chronological). Metrics stay fixed.
6. **Relocation line** (`.relocation`) — match the role's city/visa reality (e.g. swap "Porto"
   for the actual city; adjust the visa framing for EU Blue Card vs. local work permit vs. US).

## Domain match is the biggest lever
Lead the profile and foreground the matching experience block:
- **Tax / govtech** → Taazaa / **Civi Tax** (rule engine, 50+ localities, LLM+RPA pipeline).
- **Healthcare / pharma / compliance / regulated** → **qordata** (HCP Engagement, EFPIA,
  Aggregate Spend — 1M+ users, Okta, regulated US/EU workflows).
- **Banking / fintech / payments** → **STC Bank** merchant portal (8M+ users, KYC, gRPC, Kafka).
- **AI / LLM / agentic** → Civi Tax LLM+RPA, Sellify AI (GPT-4), HanCraft side projects.
- **High-scale consumer** → STC Bank (8M+ users), qordata HCP (1M+ users).

## Two A4 pages, always
The master fits two pages. If a tuned copy spills onto a third:
- First, add `tight` to the `<body>` class — this collapses the 2014–2016 qordata Associate
  Consultant role to a single header line (pure-CSS, already wired up).
- If still over, trim adjectives from the least-relevant bullets. Never drop a whole role or
  a metric to save space.

## Photo & anonymisation — set on `<body class="...">`
| Situation                                             | class              |
|-------------------------------------------------------|--------------------|
| EU/EEA role that expects a headshot (ES, PL, DE, PT)  | *(none — default)* |
| US role, or AI-recruiter / ATS-screened role          | `no-photo`         |
| Employer asks to exclude pictures/age (e.g. Doctolib) | `no-photo anon`    |
| Tuned copy runs long                                  | add `tight`        |

`no-photo` hides the headshot; `anon` also hides the education years; `tight` collapses the
earliest role. Combine freely, e.g. `<body class="no-photo anon tight">`.

## Output is print-to-PDF
Never add `html2pdf.js` / `html2canvas` or any image-export path — it makes text unselectable
and ATS-unreadable. The only export is the browser's **Download PDF** button → Save as PDF
(A4, background graphics ON). Keep everything as real, selectable HTML text.

## Don't
- Don't edit `roles/*.html` to fix a fact — fix `index.html`, then re-tailor.
- Don't touch the print CSS, the toolbar, or the metrics.
- Don't add a build step, JSON data layer, or dependencies unless explicitly asked.
