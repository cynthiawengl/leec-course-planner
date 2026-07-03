# LEEC Course Planner

A pure front-end single-page app that helps you pick courses and plan credits across two Técnico Lisboa master's programs — **MEEC** (Master in Electrical and Computer Engineering) and **MEIC-A** (Master in Computer Science and Computer Engineering) — and arrange a weekly class timetable.

Just open [`planner/index.html`](planner/index.html) in a browser — no install, no server required.

## Features

### 1. Credit planner
- Two years, four semesters (Y1S1 / Y1S2 / Y2S1 / Y2S2), each capped at **36 ECTS**
- Year 2 Semester 1 automatically locks in **12 ECTS for PIC** (integrated project); Year 2 Semester 2 locks in **30 ECTS for the thesis** (Dissertação) — both count toward the 36 ECTS cap
- Each semester is split by period: full-semester (Semestral) courses are shown separately, while half-semester courses are placed under P1/P2 or P3/P4
- The course catalog on the right can be filtered by program (MEEC / MEIC-A), semester, and specialization track, with search by name or acronym
- **Save & compare plans**: save the current selection as a named plan, save as many as you like, then check any two plans to open a side-by-side comparison showing per-semester course differences and credit subtotals
- Everything persists in the browser's `localStorage`, so a page refresh won't lose your selections

### 2. Weekly schedule
- Shares the same selected courses as the credit planner, switchable by semester
- A Monday–Friday, 08:00–21:00 grid that works like Apple Calendar:
  - Click and drag on empty space to create a new time block, then pick a course + type (Teórica / Prática / Lab)
  - Click an existing block to edit or delete it
  - Drag a block to move it (including across days); drag its bottom edge to resize (15-minute snapping)
  - Overlapping blocks on the same day are automatically outlined in red
- Removing a course from the credit planner automatically clears any time blocks already scheduled for it

## Data sources

Course data was parsed from two official curriculum documents (both kept at the repo root):

- `Currículo · Mestrado Bolonha em Engenharia Eletrotécnica e de Computadores.pdf` — official MEEC curriculum (86 courses)
- `A3ES MEIC2026 Plano curricular.xlsx` — MEIC-A credit structure sheet (56 courses)

The parsed result is stored in [`planner/courses.json`](planner/courses.json) and embedded directly into `index.html`, so the page needs no extra network requests.

## Project structure

```
.
├── planner/
│   ├── index.html      # single-page app (credit planner + weekly schedule)
│   └── courses.json    # parsed course data
├── A3ES MEIC2026 Plano curricular.xlsx
└── Currículo · Mestrado Bolonha em Engenharia Eletrotécnica e de Computadores.pdf
```

## Running locally

Just double-click `planner/index.html` to open it in your browser (data is embedded, no network calls needed).

To preview with a local server instead:

```bash
cd planner
python3 -m http.server 8743
# then visit http://localhost:8743
```

## Version history

Commits are kept in the order features were added; see `git log --oneline`:

1. Add original curriculum source files
2. Parse and structure course data into JSON
3. v1: initial credit planner page (dark theme)
4. v2: switch to light theme, add plan save/compare
5. v3: split semesters into periods (P1/P2, P3/P4)
6. v4: add a separate drag-to-schedule weekly calendar page
7. v5: merge into a single-page app (credit planner + weekly schedule)
