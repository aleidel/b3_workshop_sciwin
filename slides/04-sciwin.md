---
layout: fairagro
title: SciWIn
routeAlias: sciwin
---

<div class="fa-bar"></div>

<style scoped>
.sciwin-steps{
  display:flex;
  flex-direction:column;
  gap:0.35rem;
  margin-bottom:0.7rem;
}
.sciwin-step{
  display:flex;
  align-items:center;
  gap:0.6rem;
  padding:0.35rem 0.75rem;
  border-radius:10px;
  background:linear-gradient(160deg,#ffffff 0%,#f2fbf9 100%);
  border:1.5px solid #cdeee6;
  box-shadow:0 2px 7px rgba(15,152,132,0.08);
}
.sciwin-step .step-num{
  display:inline-flex;
  align-items:center;
  justify-content:center;
  width:1.3rem; height:1.3rem;
  border-radius:50%;
  background:#0f9884;
  color:#ffffff;
  font-weight:700;
  font-size:0.68rem;
  flex-shrink:0;
}
.sciwin-step .step-icon{ font-size:0.95rem; flex-shrink:0; }
.sciwin-step .step-text{
  font-size:0.8rem;
  line-height:1.3;
  color:#333;
  flex:1;
}
.sciwin-step .step-text b{ color:#0b6f60; }
.sciwin-step .pill{
  flex-shrink:0;
  font-size:0.56rem;
  font-weight:700;
  letter-spacing:.02em;
  text-transform:uppercase;
  padding:0.16rem 0.5rem;
  border-radius:20px;
  background:#A8C83C;
  color:#1a1a1a;
  white-space:nowrap;
}

.sciwin-tools{
  display:flex;
  gap:0.9rem;
  justify-content:center;
  width:100%;
  padding:0 0.5rem;
  margin-top:0.2rem;
}
.tool-card{
  flex:1;
  min-width:0;
  border-radius:12px;
  padding:0.5rem 0.65rem 0.6rem;
  background:linear-gradient(160deg,#ffffff 0%,#f2fbf9 100%);
  border:1.5px solid #cdeee6;
  box-shadow:0 3px 10px rgba(15,152,132,0.12);
  text-align:center;
  display:flex;
  flex-direction:column;
}
.tool-card h3{
  margin:0 0 0.35rem 0;
  font-size:0.82rem;
  font-weight:700;
  color:#0b6f60;
}
.tool-card .img-wrap{
  flex:1;
  display:flex;
  align-items:center;
  justify-content:center;
  background:#f7f7f7;
  border-radius:8px;
  overflow:hidden;
  border:1px solid #e2e2e2;
  box-shadow:0 2px 6px rgba(0,0,0,0.10);
}
.tool-card img{
  width:100%;
  height:180px;
  object-fit:contain;
  display:block;
}

.sciwin-punch{
  margin-top:0.6rem;
  display:flex;
  align-items:center;
  justify-content:center;
  gap:6px;
  padding:0.4rem 0.9rem;
  border-radius:10px;
  background:linear-gradient(90deg, rgba(15,152,132,0.10) 0%, rgba(168,200,60,0.10) 100%);
  border:1.5px solid #0f9884;
  box-shadow:0 2px 8px rgba(15,152,132,0.10);
  font-size:0.82rem;
  color:#0b6f60;
  text-align:center;
}
.sciwin-punch b{ color:#0b6f60; }
</style>

<div class="sciwin-steps">

  <div class="sciwin-step" v-click="1">
    <span class="step-num">1</span>
    <span class="step-icon">🛠️</span>
    <span class="step-text">Create CWL CommandLineTools <b>semi-automatically</b> from your scripts or CLI calls</span>
    <span class="pill">Hands-On 1</span>
  </div>

  <div class="sciwin-step" v-click="2">
    <span class="step-num">2</span>
    <span class="step-icon">🔗</span>
    <span class="step-text">Build <b>complex CWL workflows</b> by connecting your tools</span>
    <span class="pill">Hands-On 2</span>
  </div>

  <div class="sciwin-step" v-click="3">
    <span class="step-num">3</span>
    <span class="step-icon">🚀</span>
    <span class="step-text"><b>Execute</b> workflows locally or on HPC, and share them</span>
    <span class="pill">Hands-On 3</span>
  </div>

</div>

<div class="sciwin-tools" v-click="4">
  <div class="tool-card">
    <h3>🖥️ SciWIn-Client (s4n)</h3>
    <div class="img-wrap">
      <img
        src="/client.png"
        alt="SciWIn-Client terminal example"
        loading="lazy"
      />
    </div>
  </div>
  <div class="tool-card">
    <h3>🎨 SciWIn-Studio</h3>
    <div class="img-wrap">
      <img
        src="/studio2.PNG"
        alt="SciWIn-Studio workflow canvas"
        loading="lazy"
      />
    </div>
  </div>
</div>

<div style="display:flex; justify-content:center;" v-click="5">
  <pre style="color:#0f9884;">
<b>You don't need to learn CWL but you still get all its benefits.</b>
  </pre>
</div>


<!--
notes:
- Bridge from the previous slide's ending: "So we just saw CWL solves our
  reproducibility and portability problems — but Anna and Ben don't want to
  learn a new YAML syntax and hand-write all that boilerplate. This is
  exactly the gap SciWIn was built to close."

- Introduce SciWIn briefly before the clicks: "SciWIn is a tool — actually a
  pair of tools — that lets you get all the benefits of CWL without writing
  CWL by hand. Let's walk through how that works in three steps, which also
  map to the three hands-on exercises we'll do today."

- [Click 1] Step 1 appears: "Create CWL CommandLineTools semi-automatically."
  → Say: "Instead of writing that whole CommandLineTool file we saw earlier
  by hand, SciWIn watches you run your script — or you just point it at your
  CLI call — and it generates the CWL wrapper for you automatically. This is
  Hands-On 1 today: we'll take Anna's and Ben's actual scripts and turn them
  into CWL tools this way."

- [Click 2] Step 2 appears: "Build complex CWL workflows by connecting your
  tools."
  → Say: "Once you have your individual tools, SciWIn helps you wire them
  together into a full workflow — like the one we saw with compute_ndvi,
  compute_fertility, and plot_zone_map — without manually writing the steps
  and outputSource syntax. That's Hands-On 2."

- [Click 3] Step 3 appears: "Execute workflows locally or on HPC, and share
  them."
  → Say: "Finally, once the workflow is built, you can actually run it —
  either on your laptop or scaled up on an HPC cluster — and package it up
  to share with collaborators. That's Hands-On 3, and it's where Anna and
  Ben finally get their combined management map."

- [Click 4] The two tool cards appear: SciWIn-Client and SciWIn-Studio.
  → Say: "Concretely, this comes in two flavors: SciWIn-Client, which is a
  command-line tool — 's4n' — for people who like the terminal, and
  SciWIn-Studio, which is a visual GUI for building and viewing workflows
  as diagrams. We'll get hands-on with both today."

- [Click 5] The punchline appears.
  → Deliver this as the key takeaway, slow down and let it land: "You don't
  need to learn CWL — but you still get all its benefits. Reproducibility,
  portability, clear inputs and outputs — all of that, without writing a
  single line of YAML by hand."

- Bridge to next slide: "Let's take a quick look at some of the specific
  features that make this possible before we jump into the hands-on part."

Timing: ~2 min. Keep energy up here — this is the "relief" moment after the
CWL complexity slide, so the tone should shift from "this is a lot of syntax"
to "but don't worry, here's the shortcut."
-->

---
layout: fairagro
title: SciWIn - Key Features
routeAlias: sciwin-features
---

<div class="fa-bar"></div>

<div class="feat-intro">
  SciWIn offers multiple features for <b>FAIR, reproducible, and shareable</b> scientific workflows:
</div>

<div class="feat-grid">

<div class="box" v-click="1">
  <div class="box-header">
    <span class="box-icon">🖇️</span>
    <h3>Build &amp; Visualize</h3>
    <span class="lang lang-r">CORE</span>
  </div>
  <ul>
    <li>GUI for connecting steps into complex CWL workflows</li>
    <li>Generate <b>publication-ready</b> diagrams</li>
  </ul>
</div>

<div class="box" v-click="2">
  <div class="box-header">
    <span class="box-icon">🔄</span>
    <h3>Version &amp; Reuse</h3>
    <span class="lang lang-r">GIT</span>
  </div>
  <ul>
    <li>Automatic versioning via <b>Git</b></li>
    <li>Reuse existing workflows via <b>Git submodules</b></li>
  </ul>
</div>

<div class="box" v-click="3">
  <div class="box-header">
    <span class="box-icon">⚙️</span>
    <h3>Run Anywhere</h3>
    <span class="lang lang-r">EXEC</span>
  </div>
  <ul>
    <li><b>Local</b> execution of CWL workflows</li>
    <li><b>Remote</b> execution via Reana (with de.NBI)</li>
  </ul>
</div>

<div class="box" v-click="4">
  <div class="box-header">
    <span class="box-icon">📦</span>
    <h3>Package &amp; Share</h3>
    <span class="lang lang-r">FAIR</span>
  </div>
  <ul>
    <li>Export as <b>RO-Crates</b></li>
    <li>Compatible with DataPLANT's <b>ARC</b> format</li>
  </ul>
</div>

<div class="box" v-click="5">
  <div class="box-header">
    <span class="box-icon">🐳</span>
    <h3>Containerize</h3>
    <span class="lang lang-r">NEW</span>
  </div>
  <ul>
    <li><b>Semi-automated</b> Dockerfile creation for your tools</li>
  </ul>
</div>

<div class="box" v-click="6">
  <div class="box-header">
    <span class="box-icon">🎯</span>
    <h3>No CWL Required</h3>
    <span class="lang lang-r">KEY</span>
  </div>
  <ul>
    <li>You write your scripts and let <b>SciWIn handle the CWL boilerplate</b></li>
  </ul>
</div>

</div>

<style scoped>
.feat-intro{
  font-size:1rem;
  line-height:1.375;
  color:#333;
  margin-bottom:1rem;
}
.feat-intro b{ color:#0f9884; }

.feat-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
}

.box {
  border-radius: 14px;
  padding: 0.85rem 1rem;
  background: linear-gradient(160deg, #ffffff 0%, #f2fbf9 100%);
  border: 1.5px solid #cdeee6;
  box-shadow: 0 4px 12px rgba(15, 152, 132, 0.10);
}

.box-header {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  margin-bottom: 0.45rem;
  flex-wrap: wrap;
}

.box-icon {
  font-size: 1.25rem;
}

.box h3 {
  margin: 0;
  font-family: "Fira Code", monospace;
  font-size: 0.92rem;
  font-weight: 700;
  color: #0b6f60;
  flex: 1;
  min-width: 0;
}

.box ul {
  margin: 0;
  padding-left: 1.1rem;
}
.box li {
  margin-bottom: 0.3rem;
  font-size: 0.76rem;
  line-height: 1.35;
  color: #333;
}
.box li:last-child{ margin-bottom: 0; }
.box li b { color: #0b6f60; }

.lang {
  display: inline-block;
  font-size: 0.6rem;
  padding: 0.14rem 0.55rem;
  border-radius: 20px;
  font-weight: 700;
  letter-spacing: 0.02em;
  text-transform: uppercase;
  flex-shrink: 0;
}
.lang-r {
  background: #0f9884;
  color: #ffffff;
}
</style>

<!--
notes:
- Quick framing line before diving in: "SciWIn has quite a few features under
  the hood — let's go through the highlights quickly, then we'll get our
  hands dirty."

- [Click 1] "Build & Visualize"
  → Say: "First, the GUI lets you connect steps visually into a workflow,
  and it can generate clean, publication-ready diagrams — handy if you want
  to put your workflow diagram straight into a paper or a poster."

- [Click 2] "Version & Reuse"
  → Say: "SciWIn integrates with Git — every change to your workflow is
  automatically versioned. And if someone else already built a tool or
  workflow you need, you can reuse it via Git submodules instead of
  reinventing it."

- [Click 3] "Run Anywhere"
  → Say: "You can execute locally for quick testing, or send the exact same
  workflow to run remotely via Reana, which we have access to through
  de.NBI. Same workflow file, different scale."

- [Click 4] "Package & Share" (highlighted box)
  → Say: "This one matters a lot for FAIR data — you can export your entire
  workflow, including data and metadata, as an RO-Crate. It's also
  compatible with DataPLANT's ARC format, so it plays nicely with other
  infrastructure in the German research data landscape."

- [Click 5] "Containerize"
  → Say: "Remember the Docker requirement we saw in the CWL tool example?
  SciWIn can semi-automatically generate the Dockerfile for you too — so
  even the containerization step, which is usually a barrier for a lot of
  researchers, is lowered."

- [Click 6] "No CWL Required" (highlighted box, saved for last on purpose)
  → Deliver this as the closing summary/punchline of the slide: "And to
  circle back to the key message — you write your normal scripts, in
  whatever language you're comfortable with, and SciWIn handles all the CWL
  boilerplate behind the scenes."

- Transition to hands-on: "Alright — enough slides. Let's actually try this
  ourselves. Open up your laptops, and let's start with Hands-On 1."

Timing: ~2–2.5 min. Move briskly through clicks 1–3 (these are the "nice to
know" features), then slow down slightly for clicks 4–6 since they reinforce
the core value proposition (FAIR sharing + the "no CWL required" punchline).
-->

---
layout: fairagro
---

<div class="fa-bar"></div>

<style scoped>
.check-wrap{
  flex:1;
  display:flex;
  flex-direction:column;
  align-items:center;
  justify-content:center;
  gap:1.4rem;
  text-align:center;
}
.check-icon{
  font-size:3.2rem;
  line-height:1;
}
.check-title{
  font-size:2rem;
  font-weight:800;
  color:#0b6f60;
  margin:0;
}
</style>

<div class="check-wrap">
  <div class="check-icon">🙋</div>
  <h1 class="check-title">Any questions so far?</h1>
</div>
<!--
notes:
- This is a simple transition/pause slide — no need for lengthy notes.

- Before the click: give a brief verbal wrap-up of the theory portion.
  "So to recap where we've been: Anna and Ben started with two scripts that
  couldn't talk to each other. We looked at workflows as a concept, CWL as a
  concrete standard for describing them, and SciWIn as the tool that lets us
  get those benefits without writing CWL by hand."

- [Click 2] Title "Are there any questions?" appears.
  → Pause here genuinely — make eye contact with the room, don't rush past
  this. This is a natural checkpoint before moving into the hands-on
  exercises, so it's worth waiting a few extra seconds even if no one speaks
  right away.
  → If no questions come up, use a prompt like: "No worries if not — some of
  this will probably click more once we're actually doing it. Let's move to
  Hands-On 1."

- Practical note: this is also a good moment to do a quick logistics check —
  make sure everyone has the repo cloned / environment set up / whatever is
  needed for the hands-on portion, since we're about to switch from
  slides to live coding.

Timing: flexible — 1–3 min depending on how many questions come up. Don't
feel pressured to fill silence; a pause here is natural and expected.
-->