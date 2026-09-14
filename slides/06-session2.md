---
layout: fairagro
title: "Session 2: Building the CWL worflow"
routeAlias: session2
---

<div class="mermaid-wrap">

```mermaid
---
config:
  theme: base
  look: neo
  themeVariables:
    primaryColor: '#C5E0B4'
    primaryTextColor: '#231f20'
    secondaryColor: '#EEEEEE'
    lineColor: '#385723'
    fontSize: 18px
    tertiaryTextColor: '#231f20'
    fontFamily: 'Fira Sans, trebuchet ms, verdana, arial'
  flowchart:
    nodeSpacing: 45
    rankSpacing: 90
    curve: basis
---
flowchart LR
  linkStyle default stroke:#7b5fd1,stroke-width:3px,stroke-dasharray:5 5;
  subgraph inputs[Workflow Inputs]
    direction TB
    reflectance(reflectance)
    soil(soil)
  end
  subgraph outputs[Workflow Outputs]
    direction TB
    zone_map_png(zone_map_png)
  end
    compute_fertility["compute_fertility.cwl"]
  soil --> |soil|compute_fertility

    compute_ndvi["compute_ndvi.cwl"]
  reflectance --> |reflectance|compute_ndvi
    
    plot_zone_map["plot_zone_map.cwl"]
  compute_fertility --> |fertility|plot_zone_map
  compute_ndvi --> |ndvi|plot_zone_map
  plot_zone_map --> |zone_map_png|zone_map_png
  style inputs fill:#EEEEEE,stroke-width:2px;
  style reflectance stroke:#0f9884,fill:#6FC1B5,stroke-width:2px;
  style soil stroke:#0f9884,fill:#6FC1B5,stroke-width:2px;
  style outputs fill:#EEEEEE,stroke-width:2px;
  style zone_map_png stroke:#823909,fill:#F8CBAD,stroke-width:2px;
  style compute_fertility stroke:#385723,fill:#C5E0B4,stroke-width:2px;

  style compute_ndvi stroke:#385723,fill:#C5E0B4,stroke-width:2px;
  style plot_zone_map stroke:#385723,fill:#C5E0B4,stroke-width:2px;
```
</div> <div class="wf-legend"> <span class="legend-chip studio">🎨 You'll connect all of these in SciWIn-Studio</span> </div> <div class="session mt-4"> <div class="session-title">🙌 Hands-On Session 2 — Create a CWL Workflow with SciWIn-Studio</div> <div class="session-steps"> <div class="step"><span class="step-num step-num-highlight">1</span> Create a new workflow with the three steps in <code>SciWIn-Studio</code></div> <div class="step"><span class="step-num step-num-highlight">2</span> Connect the steps visually</div> </div> </div> <style scoped> .wf-legend{ display:flex; gap:14px; justify-content:center; margin-top:0.5rem; font-family:'Fira Sans',sans-serif; font-size:0.78rem; } .legend-chip{ display:inline-flex; align-items:center; gap:6px; padding:4px 10px; border-radius:20px; font-weight:600; } .legend-chip.studio{ background:#f2eefb; color:#5c3fc7; border:1px solid #d9ccfb; } .session { border-radius: 14px; border: 1.5px solid #0f9884; padding: 1rem 1.5rem; background: linear-gradient(90deg, rgba(15,152,132,0.07) 0%, rgba(168,200,60,0.07) 100%); box-shadow: 0 4px 12px rgba(15, 152, 132, 0.08); } .session-title { font-weight: 700; font-size: 1.05rem; color: #0b6f60; margin-bottom: 0.65rem; } .session-steps { display: flex; flex-direction: column; gap: 0.45rem; } .step { font-size: 0.92rem; display: flex; align-items: baseline; gap: 0.6rem; color: #333; } .step-num { display: inline-flex; align-items: center; justify-content: center; width: 1.5rem; height: 1.5rem; border-radius: 50%; background: #0f9884; color: #ffffff; font-weight: 700; font-size: 0.78rem; flex-shrink: 0; } .step-num-highlight { background: #A8C83C; color: #1a1a1a; } .step code { background: #0f988415; padding: 0.15rem 0.4rem; border-radius: 5px; color: #0b6f60; font-weight: 600; } </style>

<!--
notes:
- Bridge from Session 1: "Welcome back. Last session, you built three
  independent CWL tools: compute_ndvi, compute_fertility, and
  plot_zone_map. Each one works on its own, but right now they don't know
  about each other. This session is about wiring them together into one
  actual Workflow."

- Point at the diagram: "Here's the full picture again — three tool boxes,
  green, connected by dashed purple arrows showing data flow. Two inputs
  coming in on the left, one output going out on the right — and every
  single one of these five connections is something you'll draw yourself."

- Point at the legend chip below: "All five arrows — the two inputs, the
  two step-to-step connections, and the final output — get wired up the
  same way: by dragging between ports in SciWIn-Studio's GUI."

- Walk through the "Hands-On Session 2" box: "One task this session —
  open SciWIn-Studio and visually connect all five edges of this workflow:
  reflectance and soil into their steps, the two step outputs into
  plot_zone_map, and plot_zone_map's result out to the final output."

- Bridge: "Let's open SciWIn-Studio and get started."

Timing: ~1-1.5 min. This is an orientation slide — make sure it's clear
that every connection in this session happens visually in Studio, since
that's the structure for the rest of the session.
-->

---
layout: fairagro 
title: "Understanding s4n connect workflow"
disabled: true
---

<div class="fa-bar"></div> <div class="concept-intro"> Every connection follows the same pattern: <code>s4n connect workflow --from &lt;source&gt; --to &lt;target&gt;</code>. There are three types: </div> <div class="concept-grid"> <div class="concept-card"> <div class="concept-label">📥 Workflow Input → Step Input</div> <div class="map-command-code"> <span class="tok s4n">s4n connect workflow </span> <span class="tok active-input">--from reflectance</span> <span class="tok active-command">--to compute_ndvi/reflectance</span> </div> <div class="concept-note">Wires a top-level workflow input into a step's input port.</div> </div> <div class="concept-card highlight"> <div class="concept-label">🔗 Step Output → Step Input</div> <div class="map-command-code"> <span class="tok s4n">s4n connect workflow </span> <span class="tok active-command">--from compute_ndvi/ndvi_csv</span> <span class="tok active-command">--to plot_zone_map/ndvi</span> </div> <div class="concept-note">Passes one step's output into another step's input — <b>this is what you'll do in SciWIn-Studio</b>.</div> </div> <div class="concept-card"> <div class="concept-label">📤 Step Output → Workflow Output</div> <div class="map-command-code"> <span class="tok s4n">s4n connect workflow </span> <span class="tok active-command">--from plot_zone_map/zone_map_png</span> <span class="tok active-output">--to zone_map_png</span> </div> <div class="concept-note">Exposes a step's output as a final workflow output.</div> </div> </div> <style scoped> .concept-intro{ font-family:'Fira Sans',sans-serif; font-size:1rem; line-height:1.45; color:#333; margin-bottom:1rem; } .concept-intro code{ background:#f0f0f0; padding:0.02rem 0.35rem; border-radius:4px; font-size:0.85em; } .concept-grid{ display:grid; grid-template-columns:repeat(3, 1fr); gap:14px; } .concept-card{ border-radius:14px; padding:14px 14px 12px; background:linear-gradient(160deg, #ffffff 0%, #f2fbf9 100%); border:1.5px solid #cdeee6; box-shadow:0 4px 12px rgba(15, 152, 132, 0.10); font-family:'Fira Sans',sans-serif; } .concept-card.highlight{ background:linear-gradient(160deg, #ffffff 0%, #f6f2fd 100%); border-color:#d9ccfb; box-shadow:0 4px 12px rgba(123, 95, 209, 0.18); } .concept-label{ font-size:0.82rem; font-weight:700; color:#0b6f60; margin-bottom:8px; } .concept-card.highlight .concept-label{ color:#5c3fc7; } .map-command-code{ font-family:'Fira Code','Courier New',monospace; font-size:0.62rem; line-height:1.6; margin-bottom:8px; display:flex; flex-wrap:wrap; align-items:center; gap:3px 5px; } .tok{ padding:2px 5px; border-radius:4px; color:#4b4f5e; white-space:nowrap; } .tok.s4n{ color:#a4a7b8; } .tok.active-input{ background:#e7f0ff; color:#2f6fed; font-weight:700; } .tok.active-command{ background:#f2eefb; color:#5c3fc7; font-weight:700; } .tok.active-output{ background:#fde7e6; color:#c0392b; font-weight:700; } .concept-note{ font-size:0.76rem; line-height:1.4; color:#374151; } .concept-note b{ color:#5c3fc7; } </style>
<!--
notes:
- Introduce the general pattern first: "Every single connection in a CWL
  workflow — no matter what kind — follows the exact same command pattern:
  s4n connect workflow, --from something, --to something. The only thing
  that changes is what's on each side of that arrow."
- Walk through the three card types left to right:
  Card 1 — Workflow Input → Step Input:
  → Say: "This is the simplest case — taking something declared as a
  top-level workflow input, like 'reflectance', and wiring it directly into
  a step's input port. Notice the --to side uses a slash: compute_ndvi
  slash reflectance — that's how you address a specific step's specific
  input."
  Card 2 (highlighted) — Step Output → Step Input:
  → Say: "This is the important one — this is exactly what you'll be doing
  yourselves in Studio in a few minutes. Both sides now have that slash
  notation, because we're connecting one step's output port directly to
  another step's input port. Here, compute_ndvi's ndvi_csv output feeds
  into plot_zone_map's ndvi input."
  → Pause and emphasize: "Even though you'll be doing this by dragging in a
  GUI rather than typing this command, this is precisely what's happening
  behind the scenes."
  Card 3 — Step Output → Workflow Output:
  → Say: "And the mirror image of the first case — taking a step's output
  and exposing it as the final workflow-level output. This is how the
  outside world — or the next person running this workflow — knows where
  to find the final result."
- Wrap-up: "So really, there's only one command and one pattern — --from
  and --to — and it's flexible enough to describe every type of connection
  in the whole workflow."
- Bridge: "Let's see this in action — starting with wiring in Anna's
  reflectance input."
Timing: ~2 min. This is a conceptual anchor slide — take your time here
since understanding this pattern makes the upcoming live demos and the
Studio exercise much easier to follow.
-->

---
layout: fairagro 
title: "SciWIn-Client: connect reflectance"
disabled: true
---
<script setup>
const lines3 = [
  {
    type: 'cmd',
    text: 's4n connect workflow --from reflectance --to compute_ndvi/reflectance'
  },
  {
    type: 'info',
    icon: '📄',
    segments: [
      { text: 'Created new Workflow file: ' },
      { text: 'workflows/workflow/workflow.cwl', class: 'text-green-400 font-semibold' },
    ]
  },
  {
    type: 'diff',
    lines: [
      ' 1 | + #!/usr/bin/env cwl-runner',
      ' 2 | + ',
      ' 3 3 | cwlVersion: v1.2',
      ' 4 4 | class: Workflow',
      ' 5 5 | ',
      ' 6 | - inputs: []',
      ' 6 | + inputs:',
      ' 7 | + - id: reflectance',
      ' 8 | + type: File',
      ' 9 | + default:',
      ' 10 | + class: File',
      ' 11 | + location: ../../data/reflectance.csv',
      ' 12 | + ',
      ' 7 13 | outputs: []',
      ' 8 | - steps: []',
      ' 14 | + steps:',
      ' 15 | + - id: compute_ndvi',
      ' 16 | + in:',
      ' 17 | + - id: reflectance',
      ' 18 | + source: reflectance',
      ' 19 | + run: ../compute_ndvi/compute_ndvi.cwl',
      ' 20 | + out:',
      ' 21 | + - ndvi_csv',
    ]
  },
  {
    type: 'info',
    icon: '➕',
    text: 'Added or updated connection from inputs.reflectance to compute_ndvi/reflectance in workflow'
  },
  {
    type: 'success',
    text: '✔️ Updated Workflow workflows/workflow/workflow.cwl!'
  },
]
</script>

<div class="h-100">

<TerminalDemo :lines="lines3" />

</div>

<style scoped>
:deep(.line-cmd) {
  font-size: 1.15rem;
  line-height: 1.6;
  margin-bottom: 0.5rem;
}

:deep(.line-output) {
  font-size: 0.55rem;
  line-height: 1.25;
}
</style>

<!--
notes:
- Narrate live as the terminal demo plays (or as you type/run it yourself).

- Before running: "Let's connect our first input — reflectance — into
  compute_ndvi. Following the pattern we just saw: --from reflectance,
  --to compute_ndvi/reflectance."

- As the output appears: "First thing to notice — since this is our first
  connection, s4n actually created a brand new file for us:
  workflows/workflow/workflow.cwl. This is the Workflow file that will tie
  everything together."

- Walk through the diff highlights:
  - "The inputs section, which started empty, now has a proper entry for
    reflectance — File type, with a default location pointing at our data."
  - "The steps section also went from empty to having its first entry:
    compute_ndvi, which takes reflectance as input, points at the
    compute_ndvi.cwl file we built last session, and declares that it
    produces ndvi_csv as output."

- Point out the confirmation line: "And at the bottom, a plain-language
  confirmation: connection added from inputs.reflectance to
  compute_ndvi/reflectance. That's s4n telling us exactly what it just
  did."

- Bridge: "One input down, one to go — let's connect Ben's soil data next."

Timing: ~1.5-2 min. If this is a pre-recorded/scripted terminal demo rather
than something you type live, slow down your narration to match the pace
of the animation rather than rushing ahead of it.
-->

---
layout: fairagro 
title: "SciWIn-Client: connect soil"
disabled: true
---
<script setup>
const lines4 = [
  {
    type: 'cmd',
    text: 's4n connect workflow --from soil --to compute_fertility/soil'
  },
  {
    type: 'diff',
    lines: [
      ' 9 9 | default:',
      ' 10 10 | class: File',
      ' 11 11 | location: ../../data/reflectance.csv',
      ' 12 | + - id: soil',
      ' 13 | + type: File',
      ' 14 | + default:',
      ' 15 | + class: File',
      ' 16 | + location: ../../data/soil.csv',
      ' 12 17 | ',
      ' 13 18 | outputs: []',
      ' 14 19 | steps:',
      '--------------------------------------------------------------------------------',
      ' 19 24 | run: ../compute_ndvi/compute_ndvi.cwl',
      ' 20 25 | out:',
      ' 21 26 | - ndvi_csv',
      ' 27 | + - id: compute_fertility',
      ' 28 | + in:',
      ' 29 | + - id: soil',
      ' 30 | + source: soil',
      ' 31 | + run: ../compute_fertility/compute_fertility.cwl',
      ' 32 | + out:',
      ' 33 | + - fertility_csv',
    ]
  },
  {
    type: 'info',
    icon: '➕',
    text: 'Added or updated connection from inputs.soil to compute_fertility/soil in workflow'
  },
  {
    type: 'success',
    text: '✔️ Updated Workflow workflows/workflow/workflow.cwl!'
  },
]
</script>

<div class="h-100">

<TerminalDemo :lines="lines4" />

</div>

<style scoped>
:deep(.line-cmd) {
  font-size: 1.15rem;
  line-height: 1.6;
  margin-bottom: 0.5rem;
}

:deep(.line-output) {
  font-size: 0.55rem;
  line-height: 1.25;
}
</style>

<!--
notes:
- Same pattern as the previous slide, so you can move a bit faster here.

- Before running: "Same idea, different input — this time we're wiring
  soil into compute_fertility."

- As the diff appears: "Notice the diff view now shows context lines around
  the change — you can see our new soil input slotting in right after the
  reflectance input we just added. And down in steps, a whole new
  compute_fertility entry appears, mirroring the structure of compute_ndvi
  but pointing at soil and the compute_fertility.cwl file."

- Point out the growing structure: "You can literally watch this workflow
  file grow, one connection at a time — that's the point of doing this
  incrementally rather than hand-writing the whole thing at once."

- Bridge: "Two inputs connected. Last CLI step — let's expose the final
  output."

Timing: ~1-1.5 min. This should feel noticeably quicker than the previous
slide since the audience already understands the pattern — lean into the
"see, same thing again" pacing.
-->
---
layout: fairagro 
title: "SciWIn-Client: connect zone_map_png"
disabled: true
---
<script setup>
const lines5 = [
  {
    type: 'cmd',
    text: 's4n connect workflow --from plot_zone_map/zone_map_png --to zone_map_png'
  },
  {
    type: 'diff',
    lines: [
      ' 15 15 | class: File',
      ' 16 16 | location: ../../data/soil.csv',
      ' 17 17 | ',
      ' 18 | - outputs: []',
      ' 18 | + outputs:',
      ' 19 | + - id: zone_map_png',
      ' 20 | + type: File',
      ' 21 | + outputSource: plot_zone_map/zone_map_png',
      ' 22 | + ',
      ' 19 23 | steps:',
      ' 20 24 | - id: compute_ndvi',
      ' 21 25 | in:',
      '--------------------------------------------------------------------------------',
      ' 31 35 | run: ../compute_fertility/compute_fertility.cwl',
      ' 32 36 | out:',
      ' 33 37 | - fertility_csv',
      ' 38 | + - id: plot_zone_map',
      ' 39 | + in: []',
      ' 40 | + run: ../plot_zone_map/plot_zone_map.cwl',
      ' 41 | + out:',
      ' 42 | + - zone_map_png',
    ]
  },
  {
    type: 'info',
    icon: '➕',
    text: 'Added or updated connection from plot_zone_map/zone_map_png to outputs.zone_map_png in workflow!'
  },
  {
    type: 'success',
    text: '✔️ Updated Workflow workflows/workflow/workflow.cwl!'
  },
]
</script>

<div class="h-100">

<TerminalDemo :lines="lines5" />

</div>

<style scoped>
:deep(.line-cmd) {
  font-size: 1.15rem;
  line-height: 1.6;
  margin-bottom: 0.5rem;
}

:deep(.line-output) {
  font-size: 0.55rem;
  line-height: 1.25;
}
</style>

<!--
notes:
- Frame this as the last CLI step: "Last one on the command line — we're
  connecting the far end of the pipeline: plot_zone_map's output, all the
  way out to the workflow's final output."

- Before running: "Notice the direction here is reversed from the last two
  — --from is now a step's output, plot_zone_map/zone_map_png, and --to is
  a plain workflow-level output, zone_map_png."

- As the diff appears: "The outputs section, which was empty, now declares
  zone_map_png as a File, with outputSource pointing back at
  plot_zone_map/zone_map_png — that's the traceability we talked about
  earlier, you can always see exactly which step produced a given output."

- Point out the new steps entry: "And notice plot_zone_map itself now
  appears in the steps list too — but look closely at its 'in' field: it
  says 'in: []' — empty. That's intentional and important."
  → Pause here deliberately: "This step has no inputs connected yet. That's
  exactly the gap you're going to fill in Studio — plot_zone_map needs
  ndvi and fertility, and right now it has neither."

- Bridge: "So to recap — three CLI commands, two inputs and one output
  wired up. But our workflow is still incomplete, because plot_zone_map
  isn't receiving anything yet. Let's look at a reference slide with these
  commands, then head into Studio to finish the job visually."

Timing: ~2 min. Don't rush past the "in: []" observation — it's the natural
setup for why the Studio exercise is necessary, so let that land clearly.
-->

---
layout: fairagro 
title: "Reference — SciWIn-Client connect commands"
disabled: true
---
<script setup>
import { ref } from 'vue'

const copiedIndex = ref(null)

function copyCommand(text, index) {
  navigator.clipboard.writeText(text).then(() => {
    copiedIndex.value = index
    setTimeout(() => { copiedIndex.value = null }, 1500)
  })
}

const cmd1 = 's4n connect workflow --from reflectance --to compute_ndvi/reflectance'
const cmd2 = 's4n connect workflow --from soil --to compute_fertility/soil'
const cmd3 = 's4n connect workflow --from plot_zone_map/zone_map_png --to zone_map_png'
</script> <div class="fa-bar"></div> <style> .ref-page{ font-family:'Fira Sans',sans-serif; } .ref-section{ border-radius:12px; padding:10px 16px; background:linear-gradient(180deg,#fbfbfd 0%,#f4f5f9 100%); border:1px solid #e6e7ee; margin-bottom:0.7rem; } .ref-label{ font-size:0.76rem; font-weight:700; color:#0f9884; text-transform:uppercase; letter-spacing:.03em; margin-bottom:6px; } .ref-cmd-wrap{ position:relative; display:flex; align-items:flex-start; gap:8px; } .ref-cmd{ flex:1; min-width:0; font-family:'Fira Code','Courier New',monospace; font-size:0.74rem; color:#374151; background:#ffffff; border:1px solid #e5e7eb; border-radius:6px; padding:7px 10px; line-height:1.5; word-break:break-word; } .ref-cmd .prompt{ color:#0f9884; font-weight:700; margin-right:6px; } .copy-btn{ flex-shrink:0; display:flex; align-items:center; gap:4px; font-family:'Fira Sans',sans-serif; font-size:0.66rem; font-weight:700; color:#0f9884; background:#ffffff; border:1px solid #cdeee6; border-radius:6px; padding:7px 9px; cursor:pointer; transition:all 0.15s ease; white-space:nowrap; } .copy-btn:hover{ background:#f2fbf9; border-color:#0f9884; } .copy-btn.copied{ background:#0f9884; border-color:#0f9884; color:#ffffff; } .ref-note{ margin-top:6px; font-size:0.76rem; color:#4b5563; line-height:1.4; } .ref-note code{ background:#f0f0f0; padding:0.02rem 0.3rem; border-radius:3px; } </style> <div class="ref-page"> <div class="ref-section"> <div class="ref-label">1️⃣ Connect workflow input → step</div> <div class="ref-cmd-wrap"> <div class="ref-cmd"><span class="prompt">$</span>s4n connect workflow --from reflectance --to compute_ndvi/reflectance</div> <button class="copy-btn" :class="{ copied: copiedIndex === 1 }" @click="copyCommand(cmd1, 1)"> {{ copiedIndex === 1 ? '✓ Copied' : '📋 Copy' }} </button> </div> <div class="ref-note">Wires the <code>reflectance</code> workflow input into <code>compute_ndvi</code>.</div> </div> <div class="ref-section"> <div class="ref-label">2️⃣ Connect workflow input → step</div> <div class="ref-cmd-wrap"> <div class="ref-cmd"><span class="prompt">$</span>s4n connect workflow --from soil --to compute_fertility/soil</div> <button class="copy-btn" :class="{ copied: copiedIndex === 2 }" @click="copyCommand(cmd2, 2)"> {{ copiedIndex === 2 ? '✓ Copied' : '📋 Copy' }} </button> </div> <div class="ref-note">Wires the <code>soil</code> workflow input into <code>compute_fertility</code>.</div> </div> <div class="ref-section"> <div class="ref-label">3️⃣ Connect step → workflow output</div> <div class="ref-cmd-wrap"> <div class="ref-cmd"><span class="prompt">$</span>s4n connect workflow --from plot_zone_map/zone_map_png --to zone_map_png</div> <button class="copy-btn" :class="{ copied: copiedIndex === 3 }" @click="copyCommand(cmd3, 3)"> {{ copiedIndex === 3 ? '✓ Copied' : '📋 Copy' }} </button> </div> <div class="ref-note">Exposes <code>plot_zone_map</code>'s output as the final workflow output.</div> </div> </div>

<!--
notes:
- Standard reference/lookup slide — keep narration brief.

- Say: "Just like before, here's a reference slide with copy buttons for
  all three commands we just ran — the two input connections and the
  output connection. Feel free to pause here if you want to copy these for
  your own notes."

- Optional: briefly reiterate the pattern one more time for reinforcement:
  "Notice again — first two commands go from a plain name into a
  step/port; the third goes from a step/port into a plain name. Same
  --from/--to structure throughout."

- Bridge: "Now, the part you've been waiting for — let's open SciWIn-Studio
  and finish this workflow by hand."

Timing: ~30-60 sec, or longer if participants are actively copying/running
commands themselves before moving on.
-->


---
layout: fairagro
title: Install SciWIn-Studio
---

<div class="text-sm leading-snug">

Download from the official release page: https://github.com/fairagro/sciwin_studio/releases/tag/v1.0.1 and download:

## Windows

1. Download the `.exe` (or `.msi`) installer from the table above.
2. Run the installer. Windows SmartScreen may show a warning since the app isn't signed. Click **"More info"** (*"Weitere Informationen"*) and then **"Run anyway"** (*"Trotzdem ausführen"*).
3. Follow the installation prompts.

## Linux

**.deb** (Ubuntu/Debian): `sudo dpkg -i SciWIn-Studio_1.0.1_amd64.deb` and `gtk-launch SciWIn-Studio`

## macOS

1. Download the `.dmg` file matching your chip.
2. Open the `.dmg` and drag SciWIn-Studio into Applications.

</div>


---
layout: fairagro 
title: Build the Workflow in SciWIn-Studio
---
<div class="fa-logo-title"></div> <div class="fa-bar"></div> <style> .slidev-layout{ height:100%; display:flex; flex-direction:column; } .ex-page{ flex:1; min-height:0; display:flex; flex-direction:column; font-family:'Fira Sans',sans-serif; } .ex-task{ border-radius:10px; padding:8px 12px; background:linear-gradient(180deg,#fbfbfd 0%,#f4f5f9 100%); border:1px solid #e6e7ee; box-shadow:0 2px 8px rgba(20,20,40,0.05); margin-bottom:0.6rem; flex-shrink:0; } .ex-task-label{ font-size:0.75rem; font-weight:700; color:#0f9884; text-transform:uppercase; letter-spacing:.03em; margin-bottom:2px; } .ex-task-text{ font-size:0.85rem; color:#374151; line-height:1.4; } .ex-task-text code{ background:#f0f0f0; padding:0.02rem 0.3rem; border-radius:3px; } .ex-columns{ flex:1; min-height:0; display:flex; gap:20px; align-items:flex-start; } .ex-hints{ flex:0 0 32%; min-height:0; display:flex; flex-direction:column; gap:0.4rem; } .ex-reference{ flex:1; min-width:0; display:flex; flex-direction:column; } .hint-box, .solution-box, .reference-box{ border-radius:8px; border:1.2px solid #e6e7ee; background:#fafafc; padding:6px 9px; flex-shrink:0; width:100%; box-sizing:border-box; } .hint-box summary, .solution-box summary, .reference-box summary{ cursor:pointer; font-size:0.75rem; font-weight:700; color:#333; list-style:none; display:flex; align-items:center; gap:5px; } .hint-box summary::-webkit-details-marker, .solution-box summary::-webkit-details-marker, .reference-box summary::-webkit-details-marker{ display:none; } .hint-box summary::before{ content:'▸'; color:#2f6fed; font-size:0.78rem; transition:transform .15s ease; } .hint-box[open] summary::before{ transform:rotate(90deg); } .hint-box{ border-color:#bcd3ff; } .hint-box[open]{ background:#e7f0ff; } .solution-box summary::before{ content:'▸'; color:#0f9884; font-size:0.78rem; transition:transform .15s ease; } .solution-box[open] summary::before{ transform:rotate(90deg); } .solution-box{ border-color:#cfe6cf; } .solution-box[open]{ background:#f2f9f2; } .hint-content, .solution-content{ margin-top:5px; font-size:0.75rem; line-height:1.5; color:#374151; width:100%; box-sizing:border-box; text-align:left; } .hint-content code, .solution-content code{ background:#f0f0f0; padding:0.02rem 0.3rem; border-radius:3px; } .hint-content ul{ margin:4px 0 0 0; padding-left:1.1rem; } .hint-content li{ margin-bottom:4px; } .cmd-line{ font-family:'Fira Code','Courier New',monospace; font-size:0.7rem; color:#4b4f5e; line-height:1.5; word-break:break-word; background:#fff; border:1px solid #e5e7eb; border-radius:6px; padding:5px 8px; margin-top:4px; } .cmd-line .prompt{ color:#0f9884; font-weight:700; margin-right:4px; } .download-link{ display:inline-block; margin-top:6px; font-size:0.75rem; font-weight:600; color:#fff; background:#0f9884; padding:5px 10px; border-radius:6px; text-decoration:none; } .download-link:hover{ background:#0c7c6d; } .solution-img{ display:block !important; width:100% !important; max-width:100% !important; height:auto !important; margin:6px 0 0 0 !important; border-radius:8px; border:1px solid #e5e7eb; box-shadow:0 2px 10px rgba(20,20,40,0.08); } </style> <div class="ex-page"> <div class="ex-task"> <div class="ex-task-label">🎯 Your Task</div> <div class="ex-task-text"> Create a new workflow in <b>SciWIn-Studio</b>, add <code>compute_ndvi</code>, <code>compute_fertility</code> and <code>plot_zone_map</code> as steps, and visually connect <b>all five edges</b> — two workflow inputs, two step-to-step connections, and the final output — by dragging between the matching ports. </div> </div> <div class="ex-columns"> <div class="ex-hints">  <details class="hint-box"> <summary>💡 Hint — How to add steps and draw connections?</summary> <div class="hint-content"> Start by clicking on '+' to create a new workflow. Then drag and drop the cwl step files onto the canvas. Create a connection by clicking on the output port of a tool and dragging the line to its matching input port. </div> </details> </div> <div class="ex-reference"> <details class="solution-box"> <summary>✅ Show solution</summary> <div class="solution-content"> Once fully connected, your workflow graph in SciWIn-Studio should look like this: <img class="solution-img" src="/workflow_session_2.PNG" alt="Connected workflow in SciWIn-Studio" /> </div> </details> </div> </div> </div> 

<!--
notes:
- Transition energy: "Now for the fun part — no typing commands at all,
  we're going to build this whole workflow visually, start to finish."

- Read the task box: "Your job is to open SciWIn-Studio, start a new
  workflow, add compute_ndvi, compute_fertility, and plot_zone_map as
  steps, and then wire up all five connections — the two workflow inputs,
  the two step-to-step edges, and the final output — by dragging between
  ports."

- Point out the download hint box (expanded by default): "If you haven't
  already, grab SciWIn-Studio from the GitHub releases page — it's a
  desktop app, available for Windows, macOS, and Linux. Take a minute now
  if you need to install it."
  → Give people a moment here if installation is needed.

- Point out Hint 2: "Start a new workflow in Studio and add the three .cwl
  tools you built in Session 1 as steps — you should see all three
  represented as boxes, with no connections between them yet."

- Explain exactly what to connect, in order: "First, the two workflow
  inputs — reflectance into compute_ndvi, and soil into compute_fertility.
  Then the two step-to-step edges — compute_ndvi's ndvi_csv output into
  plot_zone_map's ndvi input, and compute_fertility's fertility_csv output
  into plot_zone_map's fertility input. Finally, plot_zone_map's
  zone_map_png output out to the workflow's final output."

- Reassure: "SciWIn-Studio writes the actual workflow.cwl file
  automatically as you drag — so there's no syntax to get wrong here, just
  make sure you're connecting the right ports."

- Give working time: "Take about 10-15 minutes to get this working. If
  you're not sure whether you've done it right, there's a solution image
  under 'Show solution' you can compare against — try not to peek until
  you've given it a real attempt though."

- While people work: circulate and help with port-matching confusion (a
  common mistake is trying to connect an output port to another output
  port, or connecting to the wrong step entirely if multiple ports look
  similar).

- After time is up, reveal the solution image together: "Let's compare —
  open the solution reveal. Your graph should look like this, with
  everything now fully connected from inputs all the way through to the
  final zone_map_png output."

- Close out the session: "And with that, Anna and Ben's workflow is
  complete — a single, reproducible, portable file that runs their entire
  pipeline: two languages, three tools, zero manual copying of files
  between steps."

Timing: ~10-15 min total including setup, working time, and review. This is
the culminating exercise of Session 2 — give it the time it needs, since
successfully completing this is the emotional payoff of the whole workshop
so far.
-->

---
layout: fairagro
title: "SciWIn-Studio: Open a Project" 
---

<img src="/open_folder.png" class="h-100 w-full object-contain mx-auto" />


---
layout: fairagro
title: "SciWIn-Studio: Create a new workflow"
---

<img src="/create_wf.png" class="h-100 w-full object-contain mx-auto" />

---
layout: fairagro
title: "SciWIn-Studio: Add new steps via drag & drop"
---

<img src="/drag_n_drop.png" class="h-100 w-full object-contain mx-auto" />

---
layout: fairagro
title: "SciWIn-Studio: Connect workflow steps"
---

<img src="/connect_tools.png" class="h-100 w-full object-contain mx-auto" />

---
layout: fairagro
title: "SciWIn-Studio: Add workflow inputs"
---

<img src="/add_wf_inputs.png" class="h-100 w-full object-contain mx-auto" />

---
layout: fairagro
title: "SciWIn-Studio: Save workflow"
disabled: true
---

<img src="/save_wf.png" class="h-100 w-full object-contain mx-auto" />

---
layout: fairagro
title: The complete workflow in SciWIn-Studio
disabled: true
---

<div class="fa-bar"></div>

<div class="studio-tour h-100 w-full">

  <div class="studio-gif-wrap">
    <img src="/create_workflow_linux.gif" alt="Creating and connecting a CWL workflow visually in SciWIn-Studio" class="studio-gif" />
  </div>

</div>

<style scoped>
.studio-tour {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.9rem;
}
.studio-gif-wrap {
  width: 100%;
  max-width: 760px;
}
.studio-gif {
  display: block;
  width: 100%;
  height: auto;
  border-radius: 10px;
  border: 1px solid #e5e7eb;
  box-shadow: 0 6px 20px rgba(20, 20, 40, 0.12);
}
.studio-features {
  display: flex;
  gap: 12px;
  width: 100%;
  max-width: 900px;
}
.studio-feature {
  flex: 1;
  display: flex;
  align-items: flex-start;
  gap: 8px;
  border-radius: 12px;
  padding: 10px 12px;
  background: linear-gradient(160deg, #ffffff 0%, #f2fbf9 100%);
  border: 1.5px solid #cdeee6;
  box-shadow: 0 4px 12px rgba(15, 152, 132, 0.08);
  font-family: 'Fira Sans', sans-serif;
}
.sf-icon {
  font-size: 1.1rem;
  flex-shrink: 0;
}
.sf-text {
  font-size: 0.78rem;
  line-height: 1.35;
  color: #374151;
}
.sf-text b {
  color: #0b6f60;
}
.sf-text code {
  background: #f0f0f0;
  padding: 0.02rem 0.3rem;
  border-radius: 4px;
  font-size: 0.9em;
}
</style>

<!--
notes:
- Play the clip and narrate along with it: "This is SciWIn-Studio, start to
  finish — creating a new workflow, dragging in the three tools we built
  last session, and wiring up every connection by dragging between ports.
  No command line at all."

- Point at the three feature callouts below:
  - "Visual canvas: every tool shows up as a node on the canvas, connected
    by lines that represent the actual data flowing between them."
  - "Drag to connect: click an output port on one tool, drag to the
    matching input port on another — that's the entire interaction."
  - "Always in sync: you're not editing a diagram that's disconnected from
    reality — every drag you make is written straight into the real
    workflow.cwl file underneath."

- Bridge: "That's exactly what you're about to do yourselves — let's open
  Studio for real."

Timing: ~1 min. Let the clip do the talking — this is a preview to build
confidence before the hands-on exercise, not a deep explanation.
-->
