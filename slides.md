---
title: "Reproducible CWL workflows made easy with SciWIn"
theme: default
layout: center
class: "text-center"
fonts:
  sans: 'Fira Sans'
---

<!-- --------------------------------------------------------------
  GLOBAL BRAND STYLES (FAIRagro CD Manual, Dec 2024)
  Primary green   #6abf5c   Lime   #9acb4e   Teal   #0f9884
  Accent coral    #f26e5f   Accent maroon #973442
  Ink   #231f20   Grey  #a7a6a6
-------------------------------------------------------------- -->

<style global>
:root {
  --fa-green:  #6abf5c;
  --fa-lime:   #9acb4e;
  --fa-teal:   #0f9884;
  --fa-coral:  #f26e5f;
  --fa-maroon: #973442;
  --fa-ink:    #231f20;
  --fa-grey:   #a7a6a6;
  --fa-gradient: linear-gradient(90deg, #6abf5c 0%, #9acb4e 45%, #0f9884 100%);
}
h1, h2, h3 { color: var(--fa-ink); }
.slidev-layout { font-family: 'Fira Sans', sans-serif; }
.fa-bar {
  height: 6px;
  width: 100%;
  background: var(--fa-gradient);
  border-radius: 4px;
  margin-bottom: 1.5rem;
}
.fa-nav-list {
  max-width: 640px;
  margin: 0 auto;
  text-align: left;
}
.fa-nav-item {
  display: flex;
  align-items: center;
  gap: 0.9rem;
  padding: 0.7rem 1.1rem;
  margin-bottom: 0.55rem;
  border-radius: 0.65rem;
  border-left: 5px solid var(--accent);
  text-decoration: none;
  transition: transform 0.15s ease, box-shadow 0.15s ease;
}
.fa-nav-item:hover {
  transform: translateX(6px);
  box-shadow: 0 4px 14px rgba(0,0,0,0.10);
}
.fa-nav-num {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background: var(--accent);
  color: #fff;
  font-weight: 700;
  font-size: 0.85rem;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
.fa-nav-label {
  flex: 1;
  color: var(--fa-ink);
  font-weight: 600;
  font-size: 1.05rem;
  text-align: left;
}
.fa-nav-arrow {
  color: var(--accent);
  font-weight: 700;
  font-size: 1.1rem;
}
</style>

<!-- --------------------------------------------------------------
  1️⃣ TITLE
-------------------------------------------------------------- -->

<img src="https://fairagro.net/wp-content/uploads/2025/04/Fairagro_Logo_mittelachsig_Verlauf_w_512.png" class="mx-auto mb-8" style="width:260px" />

# Reproducible CWL workflows made easy with SciWIn
### Boosting Biodata Bootcamp

<div class="fa-bar" style="max-width:320px; margin:2rem auto 0;"></div>

<div class="mt-8 flex flex-col items-center gap-1" style="font-size:0.95rem; color:#385723;">
  <span><b>Xaver Stiensmeier</b> &nbsp;·&nbsp; <b>Antonia Leidel</b>&nbsp;·&nbsp; <b>Jens Krumsieck</b>&nbsp;·&nbsp; <b>Harald von Waldow</b></span>
  <span style="color:#5c6067; font-size:0.85rem;">15.09.2026 &nbsp;·&nbsp; Aachen</span>
</div>

<!--
notes:
- Welcome the room as people settle in: "Welcome to today's Boosting
  Biodata Bootcamp session — Reproducible CWL workflows made easy with
  SciWIn. Thanks for joining us."

- Brief round of introductions from the presenting team, one line each is
  enough — the room wants to get into content, not a long bio.

- Set expectations for the format: "Today is mostly hands-on. We'll cover
  just enough theory to make sense of what we're doing, then spend most of
  the time building a real, working workflow together — from raw scripts
  all the way to a finished, reproducible pipeline."

- Bridge: "Let's start with the agenda, so you know what today looks
  like."

Timing: ~2 min. Keep this brisk — energy should build toward the hands-on
work, not the introductions.
-->

---
layout: fairagro
title: "Agenda"
---

<!-- --------------------------------------------------------------
  2️⃣ MENU / AGENDA
-------------------------------------------------------------- -->

<style>
.fa-menu-header {
  text-align: center;
  margin-top: -20px;
  margin-bottom: 4px;
}

.fa-menu-sub {
  text-align: center;
  color: var(--text-muted, #6b7280);
  font-size: 0.85rem;
  margin-bottom: 16px;
}

.fa-nav-list {
  display: flex;
  flex-direction: column;
  gap: 8px;
  max-width: 640px;
  margin: 0 auto;
}

.fa-nav-item {
  --accent: #6abf5c;
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 8px 16px;
  border-radius: 10px;
  text-decoration: none;
  color: inherit;
  border: 1px solid rgba(0, 0, 0, 0.06);
  transition: all 0.2s ease;
  position: relative;
  overflow: hidden;
}

.fa-nav-item::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  width: 3px;
  background: var(--accent);
}


.fa-nav-num {
  flex-shrink: 0;
  width: 26px;
  height: 26px;
  border-radius: 50%;
  color: white;
  font-weight: 700;
  font-size: 0.85rem;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
}

.fa-nav-label {
  flex-grow: 1;
  font-weight: 600;
  font-size: 0.95rem;
}

.fa-nav-arrow {
  flex-shrink: 0;
  opacity: 0.4;
  font-size: 1rem;
  transition: all 0.2s ease;
}

.fa-nav-item:hover .fa-nav-arrow {
  opacity: 1;
  transform: translateX(2px);
  color: var(--accent);
}
</style>


<div class="fa-bar" style="margin-left:auto; margin-right:auto;"></div>

<div class="fa-nav-list">

<a href="./motivation" class="fa-nav-item" style="--accent:#6abf5c; background:rgba(106,191,92,0.06)">
  <span class="fa-nav-num" style="background:#6abf5c">1</span>
  <span class="fa-nav-label">Motivation</span>
  <span class="fa-nav-arrow">→</span>
</a>

<a href="./workflows" class="fa-nav-item" style="--accent:#9acb4e; background:rgba(154,203,78,0.06)">
  <span class="fa-nav-num" style="background:#9acb4e">2</span>
  <span class="fa-nav-label">Workflows</span>
  <span class="fa-nav-arrow">→</span>
</a>

<a href="./cwl-basics" class="fa-nav-item" style="--accent:#e6b800; background:rgba(230,184,0,0.07)">
  <span class="fa-nav-num" style="background:#e6b800">3</span>
  <span class="fa-nav-label">Common Workflow Language (CWL)</span>
  <span class="fa-nav-arrow">→</span>
</a>

<a href="./sciwin" class="fa-nav-item" style="--accent:#0f9884; background:rgba(15,152,132,0.06)">
  <span class="fa-nav-num" style="background:#0f9884">4</span>
  <span class="fa-nav-label">SciWIn</span>
  <span class="fa-nav-arrow">→</span>
</a>

<a href="./session1" class="fa-nav-item" style="--accent:#f26e5f; background:rgba(242,110,95,0.06)">
  <span class="fa-nav-num" style="background:#f26e5f">5</span>
  <span class="fa-nav-label">Hands‑On 1: The building blocks</span>
  <span class="fa-nav-arrow">→</span>
</a>

<a href="./session2" class="fa-nav-item" style="--accent:#973442; background:rgba(151,52,66,0.05)">
  <span class="fa-nav-num" style="background:#973442">6</span>
  <span class="fa-nav-label">Hands‑On 2: The workflow</span>
  <span class="fa-nav-arrow">→</span>
</a>

<a href="./session3" class="fa-nav-item" style="--accent:#4a90c4; background:rgba(74,144,196,0.06)">
  <span class="fa-nav-num" style="background:#4a90c4">7</span>
  <span class="fa-nav-label">Hands-On 3: Execution</span>
  <span class="fa-nav-arrow">→</span>
</a>

<a href="./wrapup" class="fa-nav-item" style="--accent:#4f4b4c; background:rgba(79,75,76,0.05)">
  <span class="fa-nav-num" style="background:#4f4b4c">8</span>
  <span class="fa-nav-label">Wrap‑Up</span>
  <span class="fa-nav-arrow">→</span>
</a>

</div>

<!--
notes:
- Walk down the list briefly, framing the shape of the day rather than
  reading every label verbatim: "We'll start with some motivation — why
  this matters — then cover Workflows and CWL as the underlying concepts,
  and introduce SciWIn as the tool that makes CWL approachable."

- "From there, it's three hands-on sessions, building up one continuous
  example: Session 1 builds the individual tools, Session 2 wires them into
  a workflow, Session 3 actually runs it."

- "We'll wrap up with best practices and time for questions."

- Bridge: "Let's start with the motivation — why go through all this in the
  first place."

Timing: ~1 min. This is a map, not content — move quickly and let the
hands-on session numbers do the work of building anticipation.
-->

---
src: ./slides/01-intro.md
---
---
src: ./slides/02-workflows.md
---
---
src: ./slides/03-cwl.md
---
---
src: ./slides/04-sciwin.md
---
---
src: ./slides/05-session1.md
---
---
src: ./slides/06-session2.md
---
---
src: ./slides/07-session3.md
---
---
src: ./slides/08-wrapup.md
---