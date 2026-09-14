---
layout: fairagro
title: The outcome
routeAlias: wrapup
---

<div class="fa-bar"></div>

<div class="encounter-wrap">
  <div class="researcher-card">
    <div class="mood">😊</div>
    <img src="/researcher1.png" alt="Anna" />
    <span class="name">Anna</span>
    <span class="role">🛰️ Remote Sensing</span>
  </div>

  <div class="encounter-connector">🤝</div>

  <div class="researcher-card">
    <div class="mood">😊</div>
    <img src="/researcher2.png" alt="Ben" />
    <span class="name">Ben</span>
    <span class="role">🌱 Soil Science</span>
  </div>
</div>

<div class="box-wrap">
  <Box
    label="The outcome"
    :start-click="0"
    :items="[
      { strong: 'One workflow:', text: 'a single workflow.cwl file that combines both of their work' },
      { strong: 'Both can execute it locally:', text: 'for each step a runtime environment is specified including package versions' },
      { strong: 'Collaboration:', text: 'They can easily share their workflow on Git and extend it with scripts from colleagues' } 
    ]"
  />
</div>
<div class="image-credit">
  Icons by Amethyst Studio, <a href="https://thenounproject.com/creator/AmethystStudio/" target="_blank">The Noun Project</a> — <a href="https://creativecommons.org/licenses/by/3.0/deed.de" target="_blank">CC BY 3.0</a>
</div>


<style scoped>
.encounter-wrap{
  display:flex;
  align-items:center;
  justify-content:center;
  gap:24px;
  margin: 0 0 0.5rem;
}
.researcher-card{
  position:relative;
  display:flex;
  flex-direction:column;
  align-items:center;
  gap:4px;
}
.researcher-card img{
  height:80px;
  width:80px;
  object-fit:contain;
  padding:6px;
  border-radius:50%;
  border:3px solid #ffffff;
  background:#ffffff;
  box-shadow:0 6px 18px rgba(15,152,132,0.18);
  box-sizing:border-box;
}
.researcher-card .name{
  font-size:0.85rem;
  font-weight:700;
  color:#0b6f60;
  letter-spacing:.02em;
}
.researcher-card .role{
  font-size:0.65rem;
  font-weight:600;
  color:#0f9884;
  background:#e9f7f4;
  border:1px solid #a9ded3;
  padding:1px 8px;
  border-radius:20px;
}
.encounter-connector{
  display:flex;
  align-items:center;
  justify-content:center;
  width:34px;
  height:34px;
  border-radius:50%;
  background:linear-gradient(135deg,#0f9884,#0b6f60);
  color:#ffffff;
  font-size:1rem;
  font-weight:700;
  box-shadow:0 4px 12px rgba(15,152,132,0.3);
  flex-shrink:0;
  margin-bottom: 16px;
}
.box-wrap{
  max-width: 720px;
  margin: 0 auto;
  font-size: 1rem;
}
.researcher-card .mood{
  position:absolute;
  top:-6px;
  right:0;
  font-size:1.2rem;
  background:#ffffff;
  border-radius:50%;
  padding:2px;
  box-shadow:0 2px 6px rgba(15,152,132,0.25);
  z-index:2;
}
.image-credit{
  position:absolute;
  bottom:16px;
  left:0;
  right:0;
  text-align:center;
  font-size:0.5rem;
  line-height:1.3;
  color:#b0b5ba;
  white-space:nowrap;
}
.image-credit a{
  color:#b0b5ba;
  text-decoration:underline;
}
</style>
<!--
notes:
- Bring the story full circle: "Let's close the loop on Anna and Ben —
  remember the 'How It Started' box from this morning? Here's how it's
  going now."

- Walk through the four points, pairing each one back to a specific
  problem from earlier in the day:
  - "No more hand-offs — remember Anna couldn't touch Ben's R code and
    vice versa? Now either of them can update their own step, and the
    workflow just picks up the change — the other person's part doesn't
    even need to be touched."
  - "No more 'USE_THIS_ONE.csv' — that cryptic filename problem from
    Anna's very first script this morning? Every output now has an
    explicit name and a checksum tracing it back to the exact step that
    made it."
  - "No more 'works on my machine' — a new collaborator, or Anna and Ben's
    supervisor, or anyone else, can run this entire pipeline with one
    command, without installing Python, R, or anything else by hand."
  - "And underneath all of it: one single, versioned workflow.cwl file
    that IS the documentation — it doesn't just describe how the map was
    built, running it reproduces the map."

- Land the emotional close: "Two researchers, two languages, one shared
  field — and now, one reproducible pipeline that belongs to both of
  them."

- Bridge to the wrap-up: "That's Anna and Ben's story. Let's zoom out one
  more time and talk about the habits worth taking with you into your own
  work."

Timing: ~1.5 min. This is the emotional payoff of the whole day's running
example — let it land before moving into the more general best-practices
wrap-up.
-->

---
layout: fairagro
title: Best practices
---

<div class="fa-bar"></div>

<div class="bp-grid mt-4">

  <div class="bp-card">
    <div class="bp-icon">🔒</div>
    <h3>Reproducibility</h3>
    <ul>
      <li>Pin container versions — <code>tool:1.2.3</code>, never <code>:latest</code></li>
      <li>Pin package versions inside the container itself</li>
    </ul>
  </div>

  <div class="bp-card">
    <div class="bp-icon">🧩</div>
    <h3>Modularity</h3>
    <ul>
      <li>Keep tools small &amp; single-purpose</li>
      <li>Compose them into workflows instead of one large script</li>
      <li>Reuse existing tool definitions where possible</li>
    </ul>
  </div>

  <div class="bp-card">
    <div class="bp-icon">📂</div>
    <h3>Portability</h3>
    <ul>
       <li>Package the <b>runtime environment</b> (Docker/Singularity), not just the code</li>
      <li>Use <code>File</code>/<code>Directory</code> inputs instead of hardcoded paths</li>
      <li>Use CWL to run unchanged on a laptop, HPC cluster, or the cloud</li>
    </ul>
  </div>

  <div class="bp-card">
    <div class="bp-icon">📦</div>
    <h3>Version Control</h3>
  <ul>
    <li>Commit <code>.cwl</code> files, scripts, and Dockerfiles together in one repo</li>
    <li><b>Collaborate</b> safely merge, branch, and review workflow changes like code</li>
    <li><b>Roll back</b> instantly if a workflow update breaks something</li>
  </ul>
  </div>

  <div class="bp-card">
    <div class="bp-icon">📝</div>
    <h3>Documentation</h3>
    <ul>
      <li>Provide an <code>inputs.yml</code> template for exact reruns</li>
      <li>Describe expected inputs/outputs in a README</li>
    </ul>
  </div>

</div>

<style scoped>
.bp-grid {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 0.7rem;
  max-width: 100%;
}
.bp-grid .bp-card:nth-child(1) { grid-column: span 2; }
.bp-grid .bp-card:nth-child(2) { grid-column: span 2; }
.bp-grid .bp-card:nth-child(3) { grid-column: span 2; }
.bp-grid .bp-card:nth-child(4) { grid-column: 2 / span 2; }
.bp-grid .bp-card:nth-child(5) { grid-column: 4 / span 2; }

.bp-card {
  border: 1.5px solid #0f9884;
  border-radius: 12px;
  padding: 0.7rem 0.9rem;
  background: #0f98840f;
  transition: transform 0.15s ease, box-shadow 0.15s ease;
}
.bp-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(15, 152, 132, 0.18);
}
.bp-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 1.8rem;
  height: 1.8rem;
  font-size: 1rem;
  border-radius: 50%;
  background: #ffffffaa;
  margin-bottom: 0.35rem;
}
.bp-card h3 {
  margin: 0 0 0.4rem 0;
  font-size: 0.88rem;
  font-weight: 700;
  color: #385723;
}
.bp-card ul {
  margin: 0;
  padding-left: 1rem;
}
.bp-card li {
  font-size: 0.7rem;
  line-height: 1.25;
  margin-bottom: 0.22rem;
}
.bp-card code {
  background: #00000012;
  padding: 0.08rem 0.3rem;
  border-radius: 4px;
  font-size: 0.66rem;
}
</style>

<!--
notes:
- Frame this as a "lessons learned" slide, not new material: "We've spent
  the whole day building a hands-on example with Anna and Ben. Before we
  wrap up, let's zoom out and talk about best practices — things you should
  apply when you take this into your own projects, beyond just today's
  demo."

- Reproducibility:
  → "The single most common mistake we see: pinning a container to
  `:latest`. It feels convenient today, but six months from now, `latest`
  might point to a completely different image. Always pin an explicit
  version — tool:1.2.3, not tool:latest. And this applies inside the
  container too — pin your package versions in the Dockerfile itself, not
  just the image tag."

- Modularity:
  → "Notice how we never wrote one giant script that did everything. Anna's
  NDVI step, Ben's fertility step, and the plotting step were all kept
  small and single-purpose. That's intentional — small, focused tools are
  easier to test, debug, reuse, and swap out. And if someone's already
  built a tool for something you need, reuse their CWL definition instead
  of rewriting it."

- Portability:
  → "This is the core CWL value proposition — you're not just packaging
  code, you're packaging the entire runtime environment. Combined with
  using proper File/Directory input types instead of hardcoded paths — like
  the absolute path problem we saw in Anna's very first script this
  morning — this is what lets the exact same workflow run unchanged on your
  laptop, an HPC cluster, or in the cloud."
  → Nice callback opportunity here: "Remember Anna's original script with
  the hardcoded /home/anna/... path? This is the direct fix for that
  problem."

- Version Control:
  → "Treat your .cwl files exactly like code — because they are code. Commit
  them alongside your scripts and Dockerfiles in the same repo. This gets
  you everything Git normally gives you: safe collaboration through
  branches and merges, proper code review on workflow changes, and the
  ability to roll back instantly if an update breaks something."

- Documentation:
  → "Two lightweight things go a long way: an inputs.yml template so anyone
  can rerun your exact workflow with the exact same inputs, and a README
  describing what inputs are expected and what outputs to expect. This
  doesn't need to be extensive — just enough that someone unfamiliar with
  your project can pick it up."

- Wrap up the slide: "None of this is CWL-specific dogma — these are just
  general good engineering practices. CWL just makes it easier to actually
  follow them."

Timing: ~3 min. Move at a steady pace through each card — this slide has a
lot of content packed in, so resist the urge to read every bullet verbatim;
paraphrase and use the Anna/Ben callbacks where natural to keep energy up
before the final wrap-up slide.
-->

---
layout: fairagro
title: Wrap-Up
---

<div class="h-full flex flex-col justify-center items-center text-center px-12">


<div class="fa-bar" style="margin-left:auto; margin-right:auto;"></div>

<div class="wrap-grid mt-8">

  <div class="wrap-item">
    <div class="wrap-icon">🔄</div>
    <p>CWL turns ad‑hoc scripts into <strong>portable, reproducible</strong> workflows</p>
  </div>

  <div class="wrap-item">
    <div class="wrap-icon">🛠️</div>
    <p>You wrote and chained <strong>your first CWL tools into a CWL workflow</strong> today</p>
  </div>

  <div class="wrap-item">
    <div class="wrap-icon">🚀</div>
    <p>Next step: apply this to a <strong>real pipeline</strong> in your own project</p>
  </div>

</div>

<div class="docs-card mt-8">
  <img src="/sciwin_docs.svg" alt="QR code linking to the SciWIn documentation" class="docs-qr" />
  <div class="docs-text">
    <div class="docs-label">SciWIn Docs</div>
    <a href="https://fairagro.github.io/sciwin/" target="_blank" class="docs-link">fairagro.github.io/sciwin</a>
  </div>
</div>

<div class="thank-you mt-10">
  <div class="thank-you-title">Thank you!</div>
  <div class="thank-you-sub">Questions &amp; discussion welcome</div>
</div>



</div>

<style scoped>
.wrap-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.2rem;
  max-width: 900px;
}
.wrap-item {
  border: 1.5px solid #0f9884;
  border-radius: 14px;
  background: #0f98840f;
  padding: 1.2rem 1rem;
  transition: transform 0.15s ease, box-shadow 0.15s ease;
}
.wrap-item:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 16px rgba(15, 152, 132, 0.18);
}
.wrap-icon {
  font-size: 1.8rem;
  margin-bottom: 0.5rem;
}
.wrap-item p {
  font-size: 0.85rem;
  line-height: 1.4;
  margin: 0;
  color: #333;
}
.thank-you-title {
  font-size: 1.8rem;
  font-weight: 800;
  color: #0f9884;
}
.thank-you-sub {
  font-size: 1rem;
  color: #385723;
  margin-top: 0.2rem;
}
.docs-card {
  display: flex;
  align-items: center;
  gap: 0.9rem;
  border: 1.5px solid #0f9884;
  border-radius: 14px;
  background: #0f98840f;
  padding: 0.7rem 1.1rem;
}
.docs-qr {
  width: 84px;
  height: 84px;
  padding: 4px;
  background: #ffffff;
  border-radius: 8px;
  flex-shrink: 0;
}
.docs-text {
  text-align: left;
}
.docs-label {
  font-size: 0.75rem;
  font-weight: 700;
  color: #385723;
  text-transform: uppercase;
  letter-spacing: .03em;
  margin-bottom: 0.15rem;
}
.docs-link {
  font-size: 0.95rem;
  font-weight: 600;
  color: #0f9884;
  text-decoration: underline;
}
</style>

<!--
notes:
- Slow down here — this is the emotional close of the session, so let it
  breathe a bit more than the content-heavy slides.

- Walk through the three wrap-up items, pausing briefly on each:
  1. "The big picture takeaway: CWL turns those ad-hoc, hard-to-rerun
     scripts we saw at the very start of the day — remember Anna's script
     with the hardcoded path and the 'USE_THIS_ONE' file — into portable,
     reproducible workflows."
  2. "And this wasn't just theory — you personally wrote and chained your
     first CWL tools today. Three tools, two languages, one working
     pipeline, built by you."
  3. "The natural next step is to take this same approach back to your own
     projects — even if it's not to switch everything to CWL, but at least
     to have this in your back pocket next time you find yourself emailing
     a script to a colleague who can't run it."

- Full-circle callback: "We started this morning with Anna and Ben stuck —
  two scripts, two languages, no way to combine them. By the end of today,
  that exact problem is solved, and you built the solution yourselves."

- Deliver the thank-you: "Thank you all for the energy and the questions
  today — genuinely made this a lot more fun to run."

- Open the floor: "We have time for questions and discussion now — anything
  from today, anything about applying this to your own work, all fair
  game."

Timing: ~2 min for the wrap-up narration, then open-ended for Q&A afterward.
Don't rush this slide even if running slightly over on time — a strong,
unhurried close leaves a much better impression than a rushed one.
-->