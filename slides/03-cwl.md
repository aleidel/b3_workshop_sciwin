---
layout: fairagro
title: Common Workflow Language (CWL)
routeAlias: cwl-basics
---

- **Open standard for describing computational workflows**
- Describes what to run not how to
- Based on **YAML**: human-readable and machine-executable

<style>
/* Restore original box position by removing the component's default top margin */
.why-box {
  margin-top: 0 !important;
}
</style>

<Box
  label="Why is CWL useful?"
  :startClick="0"
  :items="[
    { strong: '🔄 Reproducible:', text: 'Capture every step with tools, runtime environment, parameters, data' },
    { strong: '🌍 Portable:', text: 'Run workflows on local machines, HPC, cloud (de.NBI)' },
    { strong: '🛠️ Tool-Agnostic:', text: 'Integrate Python, R, Bash, Docker, Singularity, etc.' },
    { strong: '📥 Clear Inputs/Outputs:', text: 'Define data types and expected results explicitly' },
    { strong: '⚙️ Automated Data Flow:', text: 'Pass data between steps without manual scripting' },
    { strong: '🤝 Collaborative:', text: 'Share, reuse, and extend workflows across teams and institutions' },
    { strong: '🚀 Scalable:', text: 'Designed for big data and distributed computing environments' },
  ]"
/>

<!--
notes:
- Bridge from the previous slide: "So we just said there are 300+ workflow
  tools out there. For this session, we're going to focus on one of the most
  widely adopted ones in bioinformatics and research computing: the Common
  Workflow Language, or CWL."

- Walk through the three bullet points at the top:
  - "It's an open standard" — not tied to one company or one specific
    software. Multiple engines can run the same CWL file.
  - "Describes WHAT to run, not HOW to run it" — this is the key mental
    model. You're not writing a program; you're describing a computation
    declaratively. The engine figures out the "how" (scheduling, execution,
    containerization).
  - "Based on YAML" — reassure the audience this isn't a brand-new
    programming language. If they've written a Docker-compose file or a
    GitHub Actions workflow, the syntax will feel familiar.

- Move into the "Why is CWL useful?" box. Go through the 7 items at a
  comfortable pace — you don't need to read each one verbatim, paraphrase
  and give a one-sentence example tied back to Anna & Ben where it helps:
  - Reproducible → "No more 'works on my machine' — the exact environment
    is captured."
  - Portable → "Anna could develop locally, then Ben runs the same workflow
    on an HPC cluster without changes."
  - Tool-Agnostic → "This is huge for Anna and Ben specifically — Python and
    R can live side by side in the same workflow."
  - Clear Inputs/Outputs → ties back to the "USE_THIS_ONE.csv" problem from
    earlier — CWL forces you to explicitly declare what a step produces.
  - Automated Data Flow → no more manually copying file paths between
    scripts.
  - Collaborative → workflows can be shared and reused like building blocks.
  - Scalable → briefly mention this matters for bigger datasets/HPC/cloud,
    but don't dwell — it's not the focus of today's session.

- Close with a forward-looking line: "Let's look at what a CWL file actually
  looks like — starting with the smallest building block: a single tool."

Timing: ~2 min. Don't over-explain each bullet in the box — the goal is
recognition ("oh, that solves a problem we just saw"), not deep technical
detail yet.
-->

---
layout: fairagro
title: CWL CommandLineTools
---

<div class="fa-logo-title"></div>
<div class="fa-bar"></div>

<style>
.cwl-wrap{ display:flex; gap:28px; align-items:flex-start; font-family:'Fira Sans',sans-serif; }

/* ---------- Left column: explanation ---------- */
.cwl-text{ flex:1; min-width:0; }
.cwl-intro{ font-size:1rem; line-height:1.6; margin-bottom:1rem; color:#333; padding-left:1.4em; }
.cwl-intro li{ margin-bottom:0.3rem; }

/* ---------- Workflow-context schematic (modernized) ---------- */
.cwl-workflow-context{
  margin-bottom:1.2rem;
  border-radius:14px;
  padding:14px 16px 14px;
  background:linear-gradient(180deg,#fbfbfd 0%,#f4f5f9 100%);
  border:1px solid #e6e7ee;
  box-shadow:0 2px 10px rgba(20,20,40,0.05);
}
.cwl-workflow-title{
  font-size:0.68rem; font-weight:700; color:#6b6f80;
  text-transform:uppercase; letter-spacing:.04em;
  margin-bottom:10px; display:flex; align-items:center; gap:6px;
}
.cwl-workflow-title .wf-icon{ font-size:0.85rem; }

.wf-outer{
  border:1.5px dashed #c7cadb;
  border-radius:12px;
  padding:12px 10px 10px;
  background:#ffffff;
  position:relative;
}
.wf-outer-label{
  position:absolute; top:-9px; left:12px;
  background:#ffffff; padding:0 6px;
  font-size:0.58rem; font-weight:700; color:#8b8fa3;
  text-transform:uppercase; letter-spacing:.03em;
}

.wf-steps{
  display:flex; align-items:center; justify-content:center; gap:2px;
}
.wf-step{
  flex:1; display:flex; flex-direction:column; align-items:center;
  gap:4px; padding:9px 4px; border-radius:10px;
  background:#f1f2f6; color:#8b8fa3;
  transition:transform .15s ease;
}
.wf-step .wf-icon-badge{
  width:22px; height:22px; border-radius:6px;
  display:flex; align-items:center; justify-content:center;
  font-size:0.72rem; background:#e2e4ee; color:#8b8fa3;
}
.wf-step .wf-step-label{
  font-size:0.58rem; font-weight:700; text-align:center; line-height:1.2;
}
.wf-step .wf-step-sub{
  font-size:0.5rem; color:#a7aabb; text-align:center; line-height:1.15;
}

.wf-step.highlight{
  background:linear-gradient(180deg,#f4effd 0%,#ece3fb 100%);
  box-shadow:0 3px 10px rgba(123,95,209,0.22);
  transform:translateY(-2px);
}
.wf-step.highlight .wf-icon-badge{
  background:#7b5fd1; color:#fff;
}
.wf-step.highlight .wf-step-label{ color:#5c3fc7; }
.wf-step.highlight .wf-step-sub{ color:#7b5fd1; font-weight:600; }

.wf-arrow-h{
  color:#c7cadb; font-size:0.95rem; flex:0 0 auto; padding:0 2px;
}

.wf-caption{
  display:flex; align-items:center; gap:6px;
  margin-top:10px; padding-top:9px;
  border-top:1px dashed #e6e7ee;
  font-size:0.66rem; color:#5c6070; line-height:1.4;
}
.wf-caption .dot-inline{
  flex-shrink:0; width:7px; height:7px; border-radius:50%;
  background:#7b5fd1; margin-top:2px;
}
.wf-caption b{ color:#5c3fc7; }

.cwl-legend-title{
  font-weight:700; font-size:0.8rem; color:#0f9884;
  text-transform:uppercase; letter-spacing:.03em; margin-bottom:0.5rem;
}

.cwl-legend-item{
  display:flex; align-items:flex-start; gap:8px;
  margin-bottom:0.4rem;
}
.cwl-legend-item .dot{
  flex-shrink:0; width:8px; height:8px; border-radius:50%; margin-top:4px;
}
.cwl-legend-item .txt{ font-size:0.76rem; line-height:1.35; }
.cwl-legend-item .txt b{ font-weight:700; }
.cwl-legend-item code{
  background:#f0f0f0; padding:0.03rem 0.3rem; border-radius:3px; font-size:0.85em;
}

.dot.meta{ background:#9e9e9e; }
.dot.input{ background:#2f6fed; }
.dot.runtime{ background:#43a047; }
.dot.command{ background:#7b5fd1; }
.dot.output{ background:#e0524f; }
.dot.result{ background:#0f9884; }

.cwl-hint{
  font-size:0.68rem; color:#999; font-style:italic; margin-top:0.5rem;
}

/* ---------- Right column: animated diagram (slightly smaller) ---------- */
.cwl-diagram{ flex:0 0 300px; display:flex; flex-direction:column; align-items:stretch; }
.cwl-diagram-title{
  text-align:center; font-weight:700; font-size:0.78rem; color:#333;
  margin-bottom:5px;
}

.cwl-card{
  border-radius:7px;
  padding:5px 9px;
  box-shadow:0 1px 5px rgba(0,0,0,0.07);
  margin:0;
}
.cwl-card-label{
  font-size:0.56rem; font-weight:700; text-transform:uppercase;
  letter-spacing:.03em; margin-bottom:2px; display:flex; align-items:center; gap:5px;
}
.cwl-card-code{
  font-family:'Fira Code','Courier New',monospace;
  font-size:0.62rem; line-height:1.25; margin:0; white-space:pre;
}

.cwl-card.meta{ background:#f4f4f5; }
.cwl-card.meta .cwl-card-label{ color:#8a8a8a; }

.cwl-card.input{ background:#e7f0ff; }
.cwl-card.input .cwl-card-label{ color:#2f6fed; }

.cwl-card.runtime{ background:#eaf7e6; }
.cwl-card.runtime .cwl-card-label{ color:#43a047; }

.cwl-card.command{ background:#f2eefb; }
.cwl-card.command .cwl-card-label{ color:#7b5fd1; }

.cwl-card.output{ background:#fde7e6; }
.cwl-card.output .cwl-card-label{ color:#e0524f; }

.cwl-card.result{
  background:#ffffff; border:1.5px dashed #0f9884;
}
.cwl-card.result .cwl-card-label{ color:#0f9884; }
.cwl-card.result .cwl-card-code{ color:#0f9884; font-weight:600; }

.cwl-arrow{
  text-align:center; font-size:1rem; color:#0f9884;
  line-height:1; margin:0;
}
</style>

<div class="cwl-wrap">

<div class="cwl-text">

<ul class="cwl-intro">
  <li>Wraps a <b>single command-line program</b> as a reusable, portable step</li>
  <li>Describes the executable, its inputs, outputs, and how to run it</li>
</ul>

<div class="cwl-workflow-context">
  <div class="cwl-workflow-title"><span class="wf-icon">🔗</span> Where it fits: inside a Workflow</div>

  <div class="wf-outer">
    <span class="wf-outer-label">Workflow</span>
    <div class="wf-steps">
      <div class="wf-step">
        <div class="wf-icon-badge">⚙️</div>
        <div class="wf-step-label">Step 1</div>
        <div class="wf-step-sub">CommandLineTool</div>
      </div>
      <div class="wf-arrow-h">→</div>
      <div class="wf-step highlight">
        <div class="wf-icon-badge">⚙️</div>
        <div class="wf-step-label">Step 2</div>
        <div class="wf-step-sub">this tool</div>
      </div>
      <div class="wf-arrow-h">→</div>
      <div class="wf-step">
        <div class="wf-icon-badge">⚙️</div>
        <div class="wf-step-label">Step 3</div>
        <div class="wf-step-sub">CommandLineTool</div>
      </div>
    </div>
  </div>
</div>

<div class="cwl-legend-title" v-click="1">Components</div>

<div class="cwl-legend-item" v-click="1">
  <div class="dot meta"></div>
  <div class="txt">🏷️ <b>Metadata</b> — <code>class: CommandLineTool</code> and <code>cwlVersion</code></div>
</div>

<div class="cwl-legend-item" v-click="2">
  <div class="dot input"></div>
  <div class="txt">📥 <b>Inputs</b> — <code>soil</code> file passed to the command via <code>--soil</code></div>
</div>
<div class="cwl-legend-item" v-click="3">
  <div class="dot output"></div>
  <div class="txt">📤 <b>Outputs</b> — <code>fertility</code> file captured via <code>glob</code></div>
</div>
<div class="cwl-legend-item" v-click="4">
  <div class="dot runtime"></div>
  <div class="txt">🧩 <b>Runtime</b> — runs inside a <code>r-base:4.4.1</code> Docker container</div>
</div>

<div class="cwl-legend-item" v-click="5">
  <div class="dot command"></div>
  <div class="txt">⚡ <b>Command</b> — executes <code>Rscript compute_fertility.R</code></div>
</div>


</div>

<div class="cwl-diagram">
  <div class="cwl-diagram-title" v-click="1">CommandLineTool</div>

  <div class="cwl-card meta" v-click="1">
    <div class="cwl-card-label">🏷️ Metadata</div>
    <pre class="cwl-card-code">cwlVersion: v1.2
class: CommandLineTool</pre>
  </div>

  <div class="cwl-card input" v-click="2">
    <div class="cwl-card-label">📥 Input Parameters</div>
    <pre class="cwl-card-code">inputs:
- id: soil
  type: File
  default:
    class: File
    location: ../../data/soil.csv
  inputBinding:
    prefix: --soil</pre>
  </div>

  
<div class="cwl-card output" v-click="3">
    <div class="cwl-card-label">📤 Output Parameters</div>
    <pre class="cwl-card-code">outputs:
- id: fertility
  type: File
  outputBinding:
    glob: $(inputs.output)</pre>
  </div>

  <div class="cwl-card runtime" v-click="4">
    <div class="cwl-card-label">🧩 Runtime Environment</div>
    <pre class="cwl-card-code">requirements:
- class: DockerRequirement
  dockerPull: r-base:4.4.1</pre>
  </div>


  <div class="cwl-card command" v-click="5">
    <div class="cwl-card-label">⚡ Command</div>
    <pre class="cwl-card-code">baseCommand:
- Rscript
- code/compute_fertility/compute_fertility.R</pre>
  </div>


</div>

</div>

<!--
notes:
- Set up the concept before revealing anything: "The smallest building block
  in CWL is called a CommandLineTool. It wraps a single command-line program
  — like a Python script or an R script — and describes it in a
  standardized way."

- Point at the schematic (workflow-context box) at the top: "If a workflow
  is a chain of steps, a CommandLineTool is just one link in that chain —
  here we're zooming into Step 2." This helps the audience keep the mental
  model of "this is a piece of a bigger picture," not the whole thing.

- We'll walk through this using Ben's fertility computation script as the
  real example — this is literally Ben's R script, now wrapped as a CWL
  tool.

- [Click 1] Metadata card appears on the right, "Components" legend starts
  on the left.
  → Say: "First, some basic metadata: which CWL version we're using, and
  that this is a CommandLineTool — that's it, nothing fancy."

- [Click 2] Input card appears.
  → Say: "Next, the inputs. Here we declare that this tool expects a file
  called 'soil' — and CWL even tells us exactly how it gets passed to the
  command: as a --soil flag. No more guessing what argument order a script
  expects."

- [Click 3] Output card appears.
  → Say: "Then the outputs — we tell CWL to look for a file matching a
  certain pattern (glob) once the command finishes, and call it 'fertility'.
  This is the fix for our 'USE_THIS_ONE.csv' problem from earlier — the
  output is explicitly named and declared, not guessed."

- [Click 4] Runtime card appears.
  → Say: "This is where it gets powerful — the runtime requirement says this
  tool always runs inside a Docker container with r-base version 4.4.1.
  That means Ben's collaborators don't need R installed at all, let alone
  the right version. The container has it baked in."

- [Click 5] Command card appears.
  → Say: "Finally, the actual command that gets executed — just calling
  Rscript on Ben's compute_fertility.R script. Everything above this is
  essentially metadata and configuration; this line is the only part that
  actually 'does' anything."

- Wrap-up: "So in one file, we've fully described: what version of CWL, what
  inputs it needs, what outputs to expect, what environment to run it in,
  and what command to execute. This single file is now something Anna,
  or anyone else, can run — without ever opening R or installing a single
  package themselves."

- Bridge to next slide: "But one tool on its own isn't a workflow yet — we
  need to chain multiple tools together. That's what a CWL Workflow file
  does, and that's what we'll look at next."

Timing: ~3 min. Let each click breathe — this is dense information, so pace
yourself and use the color-coded cards as anchors ("the purple box," "the
blue box") to help the audience follow along visually.
-->

---
layout: fairagro
title: CWL Workflows
---

<div class="fa-logo-title"></div>
<div class="fa-bar"></div>

<style>
.cwl-wrap{ display:flex; gap:28px; align-items:flex-start; font-family:'Fira Sans',sans-serif; }

/* ---------- Left column: explanation ---------- */
.cwl-text{ flex:1; min-width:0; }
.cwl-intro{ font-size:1rem; line-height:1.6; margin-bottom:1rem; color:#333; padding-left:1.4em; }
.cwl-intro li{ margin-bottom:0.3rem; }

.cwl-legend-title{
  font-weight:700; font-size:0.8rem; color:#0f9884;
  text-transform:uppercase; letter-spacing:.03em; margin-bottom:0.5rem;
}

.cwl-legend-item{
  display:flex; align-items:flex-start; gap:8px;
  margin-bottom:0.4rem;
}
.cwl-legend-item .dot{
  flex-shrink:0; width:8px; height:8px; border-radius:50%; margin-top:4px;
}
.cwl-legend-item .txt{ font-size:0.76rem; line-height:1.35; }
.cwl-legend-item .txt b{ font-weight:700; }
.cwl-legend-item code{
  background:#f0f0f0; padding:0.03rem 0.3rem; border-radius:3px; font-size:0.85em;
}

.dot.meta{ background:#9e9e9e; }
.dot.input{ background:#2f6fed; }
.dot.output{ background:#e0524f; }
.dot.steps{ background:#7b5fd1; }

/* ---------- Bottom callout (left column, red) ---------- */
.cwl-callout{
  border-radius:14px;
  padding:14px 16px 14px;
  background:linear-gradient(180deg,#fef6f5 0%,#fdeceb 100%);
  border:1px solid #f3d3d1;
  box-shadow:0 2px 10px rgba(180,40,40,0.06);
}
.cwl-callout-outer{
  border:1.5px dashed #e0928d;
  border-radius:12px;
  padding:14px 14px 12px;
  background:#ffffff;
  position:relative;
}
.cwl-callout-outer-label{
  position:absolute; top:-9px; left:12px;
  background:#ffffff; padding:0 6px;
  font-size:0.58rem; font-weight:700; color:#c0392b;
  text-transform:uppercase; letter-spacing:.03em;
}
.cwl-callout-body{
  display:flex; align-items:flex-start; gap:10px;
}
.cwl-callout .callout-icon{ font-size:1.2rem; flex-shrink:0; margin-top:1px; }
.cwl-callout .callout-txt{ font-size:0.8rem; line-height:1.45; color:#8a2e28; margin:0; }
.cwl-callout .callout-txt b{ color:#c0392b; }

/* ---------- Right column: accordion diagram ---------- */
.cwl-diagram{
  flex:0 0 300px;
  display:flex;
  flex-direction:column;
  align-items:stretch;
}
.cwl-diagram-title{
  text-align:center; font-weight:700; font-size:0.75rem; color:#333;
  margin-bottom:4px;
}

/* IMPORTANT: force Slidev's click-hidden elements to collapse fully
   (no reserved space) instead of the default opacity:0 fade,
   so the accordion doesn't leave gaps where hidden cards used to be. */
.cwl-diagram .slidev-vclick-hidden{
  display:none !important;
}

.cwl-card{
  border-radius:6px;
  padding:5px 9px;
  box-shadow:0 1px 4px rgba(0,0,0,0.07);
  margin:0 0 4px 0;
}
.cwl-card-label{
  font-size:0.58rem; font-weight:700; text-transform:uppercase;
  letter-spacing:.03em; margin-bottom:2px; display:flex; align-items:center; gap:5px;
}
.cwl-card-code{
  font-family:'Fira Code','Courier New',monospace;
  font-size:0.7rem; line-height:1.2; margin:0; white-space:pre;
}

/* Collapsed variant: super-thin, headline only */
.cwl-card.collapsed{
  padding:2px 9px;
  margin-bottom:2px;
  line-height:1;
}
.cwl-card.collapsed .cwl-card-label{
  margin-bottom:0;
  font-size:0.54rem;
}

.cwl-card.meta{ background:#f4f4f5; }
.cwl-card.meta .cwl-card-label{ color:#8a8a8a; }

.cwl-card.input{ background:#e7f0ff; }
.cwl-card.input .cwl-card-label{ color:#2f6fed; }

.cwl-card.output{ background:#fde7e6; }
.cwl-card.output .cwl-card-label{ color:#e0524f; }

.cwl-card.steps{ background:#f2eefb; }
.cwl-card.steps .cwl-card-label{ color:#7b5fd1; }
</style>

<div class="cwl-wrap">

<div class="cwl-text">

<ul class="cwl-intro">
  <li>Chains multiple <b>CommandLineTools</b> (or sub-workflows) into a <b>pipeline</b></li>
  <li><b>Defines how data flows</b>: outputs of one step become inputs of the next</li>
  <li>Describes overall inputs, outputs, and the steps that connect them</li>
</ul>

<div class="cwl-legend-title" v-click="1">Components</div>

<div class="cwl-legend-item" v-click="1">
  <div class="dot meta"></div>
  <div class="txt">🏷️ <b>Metadata</b> — <code>class: Workflow</code> and <code>cwlVersion</code></div>
</div>

<div class="cwl-legend-item" v-click="2">
  <div class="dot input"></div>
  <div class="txt">📥 <b>Inputs</b> — <code>reflectance</code> and <code>soil</code> files available to the whole workflow</div>
</div>
<div class="cwl-legend-item" v-click="3">
  <div class="dot output"></div>
  <div class="txt">📤 <b>Outputs</b> — final result <code>zone_map_png</code>, sourced from <code>plot_zone_map/zone_map</code> via <code>outputSource</code></div>
</div>
<div class="cwl-legend-item" v-click="4">
  <div class="dot steps"></div>
  <div class="txt">🔗 <b>Steps</b> — <code>compute_ndvi</code> and <code>compute_fertility</code> run independently, then <code>plot_zone_map</code> consumes both results to produce the final map</div>
</div>
<br>

</div>

<div class="cwl-diagram">
  <div class="cwl-diagram-title" v-click="1">Workflow</div>

  <!-- ===== Metadata: expanded at click 1, collapses at click 2 ===== -->
  <div class="cwl-card meta" v-click="[1,2]">
    <div class="cwl-card-label">🏷️ Metadata</div>
    <pre class="cwl-card-code">cwlVersion: v1.2
class: Workflow</pre>
  </div>
  <div class="cwl-card meta collapsed" v-click="2">
    <div class="cwl-card-label">🏷️ Metadata</div>
  </div>

  <!-- ===== Inputs: expanded at click 2, collapses at click 3 ===== -->
  <div class="cwl-card input" v-click="[2,3]">
    <div class="cwl-card-label">📥 Input Parameters</div>
    <pre class="cwl-card-code">inputs:
- id: reflectance
  type: File
- id: soil
  type: File</pre>
  </div>
  <div class="cwl-card input collapsed" v-click="3">
    <div class="cwl-card-label">📥 Input Parameters</div>
  </div>

  <!-- ===== Outputs: expanded at click 3, collapses at click 4 ===== -->
  <div class="cwl-card output" v-click="[3,4]">
    <div class="cwl-card-label">📤 Output Parameters</div>
    <pre class="cwl-card-code">outputs:
- id: zone_map_png
  type: File
  outputSource: plot_zone_map/zone_map</pre>
  </div>
  <div class="cwl-card output collapsed" v-click="4">
    <div class="cwl-card-label">📤 Output Parameters</div>
  </div>

  <!-- ===== Steps: expanded at click 4, stays (last card) ===== -->
  <div class="cwl-card steps" v-click="4">
    <div class="cwl-card-label">🔗 Workflow Steps</div>
    <pre class="cwl-card-code">steps:
- id: compute_ndvi
  in:
  - id: reflectance
    source: reflectance
  run: ../compute_ndvi/compute_ndvi.cwl
  out:
  - ndvi
- id: compute_fertility
  in:
  - id: soil
    source: soil
  run: ../compute_fertility/compute_fertility.cwl
  out:
  - fertility
- id: plot_zone_map
  in:
  - id: ndvi
    source: compute_ndvi/ndvi
  - id: fertility
    source: compute_fertility/fertility
  run: ../plot_zone_map/plot_zone_map.cwl
  out:
  - zone_map</pre>
  </div>

</div>

</div>

<!--
notes:
- Frame the shift: "Now that we've seen a single CommandLineTool, let's zoom
  back out to the full picture — the Workflow file. This is what ties
  multiple tools together, including Anna's Python step and Ben's R step."

- [Click 1] Metadata card expands on the right, "Components" legend starts.
  → Say: "Just like before, we start with simple metadata — but this time
  class is 'Workflow' instead of 'CommandLineTool'."
  Note: this card will collapse down to a thin header once you click again —
  that's intentional, it's an accordion effect to save space as more sections
  are revealed.

- [Click 2] Metadata collapses, Inputs card expands.
  → Say: "The workflow declares its overall inputs — here, reflectance and
  soil. These are the two raw datasets Anna and Ben started with, now
  available to any step inside this workflow."

- [Click 3] Inputs collapses, Outputs card expands.
  → Say: "The output is the final deliverable — zone_map_png. Notice the
  outputSource syntax: it explicitly says this file comes from the
  'zone_map' output of the 'plot_zone_map' step. Every output is traceable
  back to exactly which step produced it."

- [Click 4] Outputs collapses, Steps card expands (this one stays expanded
  since it's the last and most important section).
  → Walk through the steps block slowly, pointing at each step:
    - "compute_ndvi takes the reflectance input and runs Anna's tool"
    - "compute_fertility takes the soil input and runs Ben's tool — notice
      these two steps don't depend on each other, so they could even run
      in parallel"
    - "plot_zone_map then takes the outputs of BOTH previous steps — ndvi
      and fertility — as its own inputs, and produces the final zone map"
  → Say: "This is the moment Anna and Ben have been waiting for: their two
  completely separate scripts, one Python, one R, are now connected in a
  single, explicit, reproducible pipeline — and neither of them had to touch
  the other's code."

- [Click 5] The red callout box appears at the bottom.
  → Shift tone here — this is the honest "but" moment.
  → Say: "This all sounds great... but there's a catch. Anna and Ben are
  domain scientists, not workflow engineers. They don't have time to learn
  a new YAML-based syntax, and they definitely don't want to hand-write all
  this boilerplate for every project."
  → Pause briefly — let this land as a real, relatable problem.

- Bridge to next slide: "So the question becomes: how do we get the benefits
  of CWL — reproducibility, portability, clarity — without forcing every
  researcher to become a CWL expert? That's exactly the gap we'll address
  next."

Timing: ~3 min. The accordion animation naturally paces itself — resist the
urge to talk during the collapse transitions, just let the visual settle
before you start the next point. Save extra energy for the callout at the
end since it's the emotional pivot point of the whole slide.
-->


--- layout: fairagro 
layout: fairagro
--- 

<div class="fa-bar"></div> <style> .encounter-wrap{ display:flex; align-items:center; justify-content:center; gap:28px; margin: 0.2rem 0 0.5rem; } .researcher-card{ display:flex; flex-direction:column; align-items:center; gap:7px; position:relative; } .researcher-card img{ height:145px; width:145px; object-fit:contain; padding:8px; border-radius:50%; border:4px solid #ffffff; background:#ffffff; box-shadow:0 6px 18px rgba(15,152,132,0.18); box-sizing:border-box; } .researcher-card .name{ font-size:0.95rem; font-weight:700; color:#0b6f60; letter-spacing:.02em; } .researcher-card .role{ font-size:0.72rem; font-weight:600; color:#0f9884; background:#e9f7f4; border:1px solid #a9ded3; padding:2px 10px; border-radius:20px; } .encounter-connector{ display:flex; align-items:center; justify-content:center; width:48px; height:48px; border-radius:50%; background:linear-gradient(135deg,#0f9884,#0b6f60); color:#ffffff; font-size:1.35rem; font-weight:700; box-shadow:0 4px 12px rgba(15,152,132,0.3); flex-shrink:0; } /* The realization cards */ .realization-row{ display:flex; align-items:stretch; justify-content:center; gap:22px; margin:0.35rem auto 0; max-width:900px; } .realization{ flex:1; min-height:145px; border-radius:18px; padding:16px 20px; box-sizing:border-box; text-align:center; display:flex; flex-direction:column; align-items:center; justify-content:center; } .realization.happy{ background:#e9f7f4; border:2px solid #a9ded3; box-shadow:0 5px 16px rgba(15,152,132,0.12); } .realization.sad{ background:#f7f7f7; border:2px solid #d8dadd; box-shadow:0 5px 16px rgba(80,80,80,0.08); } .realization .emoji{ font-size:2.5rem; line-height:1; margin-bottom:8px; } .realization .headline{ font-size:1.05rem; font-weight:750; margin-bottom:5px; } .realization.happy .headline{ color:#0b6f60; } .realization.sad .headline{ color:#555b62; } .realization .detail{ font-size:0.78rem; line-height:1.35; color:#666; max-width:350px; } .arrow{ display:flex; align-items:center; justify-content:center; color:#9da2a7; font-size:1.8rem; font-weight:700; } .workflow-box{ margin:0.65rem auto 0; max-width:900px; text-align:center; } .workflow-box .txt{ font-size:1.05rem; line-height:1.45; color:#0f9884; font-weight:500; margin:0; } .workflow-box .txt b{ color:#0b6f60; font-weight:750; } .workflow{ display:inline-flex; align-items:center; gap:7px; margin-top:8px; padding:7px 14px; border-radius:10px; background:#f4f5f6; border:1px solid #dfe2e5; font-family:monospace; font-size:0.7rem; color:#5d6268; } .workflow span{ color:#0b6f60; font-weight:700; } .teaser-line{ text-align:center; font-size:0.82rem; color:#7a7e84; font-style:italic; margin-top:0.55rem; } .image-credit{ position:absolute; bottom:16px; left:0; right:0; text-align:center; font-size:0.5rem; line-height:1.3; color:#b0b5ba; white-space:nowrap; } .image-credit a{ color:#b0b5ba; text-decoration:underline; } </style> <!-- The two researchers --> <div class="encounter-wrap"> <div class="researcher-card"> <img src="/researcher1.png" alt="Anna" /> <span class="name">Anna</span> <span class="role">🛰️ Remote Sensing</span> </div> <div class="encounter-connector">🤝</div> <div class="researcher-card"> <img src="/researcher2.png" alt="Ben" /> <span class="name">Ben</span> <span class="role">🌱 Soil Science</span> </div> </div> <!-- The emotional journey --> <div class="realization-row"> <div class="realization happy" v-click="1"> <div class="emoji">🤩</div> <div class="headline">"CWL can solve our problems!"</div> <div class="detail">We can connect our scripts in a CWL workflow.</div> </div> <div class="arrow"></div> <div class="realization sad" v-click="2"> <div class="emoji">😩</div> <div class="headline">“Wait… we have to write it?”</div> <div class="detail"> Now they need to learn CWL, understand its syntax, and manually describe every tool and connection. </div> </div> </div> <div class="image-credit"> Icons by Amethyst Studio, <a href="https://thenounproject.com/creator/AmethystStudio/" target="_blank">The Noun Project</a> — <a href="https://creativecommons.org/licenses/by/3.0/deed.de" target="_blank">CC BY 3.0</a> </div>

<!--
notes:
- Bring back Anna and Ben right after the CWL Workflows slide's "but"
  moment: "Let's put this back in Anna and Ben's shoes for a second."

- [Click 1] The happy realization appears.
  → Say: "They hear about CWL and think: great, this solves our exact
  problem — a standard way to connect our tools, our languages, our
  datasets, all in one reproducible pipeline."

- [Click 2] The sad realization appears.
  → Shift tone, a bit deflated: "Then reality sets in — wait, we have to
  write it? Now they'd need to learn CWL's syntax themselves, and
  hand-write a description of every tool and every connection we just
  looked at."

- Bridge: "So how do we get Anna and Ben all the benefits of CWL, without
  making them become CWL experts first? That's exactly what we'll look at
  next."

Timing: ~45 sec. This is a quick emotional beat, not new content — let the
two reactions land, then move straight into SciWIn.
-->
