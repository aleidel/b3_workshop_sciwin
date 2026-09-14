---
layout: fairagro
title: Field analysis workflow - NDVI
routeAlias: session1
---

<div class="fa-bar"></div>

<style>
.ndvi-row{
  display:grid;
  grid-template-columns: 1.1fr 1fr;
  gap: 1.5rem;
  align-items:center;
  margin-top: 1rem;
}

.box {
  border-radius: 14px;
  padding: 1.1rem 1.3rem;
  background: linear-gradient(160deg, #ffffff 0%, #f2fbf9 100%);
  border: 1.5px solid #cdeee6;
  box-shadow: 0 4px 12px rgba(15, 152, 132, 0.10);
}
.box-header {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  margin-bottom: 0.8rem;
  flex-wrap: nowrap;
}
.box-avatar{
  flex-shrink:0;
  width:34px;
  height:34px;
  border-radius:50%;
  object-fit:cover;
  border:2px solid #ffffff;
  background:#ffffff;
  box-shadow:0 2px 6px rgba(15,152,132,0.25);
}
.box h3 {
  margin: 0;
  font-family: "Fira Code", monospace;
  font-size: 1.15rem;
  font-weight: 700;
  color: #0b6f60;
  flex: 1;
  min-width: 0;
}
.lang {
  display: inline-block;
  font-size: 0.72rem;
  padding: 0.16rem 0.6rem;
  border-radius: 20px;
  font-weight: 700;
  letter-spacing: 0.02em;
  text-transform: uppercase;
  flex-shrink: 0;
}

.box ul{
  margin:0;
  padding-left: 1.1rem;
}
.box li{
  margin-bottom:0.5rem;
  font-size:0.98rem;
  line-height:1.5;
  color:#333;
}
.box li:last-child{ margin-bottom:0; }
.box li b{ color:#0b6f60; }

.ndvi-formula{
  margin-top:0.8rem;
  padding:0.6rem 0.9rem;
  border-radius:10px;
  background:rgba(15,152,132,0.06);
  border:1px solid #cdeee6;
  text-align:center;
  font-size:1.1rem;
  color:#0b6f60;
}

.ndvi-img-side img{
  width:100%;
  height:auto;
  max-height: 380px;
  object-fit:contain;
  display:block;
  margin: 0 auto;
}

.attribution {
  position: absolute;
  bottom: 1rem;
  right: 1.2rem;
  text-align: right;
  font-size: 0.62rem;
  color: #aaa;
  line-height: 1.3;
  z-index: 10;
}
.attribution a {
  color: #aaa;
  text-decoration: underline;
}
</style>

<div class="ndvi-row">

  <div class="box">
    <div class="box-header">
      <img src="/researcher1.png" alt="Anna" class="box-avatar" />
      <h3>NDVI — Normalized Difference Vegetation Index</h3>
    </div>
    <ul>
      <li>Drone imagery captures <b>red</b> and <b>near-infrared (NIR)</b> reflectance for each grid cell</li>
      <li>Healthy, dense vegetation reflects <b>more NIR</b> and <b>less red light</b></li>
      <li>NDVI is calculated from these two bands and ranges from <b>-1 to 1</b></li>
      <li>Values close to <b>1</b> = healthy, vigorous plants; values near <b>0 or negative</b> = bare soil or stressed vegetation</li>
    </ul>

<div>

$$
NDVI = \frac{NIR - Red}{NIR + Red}
$$

</div>

  </div>

  <div class="ndvi-img-side">
    <img src="/ndvi.png" alt="NDVI example" loading="lazy" />
  </div>

</div>

<div class="attribution">
  <a href="https://www.flaticon.com/free-icons/autonomy" title="autonomy icons">Autonomy icons created by Magnific - Flaticon</a> ·
  <a href="https://www.flaticon.com/free-icons/plant" title="plant icons">Plant icons created by dDara - Flaticon</a>
</div>
<!--
notes:
- Bridge from the SciWIn "questions" checkpoint: "Alright, let's get concrete.
  We're going to spend the rest of this session actually building the
  workflow for Anna and Ben's field. Let's start with Anna's data."

- Walk through Anna's side (left box) top to bottom:
  - "Anna's drone captures two specific wavelength bands for every grid cell
    in the field: red light and near-infrared light."
  - "The key insight is biological: healthy, dense vegetation reflects a lot
    of near-infrared light but absorbs red light. Stressed or sparse
    vegetation does the opposite."
  - "NDVI is just a normalized ratio of these two bands, which is why it
    always falls between -1 and 1."
  - "Values near 1 mean healthy crops, values near 0 or negative mean bare
    soil, water, or badly stressed plants."

- Point to the formula box: "The math itself is simple — NIR minus red,
  divided by NIR plus red. You don't need to memorize this, just know it's
  a simple per-pixel calculation Anna's script will need to perform."

- Point to the image on the right: "Here's a visual — you can see how NDVI
  translates raw reflectance into an interpretable map of plant health
  across the field."

- Bridge to next slide: "That's Anna's half of the story. Now let's look at
  what Ben brings to the table with his soil samples."

Timing: ~1.5 min. This is scene-setting/context — don't over-explain the
remote sensing science, just enough for the audience to understand what
compute_ndvi.py will need to do later.
-->

---
layout: fairagro
title: Field analysis workflow - Soil measurements
---

<div class="fa-bar"></div>

<style>
.soil-row{
  display:grid;
  grid-template-columns: 1.1fr 1fr;
  gap: 1.5rem;
  align-items:center;
  margin-top: 1rem;
}

.box {
  border-radius: 14px;
  padding: 1.1rem 1.3rem;
  background: linear-gradient(160deg, #ffffff 0%, #f2fbf9 100%);
  border: 1.5px solid #cdeee6;
  box-shadow: 0 4px 12px rgba(15, 152, 132, 0.10);
}
.box-header {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  margin-bottom: 0.8rem;
  flex-wrap: nowrap;
}
.box-avatar{
  flex-shrink:0;
  width:34px;
  height:34px;
  border-radius:50%;
  object-fit:cover;
  border:2px solid #ffffff;
  background:#ffffff;
  box-shadow:0 2px 6px rgba(15,152,132,0.25);
}
.box h3 {
  margin: 0;
  font-family: "Fira Code", monospace;
  font-size: 1.15rem;
  font-weight: 700;
  color: #0b6f60;
  flex: 1;
  min-width: 0;
}
.lang {
  display: inline-block;
  font-size: 0.72rem;
  padding: 0.16rem 0.6rem;
  border-radius: 20px;
  font-weight: 700;
  letter-spacing: 0.02em;
  text-transform: uppercase;
  flex-shrink: 0;
}
.lang-py { background: #A8C83C; color: #1a1a1a; }

.box ul{
  margin:0;
  padding-left: 1.1rem;
}
.box li{
  margin-bottom:0.5rem;
  font-size:0.98rem;
  line-height:1.5;
  color:#333;
}
.box li:last-child{ margin-bottom:0; }
.box li b{ color:#0b6f60; }

.soil-formula{
  margin-top:0.8rem;
  padding:0.6rem 0.9rem;
  border-radius:10px;
  background:rgba(15,152,132,0.06);
  border:1px solid #cdeee6;
  text-align:center;
  font-size:0.95rem;
  color:#0b6f60;
  font-weight:600;
}

.soil-img-side img{
  width:100%;
  height:auto;
  max-height: 380px;
  object-fit:contain;
  display:block;
  margin: 0 auto;
}

.attribution {
  margin-top: 0.4rem;
  text-align: center;
  font-size: 0.62rem;
  color: #aaa;
  line-height: 1.3;
}
.attribution a {
  color: #aaa;
  text-decoration: underline;
}
</style>

<div class="soil-row">

  <div class="box">
    <div class="box-header">
      <img src="/researcher2.png" alt="Ben" class="box-avatar" />
      <h3>Soil measurements</h3>
    </div>
    <ul>
      <li>Soil samples are taken directly from the field, at each grid cell</li>
      <li><b>Nitrate</b> (measured in <code>ppm</code>) indicates how much plant-available nitrogen is present in the soil — essential for plant growth</li>
      <li><b>Organic matter</b> (measured in <code>%</code>) reflects decomposed plant and animal material, linked to water retention and long-term fertility</li>
      <li>Together, these two values are combined into a single <b>soil fertility score</b> per grid cell</li>
    </ul>

  </div>

<div class="soil-img-side">
  <img src="/soil_measurement.png" alt="Soil measurement example" loading="lazy" />
  <div class="attribution">
    Image generated by Gemini
  </div>
</div>

</div>

<!--
notes:
- Continue directly from the previous slide: "While Anna was flying her
  drone, Ben was out in the same field on the ground, taking physical soil
  samples at the same grid locations."

- Walk through Ben's bullets:
  - "For each grid cell, he measures two things: nitrate content in parts
    per million, which tells us how much plant-available nitrogen is in the
    soil — critical for crop growth."
  - "And organic matter percentage, which relates to how well the soil
    retains water and how fertile it will be long-term."
  - "Ben combines these two measurements into a single fertility score per
    grid cell — this is the number his R script produces."

- Point to the image: "Here's what that looks like in practice — someone
  literally out in the field with a soil probe, at each of the grid
  locations."

- Key point to emphasize: "Notice — Anna and Ben are measuring completely
  different things, with completely different instruments, using
  completely different software. But they're looking at the exact same
  physical grid on the same field."

- Bridge to next slide: "So now the question is: how do we combine an NDVI
  score and a fertility score, calculated by two different people in two
  different languages, into one map? Let's look at the full workflow we're
  going to build today."

Timing: ~1.5 min. Keep pace similar to the NDVI slide — this is a parallel
structure, so the audience should already sense where this is going.
-->

---
layout: fairagro
title: "Session 1: The building blocks"
---

<div class="fa-bar"></div>

<style>
/* --- Roadmap items (used inside Box) --- */
.roadmap-item{
  display:flex;
  align-items:flex-start;
  gap:12px;
  margin-bottom:0.7rem;
}
.roadmap-item:last-child{ margin-bottom:0; }
.roadmap-num{
  flex-shrink:0;
  width:26px;
  height:26px;
  border-radius:50%;
  display:flex;
  align-items:center;
  justify-content:center;
  font-weight:700;
  font-size:0.8rem;
  color:#fff;
  background:#0f9884;
}
.roadmap-num.exercise{
  background:#A8C83C;
  color:#1a1a1a;
}
.roadmap-text{
  font-size:0.86rem;
  line-height:1.45;
  color:#333;
}
.roadmap-text b{ color:#0b6f60; }

/* --- Workflow boxes --- */
.workflow-row {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}
.box {
  border-radius: 14px;
  padding: 1.1rem 1.3rem;
  background: linear-gradient(160deg, #ffffff 0%, #f2fbf9 100%);
  border: 1.5px solid #cdeee6;
  box-shadow: 0 4px 12px rgba(15, 152, 132, 0.10);
}
.box-highlight {
  background: linear-gradient(160deg, #ffffff 0%, #f6faec 100%);
  border-color: #d7e79b;
  box-shadow: 0 4px 12px rgba(168, 200, 60, 0.20);
}
.box-header {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  margin-bottom: 0.6rem;
  flex-wrap: nowrap; /* changed from wrap */
}

.box-avatar{
  flex-shrink:0;
  width:34px;
  height:34px;
  border-radius:50%;
  object-fit:cover;
  border:2px solid #ffffff;
  background:#ffffff;
  box-shadow:0 2px 6px rgba(15,152,132,0.25);
}

.box-avatar-group{
  flex-shrink:0; /* prevent it from being squeezed */
  position:relative;
  width:48px;
  height:34px;
}
.box-avatar-group img{
  position:absolute;
  top:0;
  width:34px;
  height:34px;
  border-radius:50%;
  object-fit:cover;
  border:2px solid #ffffff;
  background:#ffffff;
  box-shadow:0 2px 6px rgba(168,200,60,0.35);
}
.box-avatar-group img:first-child{ left:0; z-index:2; }
.box-avatar-group img:last-child{ left:18px; z-index:1; }

.box h3 {
  margin: 0;
  font-family: "Fira Code", monospace;
  font-size: 1rem;
  font-weight: 700;
  color: #0b6f60;
  flex: 1;
  min-width: 0;
  white-space: nowrap;      /* new */
  overflow: hidden;         /* new */
  text-overflow: ellipsis;  /* new */
}

.box ul { margin: 0; padding-left: 1.1rem; }
.box li {
  margin-bottom: 0.4rem;
  font-size: 0.84rem;
  line-height: 1.4;
  color: #333;
}
.box li b { color: #0b6f60; }
.lang {
  display: inline-block;
  font-size: 0.66rem;
  padding: 0.16rem 0.6rem;
  border-radius: 20px;
  font-weight: 700;
  letter-spacing: 0.02em;
  text-transform: uppercase;
  flex-shrink: 0;
}
.lang-r { background: #0f9884; color: #ffffff; }
.lang-py { background: #A8C83C; color: #1a1a1a; }
</style>

<div class="workflow-row mt-4">


<div class="box">
  <div class="box-header">
    <img src="/researcher1.png" alt="Anna" class="box-avatar" />
    <h3>compute_ndvi</h3>
    <span class="lang lang-py">Python</span>
  </div>
  <ul>
    <li>Input: drone imagery — <b>red</b> + <b>near-infrared</b> bands</li>
    <li>Compares reflectance to derive a <b>plant health score (NDVI)</b></li>
  </ul>
</div>

<div class="box">
  <div class="box-header">
    <img src="/researcher2.png" alt="Ben" class="box-avatar" />
    <h3>compute_fertility</h3>
    <span class="lang lang-r">R</span>
  </div>
  <ul>
    <li>Input: soil sample with measured <b>nitrate</b> + <b>organic matter</b></li>
    <li>Combines both into a single <b>soil quality score</b> per grid cell</li>
  </ul>
</div>


<div class="box box-highlight">
  <div class="box-header">
    <div class="box-avatar-group">
      <img src="/researcher1.png" alt="Anna" />
      <img src="/researcher2.png" alt="Ben" />
    </div>
    <h3>plot_zone_map</h3>
    <span class="lang lang-py">Python</span>
  </div>
  <ul>
    <li>Uses NDVI and soil fertility score</li>
    <li>Aligns them across the <b>14×10 grid</b> and plots management zones</li>
  </ul>
</div>

</div>

<div v-click="1">

<Box label="🙌 How This Session Works: Create CWL CommandLineTools">
  <div class="roadmap-item">
    <div class="roadmap-num">1</div>
    <div class="roadmap-text"><b>Live-code together:</b> <code>compute_ndvi.py</code> → we type the <code>s4n create</code> command live, then look at the resulting CWL file line-by-line.</div>
  </div>
  <div class="roadmap-item">
    <div class="roadmap-num">2</div>
    <div class="roadmap-text"><b>Live-code together:</b> <code>compute_fertility.R</code> → same process, different language & runtime.</div>
  </div>
  <div class="roadmap-item">
    <div class="roadmap-num exercise">3</div>
    <div class="roadmap-text"><b>Your turn:</b> <code>plot_zone_map.py</code> → build the CommandLineTool yourself, with hints available if you get stuck.</div>
  </div>
</Box>

<div class="mt-2 text-center text-sm" style="color:#5c6067;">
  📎 A <b>summary slide</b> with the exact commands follows each live-coding step
</div>

</div>


<!--
notes:
- Introduce the three-box diagram first, before any clicks: "Here's the
  complete picture. Three steps: Anna's compute_ndvi in Python, Ben's
  compute_fertility in R, and a final step, plot_zone_map, that takes both
  of their outputs and produces one combined management map."

- Point out the avatar icons: "Notice the third box has both Anna and Ben's
  photos — this step literally depends on both of their work."

- Point out the language pills: "Python, R, Python again — three components,
  two different programming languages, and by the end of today they'll all
  run together as a single, reproducible workflow."

- [Click 1] The "How This Session Works" box appears with the roadmap.
  → Walk through the three roadmap items at a measured pace:
    1. "First, we'll live-code together — I'll type the s4n create command
       for compute_ndvi.py live, and we'll look at the resulting CWL file
       line by line."
    2. "Then we'll do the same thing for compute_fertility.R — same
       process, but you'll see how easily it handles a completely different
       language and runtime."
    3. "Third one is yours — you'll build the CommandLineTool for
       plot_zone_map.py yourself. Don't worry, hints will be available if
       you get stuck."

- Point to the note below the box: "After each live-coding step, there's a
  reference slide with the exact commands, so you don't need to
  frantically copy from the terminal — you can always look it up
  afterwards."

- Bridge: "Let's do a quick sanity check first — make sure everyone has
  SciWIn installed — then we'll dive into live coding."

Timing: ~2 min. This is an important orientation slide — make sure the
audience understands the "shape" of the next 30-40 minutes before diving in,
since it reduces confusion later about what's a demo vs. what's their task.
-->

---
layout: fairagro
title: Setup
---

<div class="text-sm leading-tight">

### Install SciWIn

**Linux / macOS**
```bash
curl --proto '=https' --tlsv1.2 -LsSf https://fairagro.github.io/sciwin/get_s4n.sh | sh
```

**Windows**
```powershell
powershell -ExecutionPolicy Bypass -c "irm https://fairagro.github.io/sciwin/get_s4n.ps1 | iex"
```

**Verify:** `s4n -V`

### Repository Setup

**Clone repo**
```bash
git clone https://github.com/aleidel/field_analysis.git && cd field_analysis
```

<div class="grid grid-cols-2 gap-4 mt-2">

<div>

**Virtual env (Linux/macOS)**
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

</div>
<div>

**Virtual env (Windows)**
```bash
python -m venv .venv
.venv\Scripts\activate
python -m pip install -r requirements.txt
```

</div>
</div>
</div>

---
layout: fairagro
title: CWL CommandLineTool - compute_ndvi.py
---

<script setup>
const lines2 = [
  {
    type: 'cmd',
    text: 's4n create -c Dockerfile -t demo:v1.0.0 python3 code/compute_ndvi/compute_ndvi.py --reflectance data/reflectance.csv --output ndvi.csv'
  },
  {
    type: 'info',
    icon: '▶️',
    segments: [
      { text: 'Executing command: ' },
      { text: 'python3 code/compute_ndvi/compute_ndvi.py --output ndvi.csv --reflectance data/reflectance.csv',},
    ]
  },
   {
    type: 'info',
    text: 'Computed NDVI for 140 grid cells.'
  },
   {
    type: 'info',
    text: 'NDVI range: 0.380 - 0.669'
  },
  {
    type: 'info',
    icon: '📄',
    text: 'Found outputs:'
  },
  {
    type: 'output',
    text: '- $(inputs.output)'
  },
  {
    type: 'info',
    icon: '📄',
    segments: [
      { text: 'Created CWL file ' },
      { text: 'workflows/compute_ndvi/compute_ndvi.cwl', class: 'text-green-400 font-semibold' },
    ]
  },
]
</script>

<div class="h-100">

<TerminalDemo :lines="lines2" />

</div>

<!--
notes:
- Narrate live as the terminal demo plays (or as you type/run it yourself).

- Before running: "Here's Anna's actual command — running her NDVI script
  with a reflectance file as input and ndvi.csv as output. We wrap the
  whole thing in one s4n create call, telling it to build a Docker image
  from our Dockerfile and tag it demo:latest."

- As the output appears: "s4n actually runs the command for us as part of
  creating the tool — that's how it knows what the script really does,
  rather than us having to describe it by hand."

- Point out the computed results: "You can see it genuinely computed NDVI
  for all 140 grid cells, with a sensible range — this isn't a mock, the
  script really ran inside the container."

- Point out 'Found outputs': "s4n found the output file matching what we
  told it to expect, and used that to write the outputs section of the CWL
  file automatically."

- Point out the final line: "And there it is — workflows/compute_ndvi/compute_ndvi.cwl,
  a complete CWL CommandLineTool, generated from a single command. No YAML
  was hand-written."

- Bridge: "Let's open that file and see exactly what got generated, field
  by field."

Timing: ~1.5-2 min. If this is a pre-recorded/scripted terminal demo rather
than something you type live, slow down your narration to match the pace
of the animation rather than rushing ahead of it.
-->

---
layout: fairagro
title: From Command to CWL CommandLineTool
clicks: 5
---

<div class="fa-logo-title"></div>
<div class="fa-bar"></div>

<style>
.slidev-layout{ height:100%; display:flex; flex-direction:column; }
.map-page{ flex:1; min-height:0; display:flex; flex-direction:column; }

.map-wrap{
  flex:1; min-height:0;
  display:flex; gap:22px; align-items:stretch;
  font-family:'Fira Sans',sans-serif;
}
.map-left{ flex:0 0 340px; display:flex; flex-direction:column; min-height:0; overflow-y:auto; }
.map-right{ flex:1; min-width:0; min-height:0; display:flex; }

.map-command-card{
  border-radius:10px; padding:7px 9px 8px;
  background:linear-gradient(180deg,#fbfbfd 0%,#f4f5f9 100%);
  border:1px solid #e6e7ee;
  box-shadow:0 2px 8px rgba(20,20,40,0.05);
  margin-bottom:0.55rem; flex-shrink:0;
}
.map-command-code{
  font-family:'Fira Code','Courier New',monospace; font-size:0.62rem;
  line-height:1.55; margin-top:2px;
  display:flex; flex-wrap:wrap; align-items:center; gap:3px 5px;
}
.map-command-code .prompt{ color:#0f9884; font-weight:700; }
.tok{
  padding:1px 4px; border-radius:4px; transition:all .2s ease; color:#4b4f5e;
  white-space:nowrap;
}
.tok.s4n{ color:#a4a7b8; }
.tok.active-command{ background:#f2eefb; color:#5c3fc7; font-weight:700; }
.tok.active-input{ background:#e7f0ff; color:#2f6fed; font-weight:700; }
.tok.active-env{ background:#f2f9f2; color:#3d6b40; font-weight:700; }

.map-legend-title{
  font-weight:700; font-size:0.6rem; color:#0f9884;
  text-transform:uppercase; letter-spacing:.03em; margin-bottom:0.4rem;
}

.map-legend-item{
  display:flex; align-items:flex-start; gap:6px;
  margin-bottom:0.32rem; padding:5px 7px;
  border-radius:8px; border:1.2px solid #e6e7ee; background:#fafafc;
  opacity:0.45; transition:opacity .2s ease, background .2s ease, border-color .2s ease;
  flex-shrink:0;
}
.map-legend-item.active{ opacity:1; }

.map-legend-item .dot{
  flex-shrink:0; width:7px; height:7px; border-radius:50%; margin-top:3px;
}
.map-legend-item .txt{ font-size:0.7rem; line-height:1.28; color:#333; }
.map-legend-item .txt b{ font-weight:700; }
.map-legend-item code{ background:#f0f0f0; padding:0.02rem 0.3rem; border-radius:3px; font-size:0.85em; }

.dot.command{ background:#7b5fd1; }
.dot.input{ background:#2f6fed; }
.dot.output{ background:#e0524f; }
.dot.runtime{ background:#43a047; }

.map-legend-item.command.active{ background:#f2eefb; border-color:#d9ccfb; }
.map-legend-item.command.active .txt b{ color:#5c3fc7; }

.map-legend-item.input.active{ background:#e7f0ff; border-color:#bcd3ff; }
.map-legend-item.input.active .txt b{ color:#2f6fed; }

.map-legend-item.output.active{ background:#fde7e6; border-color:#f5c2c0; }
.map-legend-item.output.active .txt b{ color:#e0524f; }

.map-missing-note{
  margin-top:0.25rem; margin-bottom:0.35rem; border:1.5px solid #cfe6cf; border-radius:8px;
  padding:6px 8px; opacity:0.45; transition:opacity .2s ease, background .2s ease;
  flex-shrink:0;
}
.map-missing-note.active{ opacity:1; background:#f2f9f2; }
.map-missing-note .txt{ font-size:0.7rem; line-height:1.28; color:#3d6b40; font-style:italic; }
.map-missing-note .txt b{ font-weight:700; font-style:normal; }

.cwl-file-box{
  background:#fafbfc; border:1px solid #e5e7eb; border-radius:8px; padding:8px 11px;
  font-family:'Fira Code','Courier New',monospace; font-size:0.52rem;
  line-height:1.22; color:#374151;
  width:100%; box-sizing:border-box; overflow-y:auto;
}
.cwl-file-box .line{ padding:0 3px; border-radius:3px; transition:background .2s ease, color .2s ease; white-space:pre; }
.cwl-file-box .line.sp{ height:4px; line-height:0; padding:0; font-size:0; }
.cwl-file-box .comment{ color:#9ca3af; }
.cwl-file-box .key{ color:#111827; font-weight:600; }
.cwl-file-box .hl-command{ background:#f2eefb; color:#5c3fc7; }
.cwl-file-box .hl-input{ background:#e7f0ff; color:#1d4ed8; }
.cwl-file-box .hl-output{ background:#fde7e6; color:#c0392b; }
.cwl-file-box .hl-runtime{ background:#f2f9f2; color:#3d6b40; }
</style>

<div class="map-page">
<div class="map-wrap">

<div class="map-left">

<div class="map-command-card">
  <div class="map-command-title">💻 Terminal command</div>
  <div class="map-command-code">
    <span class="prompt">$</span>
    <span class="tok s4n">s4n create </span>
    <span class="tok" :class="{ 'active-env': $clicks >= 1 }">-c Dockerfile -t demo:v1.0.0</span>
    <span class="tok" :class="{ 'active-command': $clicks >= 2 }">python3 code/compute_ndvi/compute_ndvi.py </span>
    <span class="tok" :class="{ 'active-input': $clicks >= 3 }">--reflectance data/reflectance.csv</span>
    <span class="tok" :class="{ 'active-input': $clicks >= 3 }">--output ndvi.csv</span>
  </div>
</div>

<div class="map-legend-title">Components</div>

<div class="map-missing-note" :class="{ active: $clicks >= 1 }">
  <div class="txt"><span class="dot runtime" style="display:inline-block;margin-right:5px;"></span>🧩 <b>Runtime environment</b> — build image from local <code>Dockerfile</code>, tagged <code>demo:v1.0.0</code>.</div>
</div>

<div class="map-legend-item command" :class="{ active: $clicks >= 2 }">
  <div class="dot command"></div>
  <div class="txt">⚡ <b>Command</b> → <code>baseCommand</code>. Script embedded via <code>InitialWorkDirRequirement</code>.</div>
</div>

<div class="map-legend-item input" :class="{ active: $clicks >= 3 }">
  <div class="dot input"></div>
  <div class="txt">📥 <b>Input</b> → <code>--reflectance data/reflectance.csv</code></div>
</div>

<div class="map-legend-item input" :class="{ active: $clicks >= 3 }">
  <div class="dot input"></div>
  <div class="txt">📥 <b>Input</b> → define name of output file <code>--output ndvi.csv</code></div>
</div>

<div class="map-legend-item output" :class="{ active: $clicks >= 4 }">
  <div class="dot output"></div>
  <div class="txt">📤 <b>Output</b> → <code>ndvi_csv</code> autodetected by s4n through git; because output file name was defined as input, it is linked to inputs.</div>
</div>

</div>
<div class="map-right">
<div class="cwl-file-box">
<div class="line comment">#!/usr/bin/env cwl-runner</div>
<div class="line sp"></div>
<div class="line"><span class="key">class</span>: CommandLineTool</div>
<div class="line"><span class="key">cwlVersion</span>: v1.2</div>
<div class="line sp"></div>
<div class="line"><span class="key">requirements</span>:</div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }">- <span class="key">class</span>: InitialWorkDirRequirement</div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }">&nbsp;&nbsp;listing:</div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }">&nbsp;&nbsp;- entry:</div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$include: ../../code/compute_ndvi/compute_ndvi.py</div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }">&nbsp;&nbsp;&nbsp;&nbsp;entryname: code/compute_ndvi/compute_ndvi.py</div>
<div class="line" :class="{ 'hl-runtime': $clicks >= 1 }">- <span class="key">class</span>: DockerRequirement</div>
<div class="line" :class="{ 'hl-runtime': $clicks >= 1 }">&nbsp;&nbsp;dockerFile:</div>
<div class="line" :class="{ 'hl-runtime': $clicks >= 1 }">&nbsp;&nbsp;&nbsp;&nbsp;$include: ../../Dockerfile</div>
<div class="line" :class="{ 'hl-runtime': $clicks >= 1 }">&nbsp;&nbsp;dockerImageId: demo:v1.0.0</div>
<div class="line" :class="{ 'hl-output': $clicks >= 4 }">- <span class="key">class</span>: InlineJavascriptRequirement</div>
<div class="line sp"></div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }"><span class="key">inputs</span>:</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">- default:</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;&nbsp;&nbsp;class: File</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;&nbsp;&nbsp;location: ../../data/reflectance.csv</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;format: edam:format_3752</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;id: reflectance</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;inputBinding:</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;&nbsp;&nbsp;prefix: --reflectance</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;type: File</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">- default: ndvi.csv</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;id: output</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;inputBinding:</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;&nbsp;&nbsp;prefix: --output</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;type: string</div>
<div class="line sp"></div>
<div class="line" :class="{ 'hl-output': $clicks >= 4 }"><span class="key">outputs</span>:</div>
<div class="line" :class="{ 'hl-output': $clicks >= 4 }">- format: edam:format_3752</div>
<div class="line" :class="{ 'hl-output': $clicks >= 4 }">&nbsp;&nbsp;id: ndvi_csv</div>
<div class="line" :class="{ 'hl-output': $clicks >= 4 }">&nbsp;&nbsp;outputBinding:</div>
<div class="line" :class="{ 'hl-output': $clicks >= 4 }">&nbsp;&nbsp;&nbsp;&nbsp;glob: $(inputs.output)</div>
<div class="line" :class="{ 'hl-output': $clicks >= 4 }">&nbsp;&nbsp;type: File</div>
<div class="line sp"></div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }"><span class="key">baseCommand</span>:</div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }">- python3</div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }">- code/compute_ndvi/compute_ndvi.py</div>
</div>
</div>

</div>
</div>
<!--
notes:
- This slide maps the terminal command (left) to the generated CWL file
  (right) click by click. Use the terminal command as your narration anchor
  — point at each highlighted token as you explain it.

- [Click 1] The "-c Dockerfile -t demo:v1.0.0" part of the command
  highlights, and the runtime note appears on the left; the DockerRequirement
  block highlights on the right.
  → Say: "This part of the command told s4n to build the runtime environment
  from our local Dockerfile and tag the resulting image demo:v1.0.0. Look at
  the CWL file — that's translated directly into a DockerRequirement block,
  referencing the Dockerfile inline."

- [Click 2] The script call itself highlights ("python3
  code/compute_ndvi/compute_ndvi.py"); the command legend item and
  InitialWorkDirRequirement + baseCommand blocks highlight on the right.
  → Say: "This is the actual command to run. Notice s4n did something
  clever — it embedded the entire script content directly into the CWL file
  via InitialWorkDirRequirement, so the CWL file is fully self-contained.
  And baseCommand at the bottom just says: run python3 on this script."

- [Click 3] The two --reflectance / --output arguments highlight; the two
  input legend items and the inputs: block highlight on the right.
  → Say: "Here's where the two command-line arguments become formal inputs.
  Look at 'reflectance' — s4n automatically figured out it's a File type,
  set a default location pointing at our data file, and recorded that it
  gets passed via the --reflectance flag. Same thing for 'output', except
  that's just a string — the output filename."

- [Click 4] Output legend item highlights; outputs: block highlights on the
  right (plus InlineJavascriptRequirement).
  → Say: "And finally the output — s4n autodetected that this script
  produces a file, named it ndvi_csv, and used a glob pattern that's
  dynamically linked back to whatever we passed as the --output input. So
  if we ever rename the output file, this still works correctly."

- Wrap-up: "So in one command, s4n did everything we saw in the manual CWL
  example earlier — metadata, runtime, inputs, outputs, command — without
  Anna needing to write a single line of YAML."

- Bridge to next slide: "Here's a reference slide with the exact commands
  we just ran, in case you want to copy them later."

Timing: ~2.5-3 min. Go click by click, don't rush — this is the core "aha"
moment of the whole session, showing the direct 1:1 mapping between a
familiar terminal command and the CWL output.
-->
---
layout: fairagro
title: "Summary: compute_ndvi"
---

<script setup>
import { ref } from 'vue'

const copiedIndex = ref(null)

function copyCommand(text, index) {
  navigator.clipboard.writeText(text).then(() => {
    copiedIndex.value = index
    setTimeout(() => {
      copiedIndex.value = null
    }, 1500)
  })
}

const cmd1 = 'python3 code/compute_ndvi/compute_ndvi.py --reflectance data/reflectance.csv --output ndvi.csv'
const cmd2 = 's4n create -c Dockerfile -t demo:v1.0.0 python3 code/compute_ndvi/compute_ndvi.py --reflectance data/reflectance.csv --output ndvi.csv'
</script>

<div class="fa-bar"></div>

<style>
.ref-page{ font-family:'Fira Sans',sans-serif; }
.ref-section{
  border-radius:12px; padding:12px 16px;
  background:linear-gradient(180deg,#fbfbfd 0%,#f4f5f9 100%);
  border:1px solid #e6e7ee;
  margin-bottom:0.8rem;
}
.ref-section.highlight{
  background:linear-gradient(180deg,#f2fbf9 0%,#e6f7f3 100%);
  border-color:#cdeee6;
}
.ref-label{
  font-size:0.78rem; font-weight:700; color:#0f9884;
  text-transform:uppercase; letter-spacing:.03em; margin-bottom:6px;
}

.ref-cmd-wrap{
  position:relative;
  display:flex;
  align-items:flex-start;
  gap:8px;
}
.ref-cmd{
  flex:1; min-width:0;
  font-family:'Fira Code','Courier New',monospace; font-size:0.78rem;
  color:#374151; background:#ffffff; border:1px solid #e5e7eb;
  border-radius:6px; padding:8px 10px; line-height:1.5; word-break:break-word;
}
.ref-cmd .prompt{ color:#0f9884; font-weight:700; margin-right:6px; }
.ref-section.docker .ref-cmd .prompt{ color:#5c3fc7; }

.copy-btn{
  flex-shrink:0;
  display:flex; align-items:center; gap:4px;
  font-family:'Fira Sans',sans-serif;
  font-size:0.68rem; font-weight:700;
  color:#0f9884;
  background:#ffffff;
  border:1px solid #cdeee6;
  border-radius:6px;
  padding:8px 10px;
  cursor:pointer;
  transition:all 0.15s ease;
  white-space:nowrap;
}
.copy-btn:hover{
  background:#f2fbf9;
  border-color:#0f9884;
}
.copy-btn.copied{
  background:#0f9884;
  border-color:#0f9884;
  color:#ffffff;
}

.ref-note{
  margin-top:6px; font-size:0.78rem; color:#4b5563; line-height:1.4;
}
.ref-note code{ background:#f0f0f0; padding:0.02rem 0.3rem; border-radius:3px; }
</style>

<div class="ref-page">

<div class="ref-section">
  <div class="ref-label">▶️ Plain script call</div>
  <div class="ref-cmd-wrap">
    <div class="ref-cmd"><span class="prompt">$</span>python3 code/compute_ndvi/compute_ndvi.py --reflectance data/reflectance.csv --output ndvi.csv</div>
    <button class="copy-btn" :class="{ copied: copiedIndex === 1 }" @click="copyCommand(cmd1, 1)">
      {{ copiedIndex === 1 ? '✓ Copied' : '📋 Copy' }}
    </button>
  </div>
  <div class="ref-note">Computed NDVI for 140 grid cells → NDVI range: 0.380 – 0.669</div>
</div>

<div class="ref-section highlight">
  <div class="ref-label">⚙️ Turn it into a CWL CommandLineTool</div>
  <div class="ref-cmd-wrap">
    <div class="ref-cmd"><span class="prompt">$</span>s4n create -c Dockerfile -t demo:v1.0.0 python3 code/compute_ndvi/compute_ndvi.py --reflectance data/reflectance.csv --output ndvi.csv</div>
    <button class="copy-btn" :class="{ copied: copiedIndex === 2 }" @click="copyCommand(cmd2, 2)">
      {{ copiedIndex === 2 ? '✓ Copied' : '📋 Copy' }}
    </button>
  </div>
  <div class="ref-note">Creates <code>workflows/compute_ndvi/compute_ndvi.cwl</code></div>
</div>

</div>

<!--
notes:
- This is a reference/lookup slide — keep narration brief since it's mostly
  for participants to copy commands at their own pace.

- Briefly summarize what's on screen: "This slide is just for reference —
  it has copy buttons for the three commands we just ran: the plain script
  call, the docker build command, and the s4n create command."

- Point out the note under the first command: "Just to confirm the science
  checks out — NDVI values ranged from about 0.38 to 0.67 across our 140
  grid cells, which is a healthy-looking field."

- Point out the note under the s4n command: "This created the file at
  workflows/compute_ndvi/compute_ndvi.cwl — that's the actual CWL tool file
  now sitting in our project, ready to be used in a larger workflow."

- Practical note: "Feel free to pause here for a few seconds if you want to
  copy any of these into your own notes — we'll wait."

Timing: ~1 min, or longer if participants are actively copying commands and
running them themselves on their own machines. Use your judgment based on
whether this is a "watch me" demo or a "follow along" exercise.
-->

---
layout: fairagro
routeAlias: session1-checkpoint
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
.check-row{
  display:flex;
  gap:1rem;
  flex-wrap:wrap;
  justify-content:center;
  margin-top:0.4rem;
}
.check-card{
  display:flex;
  align-items:center;
  gap:0.6rem;
  padding:0.6rem 1.1rem;
  border-radius:12px;
  background:linear-gradient(160deg,#ffffff 0%,#f2fbf9 100%);
  border:1.5px solid #cdeee6;
  box-shadow:0 3px 10px rgba(15,152,132,0.10);
  font-size:0.9rem;
  color:#333;
}
.check-card b{ color:#0b6f60; }
.check-card .emoji{ font-size:1.2rem; }
</style>

<div class="check-wrap">
  <div class="check-icon">🙋</div>
  <h1 class="check-title">Any questions so far?</h1>
</div>

<!--
notes:
- Simple checkpoint slide — pause and open the floor.

- Say something like: "We just covered a lot in a short time — Anna's NDVI
  script, Docker, and our first CWL CommandLineTool. Before we move to Ben's
  side of things, let's pause. Any questions, anything unclear, or did
  anyone run into an error trying this on their own machine?"

- Use the three cards as a loose prompt structure if the room is quiet:
  - "Anything conceptually unclear about what a CommandLineTool is doing?"
  - "Anyone hit an error with Docker or s4n specifically?"
  - "Otherwise, thumbs up if you're good to keep moving?"

- This is also a good moment to quickly scan the room / check if people
  are following along on their own laptops successfully, since the next
  section (compute_fertility) builds on the same environment setup.

Timing: 1-3 min depending on questions. Don't skip this even if pressed for
time — better to resolve confusion now before adding the R/Docker runtime
complexity in the next step.
-->

---
layout: fairagro
title: "Step 2: compute_fertility"
---

<div class="fa-bar"></div>

<style>
.workflow-row {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}
.box {
  border-radius: 14px;
  padding: 1.1rem 1.3rem;
  background: linear-gradient(160deg, #ffffff 0%, #f2fbf9 100%);
  border: 1.5px solid #cdeee6;
  box-shadow: 0 4px 12px rgba(15, 152, 132, 0.10);
}
.box.dimmed {
  opacity: 0.38;
  filter: grayscale(0.3);
}
.box.active {
  background: linear-gradient(160deg, #ffffff 0%, #f2fbf9 100%);
  border-color: #0f9884;
  box-shadow: 0 4px 18px rgba(15, 152, 132, 0.22);
}
.box-highlight {
  background: linear-gradient(160deg, #ffffff 0%, #f6faec 100%);
  border-color: #d7e79b;
  box-shadow: 0 4px 12px rgba(168, 200, 60, 0.20);
}
.box-header {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  margin-bottom: 0.6rem;
  flex-wrap: nowrap;
}
.box-avatar{
  flex-shrink:0;
  width:34px; height:34px;
  border-radius:50%; object-fit:cover;
  border:2px solid #ffffff; background:#ffffff;
  box-shadow:0 2px 6px rgba(15,152,132,0.25);
}
.box-avatar-group{
  flex-shrink:0;
  position:relative; width:48px; height:34px;
}
.box-avatar-group img{
  position:absolute; top:0;
  width:34px; height:34px;
  border-radius:50%; object-fit:cover;
  border:2px solid #ffffff; background:#ffffff;
  box-shadow:0 2px 6px rgba(168,200,60,0.35);
}
.box-avatar-group img:first-child{ left:0; z-index:2; }
.box-avatar-group img:last-child{ left:18px; z-index:1; }
.box h3 {
  margin: 0;
  font-family: "Fira Code", monospace;
  font-size: 1rem; font-weight: 700; color: #0b6f60;
  flex: 1; min-width: 0;
  white-space: nowrap; overflow: hidden; text-overflow: ellipsis;
}
.box ul { margin: 0; padding-left: 1.1rem; }
.box li {
  margin-bottom: 0.4rem;
  font-size: 0.84rem; line-height: 1.4; color: #333;
}
.box li b { color: #0b6f60; }
.lang {
  display: inline-block;
  font-size: 0.66rem; padding: 0.16rem 0.6rem;
  border-radius: 20px; font-weight: 700;
  letter-spacing: 0.02em; text-transform: uppercase; flex-shrink: 0;
}
.lang-r  { background: #0f9884; color: #ffffff; }
.lang-py { background: #A8C83C; color: #1a1a1a; }

/* problem callout */
.problem-callout{
  margin-top: 1rem;
  border-radius: 12px;
  padding: 12px 16px;
  background: linear-gradient(160deg, #fff9f0 0%, #fef2e0 100%);
  border: 1.5px solid #f5c97a;
  box-shadow: 0 3px 10px rgba(220,150,30,0.10);
  display: flex;
  gap: 12px;
  align-items: flex-start;
  font-family: 'Fira Sans', sans-serif;
}
.problem-icon{
  font-size: 1.6rem;
  flex-shrink: 0;
  line-height: 1;
  margin-top: 2px;
}
.problem-body{ flex: 1; min-width: 0; }
.problem-title{
  font-size: 0.82rem; font-weight: 700;
  color: #b45309; text-transform: uppercase;
  letter-spacing: 0.03em; margin-bottom: 5px;
}
.problem-text{
  font-size: 0.84rem; line-height: 1.5; color: #4b3a1a;
}
.problem-text b{ color: #92400e; }
.problem-text code{
  background: #fde9bc; padding: 0.02rem 0.32rem;
  border-radius: 3px; font-size: 0.88em;
}

/* solution hint */
.solution-hint{
  margin-top: 0.75rem;
  border-radius: 12px;
  padding: 10px 16px;
  background: linear-gradient(160deg, #f2fbf9 0%, #e6f7f3 100%);
  border: 1.5px solid #cdeee6;
  display: flex;
  gap: 12px;
  align-items: flex-start;
  font-family: 'Fira Sans', sans-serif;
}
.solution-hint .problem-title{ color: #0b6f60; }
.solution-hint .problem-text{ color: #1a3a35; }
.solution-hint .problem-text b{ color: #0b6f60; }
.solution-hint .problem-text code{
  background: #c8ece5; padding: 0.02rem 0.32rem;
  border-radius: 3px; font-size: 0.88em;
}
</style>

<div class="workflow-row mt-4">

  <div class="box dimmed">
    <div class="box-header">
      <img src="/researcher1.png" alt="Anna" class="box-avatar" />
      <h3>compute_ndvi</h3>
      <span class="lang lang-py">Python</span>
    </div>
    <ul>
      <li>Input: drone imagery — <b>red</b> + <b>near-infrared</b> bands</li>
      <li>Compares reflectance to derive a <b>plant health score (NDVI)</b></li>
    </ul>
  </div>

  <div class="box active">
    <div class="box-header">
      <img src="/researcher2.png" alt="Ben" class="box-avatar" />
      <h3>compute_fertility</h3>
      <span class="lang lang-r">R</span>
    </div>
    <ul>
      <li>Input: soil sample with measured <b>nitrate</b> + <b>organic matter</b></li>
      <li>Combines both into a single <b>soil quality score</b> per grid cell</li>
    </ul>
  </div>

  <div class="box box-highlight dimmed">
    <div class="box-header">
      <div class="box-avatar-group">
        <img src="/researcher1.png" alt="Anna" />
        <img src="/researcher2.png" alt="Ben" />
      </div>
      <h3>plot_zone_map</h3>
      <span class="lang lang-py">Python</span>
    </div>
    <ul>
      <li>Uses NDVI and soil fertility score</li>
      <li>Aligns them across the <b>14×10 grid</b> and plots management zones</li>
    </ul>
  </div>

</div>

<div class="solution-hint">
  <div><img src="/researcher1.png" alt="Anna" class="box-avatar" /></div>
  <div class="problem-body">
    <div class="problem-title">The situation</div>
    <div class="problem-text">
      Anna wants to execute  <b>Ben's script but she has not installed R on her machine</b>.
      She wants a way to run his R script <b>without changing her local environment</b>.
    </div>
  </div>
</div>


<!--
notes:
- Point at the three-box diagram: "We're moving to step two now — notice
  compute_ndvi is dimmed out, and compute_fertility is highlighted. This is
  Ben's turn."

- Read/paraphrase the "situation" callout: "Here's a very real problem —
  Anna wants to run Ben's R script to test the pipeline end-to-end, but she
  doesn't have R installed on her laptop, and she really doesn't want to
  install a whole new language runtime just to run one script."

- Pause for effect: "This is exactly the kind of friction that killed their
  collaboration back at the start of the day."

- Read/paraphrase the "solution" callout: "The fix is the same idea as
  before, but instead of building our own Docker image from a Dockerfile,
  we're going to pull an existing, publicly available image — r-base
  version 4.4.1 — that already has R installed and configured. And the
  best part: it's still the exact same s4n create command, just with a
  different flag for the runtime."

- Emphasize the takeaway: "This is the flexibility we talked about earlier
  — SciWIn doesn't care whether you're wrapping Python or R, a custom
  Dockerfile or a public image from Docker Hub. The workflow is exactly the
  same from the user's perspective."

- Bridge to next slide: "Let's go do it live."

Timing: ~1.5-2 min. This slide is mostly about building anticipation and
framing the problem before the live coding — don't rush past the callouts,
they set up the "why" before the "how."
-->

---
layout: fairagro
title: "CWL CommandLineTool: compute_fertility.cwl"
---

<script setup>
const lines2 = [
  {
    type: 'cmd',
    text: 's4n create -c r-base:4.4.1 --run-container docker Rscript code/compute_fertility/compute_fertility.R --soil data/soil.csv --output fertility.csv'
  },
  {
    type: 'info',
    icon: '▶️',
    segments: [
      { text: 'Executing: ' },
      { text: 'Rscript code/compute_fertility/compute_fertility.R --output fertility.csv --soil /tmp/ff7388a0/inputs/soil-stgef6bd02f/soil.csv',},
    ]
  },
   {
    type: 'info',
    text: 'Computed fertility index for 140 grid cells.'
  },
   {
    type: 'info',
    text: 'Fertility index range: 0.051 - 0.941'
  },
  {
    type: 'info',
    icon: '📄',
    text: 'Found outputs:'
  },
  {
    type: 'output',
    text: '- $(inputs.output)'
  },
  {
    type: 'info',
    icon: '📄',
    segments: [
      { text: 'Created CWL file ' },
      { text: 'workflows/compute_fertility/compute_fertility.cwl', class: 'text-green-400 font-semibold' },
    ]
  },
]
</script>

<div class="h-100">

<TerminalDemo :lines="lines2" />

</div>

<!--
notes:
- Same pattern as Anna's demo, so you can move a bit faster here.

- Before running: "Now Ben's turn — same idea, different language and
  runtime. Instead of a Dockerfile, we point s4n at an existing public
  image, r-base:4.4.1, and tell it to run our Rscript with --run-container
  docker."

- As the output appears: "Same live execution as before — it genuinely
  ran Ben's R script, computed a fertility index for all 140 grid cells,
  and found the output file automatically."

- Emphasize the takeaway: "Notice this is the exact same s4n create
  command shape as Anna's — just a different runtime flag. SciWIn doesn't
  care whether you're wrapping Python or R, a custom Dockerfile or a public
  image from Docker Hub."

- Point at the final line: "And again, a complete CWL file gets generated —
  workflows/compute_fertility/compute_fertility.cwl — with zero YAML
  written by hand."

- Bridge: "Two tools down. The third one — plot_zone_map — is yours to
  build."

Timing: ~1-1.5 min. This should feel noticeably quicker than Anna's demo
since the audience already understands the pattern — lean into the "see,
same thing again" pacing.
-->

---
layout: fairagro
title: From Command to CWL CommandLineTool
clicks: 5
---

<div class="fa-logo-title"></div>
<div class="fa-bar"></div>

<style>
.slidev-layout{ height:100%; display:flex; flex-direction:column; }
.map-page{ flex:1; min-height:0; display:flex; flex-direction:column; }

.map-wrap{
  flex:1; min-height:0;
  display:flex; gap:22px; align-items:stretch;
  font-family:'Fira Sans',sans-serif;
}
.map-left{ flex:0 0 340px; display:flex; flex-direction:column; min-height:0; overflow-y:auto; }
.map-right{ flex:1; min-width:0; min-height:0; display:flex; }

.map-command-card{
  border-radius:10px; padding:7px 9px 8px;
  background:linear-gradient(180deg,#fbfbfd 0%,#f4f5f9 100%);
  border:1px solid #e6e7ee;
  box-shadow:0 2px 8px rgba(20,20,40,0.05);
  margin-bottom:0.55rem; flex-shrink:0;
}
.map-command-code{
  font-family:'Fira Code','Courier New',monospace; font-size:0.62rem;
  line-height:1.55; margin-top:2px;
  display:flex; flex-wrap:wrap; align-items:center; gap:3px 5px;
}
.map-command-code .prompt{ color:#0f9884; font-weight:700; }
.tok{
  padding:1px 4px; border-radius:4px; transition:all .2s ease; color:#4b4f5e;
  white-space:nowrap;
}
.tok.s4n{ color:#a4a7b8; }
.tok.active-command{ background:#f2eefb; color:#5c3fc7; font-weight:700; }
.tok.active-input{ background:#e7f0ff; color:#2f6fed; font-weight:700; }
.tok.active-env{ background:#f2f9f2; color:#3d6b40; font-weight:700; }

.map-legend-title{
  font-weight:700; font-size:0.6rem; color:#0f9884;
  text-transform:uppercase; letter-spacing:.03em; margin-bottom:0.4rem;
}

.map-legend-item{
  display:flex; align-items:flex-start; gap:6px;
  margin-bottom:0.32rem; padding:5px 7px;
  border-radius:8px; border:1.2px solid #e6e7ee; background:#fafafc;
  opacity:0.45; transition:opacity .2s ease, background .2s ease, border-color .2s ease;
  flex-shrink:0;
}
.map-legend-item.active{ opacity:1; }

.map-legend-item .dot{
  flex-shrink:0; width:7px; height:7px; border-radius:50%; margin-top:3px;
}
.map-legend-item .txt{ font-size:0.7rem; line-height:1.28; color:#333; }
.map-legend-item .txt b{ font-weight:700; }
.map-legend-item code{ background:#f0f0f0; padding:0.02rem 0.3rem; border-radius:3px; font-size:0.85em; }

.dot.command{ background:#7b5fd1; }
.dot.input{ background:#2f6fed; }
.dot.output{ background:#e0524f; }
.dot.runtime{ background:#43a047; }

.map-legend-item.command.active{ background:#f2eefb; border-color:#d9ccfb; }
.map-legend-item.command.active .txt b{ color:#5c3fc7; }

.map-legend-item.input.active{ background:#e7f0ff; border-color:#bcd3ff; }
.map-legend-item.input.active .txt b{ color:#2f6fed; }

.map-legend-item.output.active{ background:#fde7e6; border-color:#f5c2c0; }
.map-legend-item.output.active .txt b{ color:#e0524f; }

.map-missing-note{
  margin-top:0.25rem; margin-bottom:0.35rem; border:1.5px solid #cfe6cf; border-radius:8px;
  padding:6px 8px; opacity:0.45; transition:opacity .2s ease, background .2s ease;
  flex-shrink:0;
}
.map-missing-note.active{ opacity:1; background:#f2f9f2; }
.map-missing-note .txt{ font-size:0.7rem; line-height:1.28; color:#3d6b40; font-style:italic; }
.map-missing-note .txt b{ font-weight:700; font-style:normal; }

.cwl-file-box{
  background:#fafbfc; border:1px solid #e5e7eb; border-radius:8px; padding:8px 11px;
  font-family:'Fira Code','Courier New',monospace; font-size:0.52rem;
  line-height:1.22; color:#374151;
  width:100%; box-sizing:border-box; overflow-y:auto;
}
.cwl-file-box .line{ padding:0 3px; border-radius:3px; transition:background .2s ease, color .2s ease; white-space:pre; }
.cwl-file-box .line.sp{ height:4px; line-height:0; padding:0; font-size:0; }
.cwl-file-box .comment{ color:#9ca3af; }
.cwl-file-box .key{ color:#111827; font-weight:600; }
.cwl-file-box .hl-command{ background:#f2eefb; color:#5c3fc7; }
.cwl-file-box .hl-input{ background:#e7f0ff; color:#1d4ed8; }
.cwl-file-box .hl-output{ background:#fde7e6; color:#c0392b; }
.cwl-file-box .hl-runtime{ background:#f2f9f2; color:#3d6b40; }
</style>

<div class="map-page">
<div class="map-wrap">

<div class="map-left">

<div class="map-command-card">
  <div class="map-command-title">💻 Terminal command</div>
  <div class="map-command-code">
    <span class="prompt">$</span>
    <span class="tok s4n">s4n create </span>
    <span class="tok" :class="{ 'active-env': $clicks >= 1 }">-c r-base:4.4.1</span>
    <span class="tok" :class="{ 'active-env': $clicks >= 1 }">--run-container docker</span>
    <span class="tok" :class="{ 'active-command': $clicks >= 2 }">Rscript code/compute_fertility/compute_fertility.R</span>
    <span class="tok" :class="{ 'active-input': $clicks >= 3 }">--soil data/soil.csv</span>
    <span class="tok" :class="{ 'active-input': $clicks >= 3 }">--output fertility.csv</span>
  </div>
</div>

<div class="map-legend-title">Components</div>

<div class="map-missing-note" :class="{ active: $clicks >= 1 }">
  <div class="txt"><span class="dot runtime" style="display:inline-block;margin-right:5px;"></span>🧩 <b>Runtime environment</b> — pull existing image <code>r-base:4.4.1</code> from registry, run via <code>docker</code>.</div>
</div>

<div class="map-legend-item command" :class="{ active: $clicks >= 2 }">
  <div class="dot command"></div>
  <div class="txt">⚡ <b>Command</b> → <code>baseCommand</code>. Script embedded via <code>InitialWorkDirRequirement</code>.</div>
</div>

<div class="map-legend-item input" :class="{ active: $clicks >= 3 }">
  <div class="dot input"></div>
  <div class="txt">📥 <b>Input</b> → <code>--soil data/soil.csv</code></div>
</div>

<div class="map-legend-item input" :class="{ active: $clicks >= 3 }">
  <div class="dot input"></div>
  <div class="txt">📥 <b>Input</b> → define name of output file <code>--output fertility.csv</code></div>
</div>

<div class="map-legend-item output" :class="{ active: $clicks >= 4 }">
  <div class="dot output"></div>
  <div class="txt">📤 <b>Output</b> → <code>fertility_csv</code> autodetected by s4n through git; because output file name was defined as input, it is linked to inputs.</div>
</div>

</div>
<div class="map-right">
<div class="cwl-file-box">
<div class="line"><span class="key">class</span>: CommandLineTool</div>
<div class="line"><span class="key">cwlVersion</span>: v1.2</div>
<div class="line"><span class="key">requirements</span>:</div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }">- <span class="key">class</span>: InitialWorkDirRequirement</div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }">&nbsp;&nbsp;listing:</div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }">&nbsp;&nbsp;- entry:</div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$include: ../../code/compute_fertility/compute_fertility.R</div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }">&nbsp;&nbsp;&nbsp;&nbsp;entryname: code/compute_fertility/compute_fertility.R</div>
<div class="line" :class="{ 'hl-runtime': $clicks >= 1 }">- <span class="key">class</span>: DockerRequirement</div>
<div class="line" :class="{ 'hl-runtime': $clicks >= 1 }">&nbsp;&nbsp;dockerPull: r-base:4.4.1</div>
<div class="line" :class="{ 'hl-output': $clicks >= 4 }">- <span class="key">class</span>: InlineJavascriptRequirement</div>
<div class="line sp"></div>
<div class="line sp"></div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }"><span class="key">inputs</span>:</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">- default:</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;&nbsp;&nbsp;class: File</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;&nbsp;&nbsp;location: ../../data/soil.csv</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;format: edam:format_3752</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;id: soil</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;inputBinding:</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;&nbsp;&nbsp;prefix: --soil</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;type: File</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">- default: fertility.csv</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;id: output</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;inputBinding:</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;&nbsp;&nbsp;prefix: --output</div>
<div class="line" :class="{ 'hl-input': $clicks >= 3 }">&nbsp;&nbsp;type: string</div>
<div class="line sp"></div>
<div class="line" :class="{ 'hl-output': $clicks >= 4 }"><span class="key">outputs</span>:</div>
<div class="line" :class="{ 'hl-output': $clicks >= 4 }">- format: edam:format_3752</div>
<div class="line" :class="{ 'hl-output': $clicks >= 4 }">&nbsp;&nbsp;id: fertility_csv</div>
<div class="line" :class="{ 'hl-output': $clicks >= 4 }">&nbsp;&nbsp;outputBinding:</div>
<div class="line" :class="{ 'hl-output': $clicks >= 4 }">&nbsp;&nbsp;&nbsp;&nbsp;glob: $(inputs.output)</div>
<div class="line" :class="{ 'hl-output': $clicks >= 4 }">&nbsp;&nbsp;type: File</div>
<div class="line sp"></div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }"><span class="key">baseCommand</span>:</div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }">- Rscript</div>
<div class="line" :class="{ 'hl-command': $clicks >= 2 }">- code/compute_fertility/compute_fertility.R</div>
<div class="line sp"></div>
<div class="line comment">$namespaces:</div>
<div class="line comment">&nbsp;&nbsp;edam: http://edamontology.org/</div>
<div class="line comment">$schemas:</div>
<div class="line comment">- https://edamontology.org/EDAM.owl</div>
</div>
</div>

</div>
</div>

<!--
notes:
- Frame this as a comparison to the earlier slide: "This is the exact same
  breakdown we did for Anna's tool — let's go through the clicks quickly,
  and I want you to specifically notice what's different and what's
  identical."

- [Click 1] Runtime highlights.
  → Say: "Here's the one real difference — instead of a DockerRequirement
  with a dockerFile pointing at a local file, we now have a dockerPull
  pointing directly at r-base:4.4.1 on the registry. That's it. One line
  changed."

- [Click 2] Command highlights.
  → Say: "Just like before, the R script gets embedded directly into the
  CWL file via InitialWorkDirRequirement, and baseCommand now says Rscript
  instead of python3."

- [Click 3] Inputs highlight.
  → Say: "Same pattern again — soil and output become formal, typed inputs
  with their command-line flags recorded automatically."

- [Click 4] Outputs highlight.
  → Say: "And the output — fertility_csv — follows the exact same glob
  pattern logic as ndvi_csv did."

- Key takeaway, deliver this deliberately: "The structure of this file is
  almost identical to Anna's Python tool. Different language, different
  runtime, same CWL shape. This is exactly why CWL lets Anna and Ben combine
  their work — from CWL's perspective, a Python tool and an R tool look
  the same."

- Bridge to next slide: "Reference slide with the commands is next, then
  we'll pause for questions before your turn."

Timing: ~2 min — should move faster than the compute_ndvi walkthrough since
you're mostly pointing out similarities rather than explaining concepts from
scratch.
-->

---
layout: fairagro
title: "Summary: compute_fertility.R"
---

<script setup>
import { ref } from 'vue'

const copiedIndex = ref(null)

function copyCommand(text, index) {
  navigator.clipboard.writeText(text).then(() => {
    copiedIndex.value = index
    setTimeout(() => {
      copiedIndex.value = null
    }, 1500)
  })
}

const cmd1 = 'Rscript code/compute_fertility/compute_fertility.R --soil data/soil.csv --output fertility.csv'
const cmd2 = 's4n create -c r-base:4.4.1  --run-container docker Rscript code/compute_fertility/compute_fertility.R --soil data/soil.csv --output fertility.csv'
</script>

<div class="fa-bar"></div>

<style>
.ref-page{ font-family:'Fira Sans',sans-serif; }
.ref-section{
  border-radius:12px; padding:12px 16px;
  background:linear-gradient(180deg,#fbfbfd 0%,#f4f5f9 100%);
  border:1px solid #e6e7ee;
  margin-bottom:0.8rem;
}
.ref-section.highlight{
  background:linear-gradient(180deg,#f2fbf9 0%,#e6f7f3 100%);
  border-color:#cdeee6;
}
.ref-label{
  font-size:0.78rem; font-weight:700; color:#0f9884;
  text-transform:uppercase; letter-spacing:.03em; margin-bottom:6px;
}
.ref-cmd-wrap{
  position:relative;
  display:flex;
  align-items:flex-start;
  gap:8px;
}
.ref-cmd{
  flex:1; min-width:0;
  font-family:'Fira Code','Courier New',monospace; font-size:0.78rem;
  color:#374151; background:#ffffff; border:1px solid #e5e7eb;
  border-radius:6px; padding:8px 10px; line-height:1.5; word-break:break-word;
}
.ref-cmd .prompt{ color:#0f9884; font-weight:700; margin-right:6px; }

.copy-btn{
  flex-shrink:0;
  display:flex; align-items:center; gap:4px;
  font-family:'Fira Sans',sans-serif;
  font-size:0.68rem; font-weight:700;
  color:#0f9884;
  background:#ffffff;
  border:1px solid #cdeee6;
  border-radius:6px;
  padding:8px 10px;
  cursor:pointer;
  transition:all 0.15s ease;
  white-space:nowrap;
}
.copy-btn:hover{
  background:#f2fbf9;
  border-color:#0f9884;
}
.copy-btn.copied{
  background:#0f9884;
  border-color:#0f9884;
  color:#ffffff;
}

.ref-note{
  margin-top:6px; font-size:0.78rem; color:#4b5563; line-height:1.4;
}
.ref-note code{ background:#f0f0f0; padding:0.02rem 0.3rem; border-radius:3px; }
</style>

<div class="ref-page">

<div class="ref-section">
  <div class="ref-label">▶️ Plain script call</div>
  <div class="ref-cmd-wrap">
    <div class="ref-cmd"><span class="prompt">$</span>Rscript code/compute_fertility/compute_fertility.R --soil data/soil.csv --output fertility.csv</div>
    <button class="copy-btn" :class="{ copied: copiedIndex === 1 }" @click="copyCommand(cmd1, 1)">
      {{ copiedIndex === 1 ? '✓ Copied' : '📋 Copy' }}
    </button>
  </div>
  <div class="ref-note">Computed fertility index for 140 grid cells → range: 0.051 – 0.941</div>
</div>

<div class="ref-section highlight">
  <div class="ref-label">⚙️ Turn it into a CWL CommandLineTool</div>
  <div class="ref-cmd-wrap">
    <div class="ref-cmd"><span class="prompt">$</span>s4n create -c r-base:4.4.1 --run-container docker Rscript code/compute_fertility/compute_fertility.R --soil data/soil.csv --output fertility.csv</div>
    <button class="copy-btn" :class="{ copied: copiedIndex === 2 }" @click="copyCommand(cmd2, 2)">
      {{ copiedIndex === 2 ? '✓ Copied' : '📋 Copy' }}
    </button>
  </div>
  <div class="ref-note">Creates <code>workflows/compute_fertility/compute_fertility.cwl</code></div>
</div>

</div>

<!--
notes:
- Same style as the earlier reference slide — brief, mostly for lookup.

- Point out the note under the first command: "Fertility index ranged from
  about 0.05 to 0.94 across the 140 grid cells — plenty of variation across
  the field for this to be a meaningful management factor."

- Point out the s4n command result: "This created
  workflows/compute_fertility/compute_fertility.cwl — Ben's tool, fully
  wrapped, sitting right alongside Anna's."

- Optional connecting comment: "At this point, we technically have two
  fully independent, reproducible, containerized tools — one Python, one R
  — described in the exact same standard format. That's the foundation
  we'll build the final workflow on this afternoon... but first, it's your
  turn to build the third piece."

Timing: ~1 min, or slightly longer if people are copying commands to try
themselves.
-->

---
layout: fairagro
title: " Your Turn: plot_zone_map"
---

<div class="fa-bar"></div>

<style>
.workflow-row {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}
.box {
  border-radius: 14px;
  padding: 1.1rem 1.3rem;
  background: linear-gradient(160deg, #ffffff 0%, #f2fbf9 100%);
  border: 1.5px solid #cdeee6;
  box-shadow: 0 4px 12px rgba(15, 152, 132, 0.10);
}
.box.dimmed {
  opacity: 0.38;
  filter: grayscale(0.3);
}
.box.active {
  background: linear-gradient(160deg, #ffffff 0%, #f6faec 100%);
  border-color: #A8C83C;
  box-shadow: 0 4px 18px rgba(168, 200, 60, 0.28);
}
.box-highlight {
  background: linear-gradient(160deg, #ffffff 0%, #f6faec 100%);
  border-color: #d7e79b;
  box-shadow: 0 4px 12px rgba(168, 200, 60, 0.20);
}
.box-header {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  margin-bottom: 0.6rem;
  flex-wrap: nowrap;
}
.box-avatar{
  flex-shrink:0;
  width:34px; height:34px;
  border-radius:50%; object-fit:cover;
  border:2px solid #ffffff; background:#ffffff;
  box-shadow:0 2px 6px rgba(15,152,132,0.25);
}
.box-avatar-group{
  flex-shrink:0;
  position:relative; width:48px; height:34px;
}
.box-avatar-group img{
  position:absolute; top:0;
  width:34px; height:34px;
  border-radius:50%; object-fit:cover;
  border:2px solid #ffffff; background:#ffffff;
  box-shadow:0 2px 6px rgba(168,200,60,0.35);
}
.box-avatar-group img:first-child{ left:0; z-index:2; }
.box-avatar-group img:last-child{ left:18px; z-index:1; }
.box h3 {
  margin: 0;
  font-family: "Fira Code", monospace;
  font-size: 1rem; font-weight: 700; color: #0b6f60;
  flex: 1; min-width: 0;
  white-space: nowrap; overflow: hidden; text-overflow: ellipsis;
}
.box.active h3 { color: #4a6b0a; }
.box ul { margin: 0; padding-left: 1.1rem; }
.box li {
  margin-bottom: 0.4rem;
  font-size: 0.84rem; line-height: 1.4; color: #333;
}
.box li b { color: #0b6f60; }
.box.active li b { color: #4a6b0a; }
.lang {
  display: inline-block;
  font-size: 0.66rem; padding: 0.16rem 0.6rem;
  border-radius: 20px; font-weight: 700;
  letter-spacing: 0.02em; text-transform: uppercase; flex-shrink: 0;
}
.lang-r  { background: #0f9884; color: #ffffff; }
.lang-py { background: #A8C83C; color: #1a1a1a; }

/* exercise callout */
.exercise-callout{
  margin-top: 1rem;
  border-radius: 12px;
  padding: 12px 16px;
  background: linear-gradient(160deg, #f7faed 0%, #eef5d0 100%);
  border: 1.5px solid #c8dc6e;
  box-shadow: 0 3px 10px rgba(168,200,60,0.14);
  display: flex;
  gap: 12px;
  align-items: flex-start;
  font-family: 'Fira Sans', sans-serif;
}
.callout-icon{
  font-size: 1.6rem;
  flex-shrink: 0;
  line-height: 1;
  margin-top: 2px;
}
.callout-body{ flex: 1; min-width: 0; }
.callout-title{
  font-size: 0.82rem; font-weight: 700;
  color: #4a6b0a; text-transform: uppercase;
  letter-spacing: 0.03em; margin-bottom: 5px;
}
.callout-text{
  font-size: 0.84rem; line-height: 1.5; color: #2e3d10;
}
.callout-text b{ color: #4a6b0a; }
.callout-text code{
  background: #dfedaa; padding: 0.02rem 0.32rem;
  border-radius: 3px; font-size: 0.88em;
}

/* hint callout */
.hint-callout{
  margin-top: 0.75rem;
  border-radius: 12px;
  padding: 10px 16px;
  background: linear-gradient(160deg, #f2fbf9 0%, #e6f7f3 100%);
  border: 1.5px solid #cdeee6;
  display: flex;
  gap: 12px;
  align-items: flex-start;
  font-family: 'Fira Sans', sans-serif;
}
.hint-callout .callout-title{ color: #0b6f60; }
.hint-callout .callout-text{ color: #1a3a35; }
.hint-callout .callout-text b{ color: #0b6f60; }
.hint-callout .callout-text code{
  background: #c8ece5; padding: 0.02rem 0.32rem;
  border-radius: 3px; font-size: 0.88em;
}
</style>

<div class="workflow-row mt-4">

  <div class="box dimmed">
    <div class="box-header">
      <img src="/researcher1.png" alt="Anna" class="box-avatar" />
      <h3>compute_ndvi</h3>
      <span class="lang lang-py">Python</span>
    </div>
    <ul>
      <li>Input: drone imagery — <b>red</b> + <b>near-infrared</b> bands</li>
      <li>Compares reflectance to derive a <b>plant health score (NDVI)</b></li>
    </ul>
  </div>

  <div class="box dimmed">
    <div class="box-header">
      <img src="/researcher2.png" alt="Ben" class="box-avatar" />
      <h3>compute_fertility</h3>
      <span class="lang lang-r">R</span>
    </div>
    <ul>
      <li>Input: soil sample with measured <b>nitrate</b> + <b>organic matter</b></li>
      <li>Combines both into a single <b>soil quality score</b> per grid cell</li>
    </ul>
  </div>

  <div class="box box-highlight active">
    <div class="box-header">
      <div class="box-avatar-group">
        <img src="/researcher1.png" alt="Anna" />
        <img src="/researcher2.png" alt="Ben" />
      </div>
      <h3>plot_zone_map</h3>
      <span class="lang lang-py">Python</span>
    </div>
    <ul>
      <li>Uses NDVI and soil fertility score</li>
      <li>Aligns them across the <b>14×10 grid</b> and plots management zones</li>
    </ul>
  </div>

</div>

<div class="exercise-callout">
  <div class="callout-icon">🙌</div>
  <div class="callout-body">
    <div class="callout-title">Your turn</div>
    <div class="callout-text">
      Now it is <b>your turn</b> to create a CWL CommandLineTool for <code>plot_zone_map.py</code>. 
    </div>
  </div>
</div>

<!--
notes:
- Point at the diagram: "Now both compute_ndvi and compute_fertility are
  dimmed — we've done those together. plot_zone_map is highlighted — this
  one's on you."

- Emphasize why this step matters: "Remember, this step is special — it's
  the only one that depends on BOTH Anna's and Ben's work. This is
  literally the moment their collaboration comes together into one output."

- Read the callout: "You've now seen this exact pattern twice — wrap a
  script, tell it the Docker environment, let s4n figure out the inputs and
  outputs. Now you'll do it yourselves for plot_zone_map.py."

- Set expectations for the exercise: "Head to the next slide — you'll find
  the task, some hints if you get stuck, and a full reference CWL file to
  check your work against once you're done. Take about 10 minutes, work
  with your neighbor if you'd like, and flag me down if you hit a wall."

- Bridge to next slide (the exercise itself).

Timing: ~1-1.5 min framing, then transition into the hands-on exercise time
(which will take significantly longer — plan for ~10-15 min of actual
working time before regrouping).
-->

---
layout: fairagro 
title: "Exercise: Build the CWL Tool for plot_zone_map"
disabled: true
--- 

<div class="fa-logo-title"></div> <div class="fa-bar"></div> <style> .slidev-layout{ height:100%; display:flex; flex-direction:column; } .ex-page{ flex:1; min-height:0; display:flex; flex-direction:column; font-family:'Fira Sans',sans-serif; } .ex-task{ border-radius:10px; padding:8px 12px; background:linear-gradient(180deg,#fbfbfd 0%,#f4f5f9 100%); border:1px solid #e6e7ee; box-shadow:0 2px 8px rgba(20,20,40,0.05); margin-bottom:0.6rem; flex-shrink:0; } .ex-task-label{ font-size:0.75rem; font-weight:700; color:#0f9884; text-transform:uppercase; letter-spacing:.03em; margin-bottom:2px; } .ex-task-text{ font-size:0.82rem; color:#374151; line-height:1.4; } .ex-task-text code{ background:#f0f0f0; padding:0.02rem 0.3rem; border-radius:3px; } .ex-columns{ flex:1; min-height:0; display:flex; gap:20px; align-items:stretch; } .ex-hints{ flex:0 0 44%; min-height:0; display:flex; flex-direction:column; gap:0.4rem; overflow-y:auto; } .ex-reference{ flex:1; min-width:0; min-height:0; display:flex; flex-direction:column; overflow:hidden; } .hint-box, .solution-box, .reference-box{ border-radius:8px; border:1.2px solid #e6e7ee; background:#fafafc; padding:6px 9px; flex-shrink:0; } .hint-box summary, .solution-box summary, .reference-box summary{ cursor:pointer; font-size:0.75rem; font-weight:700; color:#333; list-style:none; display:flex; align-items:center; gap:5px; } .hint-box summary::-webkit-details-marker, .solution-box summary::-webkit-details-marker, .reference-box summary::-webkit-details-marker{ display:none; } .hint-box summary::before{ content:'▸'; color:#2f6fed; font-size:0.78rem; transition:transform .15s ease; } .hint-box[open] summary::before{ transform:rotate(90deg); } .hint-box{ border-color:#bcd3ff; } .hint-box[open]{ background:#e7f0ff; } .solution-box summary::before{ content:'▸'; color:#0f9884; font-size:0.78rem; transition:transform .15s ease; } .solution-box[open] summary::before{ transform:rotate(90deg); } .solution-box{ border-color:#cfe6cf; } .solution-box[open]{ background:#f2f9f2; } .reference-box{ border-color:#d8dae0; min-height:0; overflow:hidden; display:flex; flex-direction:column; } .reference-box summary::before{ content:'▸'; color:#6b7280; font-size:0.78rem; transition:transform .15s ease; } .reference-box[open] summary::before{ transform:rotate(90deg); } .reference-box[open]{ background:#f4f5f9; flex:0 1 auto; min-height:0; overflow:visible; } .hint-content, .solution-content{ margin-top:5px; font-size:0.72rem; line-height:1.5; color:#374151; } .hint-content code, .solution-content code{ background:#f0f0f0; padding:0.02rem 0.3rem; border-radius:3px; } .cmd-line{ font-family:'Fira Code','Courier New',monospace; font-size:0.68rem; color:#4b4f5e; line-height:1.5; word-break:break-word; background:#fff; border:1px solid #e5e7eb; border-radius:6px; padding:5px 8px; margin-top:4px; } .cmd-line .prompt{ color:#0f9884; font-weight:700; margin-right:4px; } .ref-cwl-box{ margin-top:5px; background:#ffffff; border:1px solid #e5e7eb; border-radius:6px; padding:8px 11px; font-family:'Fira Code','Courier New',monospace; font-size:0.62rem; line-height:1.35; color:#374151; flex:1; min-height:0; max-height:300px; overflow-y:auto; } .ref-cwl-box .line{ white-space:pre; } .ref-cwl-box .comment{ color:#9ca3af; } .ref-cwl-box .key{ color:#2563eb; font-weight:600; } .ref-cwl-box .sp{ height:4px; } </style> <div class="ex-page"> <div class="ex-task"> <div class="ex-task-label">🎯 Your Task</div> <div class="ex-task-text"> Write a CWL <code>CommandLineTool</code> for the script <code>plot_zone_map.py</code>. Think about <b>requirements</b> (Docker), <b>inputs</b>, and <b>outputs</b>. </div> </div> <div class="ex-columns"> <div class="ex-hints"> <details class="hint-box"> <summary>💡 Hint 1 — What was the regular script call?</summary> <div class="hint-content"> <div class="cmd-line"><span class="prompt">$</span>python3 code/plot_zone_map/plot_zone_map.py --ndvi ndvi.csv --fertility fertility.csv --title "Field Management Zones" --output zone_map.png</div> </div> </details> <details class="hint-box"> <summary>💡 Hint 2 — Requirements</summary> <div class="hint-content"> You can reuse the <code>Dockerfile</code> that we used in the <code>compute_ndvi</code> step. </div> </details> <details class="solution-box"> <summary>✅ Show full solution</summary> <div class="solution-content"> <div class="cmd-line"><span class="prompt">$</span>s4n create -c Dockerfile -t demo:v1.0.0 python3 code/plot_zone_map/plot_zone_map.py --ndvi ndvi.csv --fertility fertility.csv --title "Field Management Zones" --output zone_map.png</div> </div> </details> </div> <div class="ex-reference"> <details class="reference-box"> <summary>📄 Show reference CWL file (compare your result)</summary> <div class="ref-cwl-box"> <div class="line comment">#!/usr/bin/env cwl-runner</div> <div class="sp"></div> <div class="line"><span class="key">cwlVersion</span>: v1.2</div> <div class="line"><span class="key">class</span>: CommandLineTool</div> <div class="sp"></div> <div class="line"><span class="key">requirements</span>:</div> <div class="line">- <span class="key">class</span>: InitialWorkDirRequirement</div> <div class="line">&nbsp;&nbsp;listing:</div> <div class="line">&nbsp;&nbsp;- entryname: code/plot_zone_map/plot_zone_map.py</div> <div class="line">&nbsp;&nbsp;&nbsp;&nbsp;entry:</div> <div class="line">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$include: ../../code/plot_zone_map/plot_zone_map.py</div> <div class="line">- <span class="key">class</span>: DockerRequirement</div> <div class="line">&nbsp;&nbsp;dockerFile:</div> <div class="line">&nbsp;&nbsp;&nbsp;&nbsp;$include: ../../Dockerfile</div> <div class="line">&nbsp;&nbsp;dockerImageId: demo:v1.0.0</div> <div class="line">- <span class="key">class</span>: InlineJavascriptRequirement</div> <div class="sp"></div> <div class="line"><span class="key">inputs</span>:</div> <div class="line">- id: ndvi</div> <div class="line">&nbsp;&nbsp;type: File</div> <div class="line">&nbsp;&nbsp;default:</div> <div class="line">&nbsp;&nbsp;&nbsp;&nbsp;class: File</div> <div class="line">&nbsp;&nbsp;&nbsp;&nbsp;location: ../../ndvi.csv</div> <div class="line">&nbsp;&nbsp;inputBinding:</div> <div class="line">&nbsp;&nbsp;&nbsp;&nbsp;prefix: --ndvi</div> <div class="line">- id: fertility</div> <div class="line">&nbsp;&nbsp;type: File</div> <div class="line">&nbsp;&nbsp;default:</div> <div class="line">&nbsp;&nbsp;&nbsp;&nbsp;class: File</div> <div class="line">&nbsp;&nbsp;&nbsp;&nbsp;location: ../../fertility.csv</div> <div class="line">&nbsp;&nbsp;inputBinding:</div> <div class="line">&nbsp;&nbsp;&nbsp;&nbsp;prefix: --fertility</div> <div class="line">- id: title</div> <div class="line">&nbsp;&nbsp;type: string</div> <div class="line">&nbsp;&nbsp;default: Field Management Zones</div> <div class="line">&nbsp;&nbsp;inputBinding:</div> <div class="line">&nbsp;&nbsp;&nbsp;&nbsp;prefix: --title</div> <div class="line">- id: output</div> <div class="line">&nbsp;&nbsp;type: string</div> <div class="line">&nbsp;&nbsp;default: zone_map.png</div> <div class="line">&nbsp;&nbsp;inputBinding:</div> <div class="line">&nbsp;&nbsp;&nbsp;&nbsp;prefix: --output</div> <div class="sp"></div> <div class="line"><span class="key">outputs</span>:</div> <div class="line">- id: zone_map_png</div> <div class="line">&nbsp;&nbsp;type: File</div> <div class="line">&nbsp;&nbsp;outputBinding:</div> <div class="line">&nbsp;&nbsp;&nbsp;&nbsp;glob: $(inputs.output)</div> <div class="sp"></div> <div class="line"><span class="key">baseCommand</span>:</div> <div class="line">- python3</div> <div class="line">- code/plot_zone_map/plot_zone_map.py</div> </div> </details> </div> </div> </div>

<!--
notes:
- These two slides are functionally the same exercise (one appears to be a
  disabled/backup version) — treat them as the hands-on working slide.

- Kick off the exercise clearly: "Okay, this is your task. You need to wrap
  plot_zone_map.py into a CWL CommandLineTool, just like we did for the
  previous two scripts. Think about three things: what Docker requirement
  it needs, what its inputs are, and what output it produces."

- Give a starting nudge if the room looks unsure: "If you want a starting
  point, just look at the plain script call — that's Hint 1. From there,
  think about what command you'd give to s4n create."

- While people work (~10 min):
  - Circulate if in person, or monitor chat/breakout rooms if remote.
  - Common sticking points to watch for:
    - Forgetting the --title argument has a space in it (needs quotes)
    - Not realizing they can reuse the same Dockerfile from compute_ndvi
      (Hint 2 addresses this directly)
    - Confusion about multiple inputs — remind them plot_zone_map takes
      FOUR inputs: ndvi, fertility, title, and output — more than the
      previous two tools.

- After ~10 minutes, call time: "Let's regroup. Who wants to share the
  command they used?" — Let a volunteer share their s4n create command
  aloud, then reveal the Hint 2 / Solution box together as a group if
  helpful.

- Reveal the reference CWL file: "Let's open up the reference file and
  compare — does everyone's generated file look roughly like this?" Point
  out the four inputs (ndvi, fertility, title, output) and note that title
  and output are both plain strings, not files — a subtle but important
  distinction from the file-type inputs.

- Close out the exercise: "Great work — you've now built all three
  CommandLineTools for this workflow, in two different languages, entirely
  through the command line, without writing a single line of CWL by hand.
  Next, we'll connect these three tools into one full Workflow file."

Timing: ~12-15 min total (10 min working + 3-5 min regroup/review). This is
the biggest time investment of the session — protect this time and resist
the urge to rush the regroup discussion, since seeing others' solutions
reinforces the pattern before moving to the final integration step.
-->

---
layout: fairagro
title: "Exercise: Build the CWL Tool for plot_zone_map"
---

<script setup>
import { ref } from 'vue'

const copiedIndex = ref(null)

function copyCommand(text, index) {
  navigator.clipboard.writeText(text).then(() => {
    copiedIndex.value = index
    setTimeout(() => {
      copiedIndex.value = null
    }, 1500)
  })
}

const cmd1 = 'python3 code/plot_zone_map/plot_zone_map.py --ndvi ndvi.csv --fertility fertility.csv --title "Field Management Zones" --output zone_map.png'
const cmd2 = 's4n create -c Dockerfile -t demo:v1.0.0 python3 code/plot_zone_map/plot_zone_map.py --ndvi ndvi.csv --fertility fertility.csv --title "Field Management Zones" --output zone_map.png'
</script>

<div class="fa-logo-title"></div>
<div class="fa-bar"></div>

<style>
.slidev-layout{ height:100%; display:flex; flex-direction:column; }
.ex-page{ flex:1; min-height:0; display:flex; flex-direction:column; font-family:'Fira Sans',sans-serif; }

.ex-task{
  border-radius:10px; padding:8px 12px;
  background:linear-gradient(180deg,#fbfbfd 0%,#f4f5f9 100%);
  border:1px solid #e6e7ee;
  box-shadow:0 2px 8px rgba(20,20,40,0.05);
  margin-bottom:0.6rem; flex-shrink:0;
}
.ex-task-label{
  font-size:0.75rem; font-weight:700; color:#0f9884;
  text-transform:uppercase; letter-spacing:.03em; margin-bottom:2px;
}
.ex-task-text{ font-size:0.82rem; color:#374151; line-height:1.4; }
.ex-task-text code{ background:#f0f0f0; padding:0.02rem 0.3rem; border-radius:3px; }

.ex-columns{ flex:1; min-height:0; display:flex; gap:20px; align-items:stretch; }
.ex-hints{ flex:0 0 44%; min-height:0; display:flex; flex-direction:column; gap:0.4rem; overflow-y:auto; }
.ex-reference{ flex:1; min-width:0; min-height:0; display:flex; flex-direction:column; overflow:hidden; }

.hint-box, .solution-box, .reference-box{
  border-radius:8px; border:1.2px solid #e6e7ee; background:#fafafc;
  padding:6px 9px; flex-shrink:0;
}
.hint-box summary, .solution-box summary, .reference-box summary{
  cursor:pointer; font-size:0.75rem; font-weight:700; color:#333;
  list-style:none; display:flex; align-items:center; gap:5px;
}
.hint-box summary::-webkit-details-marker,
.solution-box summary::-webkit-details-marker,
.reference-box summary::-webkit-details-marker{ display:none; }

.hint-box summary::before{ content:'▸'; color:#2f6fed; font-size:0.78rem; transition:transform .15s ease; }
.hint-box[open] summary::before{ transform:rotate(90deg); }
.hint-box{ border-color:#bcd3ff; }
.hint-box[open]{ background:#e7f0ff; }

.solution-box summary::before{ content:'▸'; color:#0f9884; font-size:0.78rem; transition:transform .15s ease; }
.solution-box[open] summary::before{ transform:rotate(90deg); }
.solution-box{ border-color:#cfe6cf; }
.solution-box[open]{ background:#f2f9f2; }

.reference-box{
  border-color:#d8dae0; min-height:0; overflow:hidden;
  display:flex; flex-direction:column;
}
.reference-box summary::before{ content:'▸'; color:#6b7280; font-size:0.78rem; transition:transform .15s ease; }
.reference-box[open] summary::before{ transform:rotate(90deg); }
.reference-box[open]{
  background:#f4f5f9;
  flex:0 1 auto;
  min-height:0;
  overflow:visible;
}

.hint-content, .solution-content{
  margin-top:5px; font-size:0.72rem; line-height:1.5; color:#374151;
}
.hint-content code, .solution-content code{
  background:#f0f0f0; padding:0.02rem 0.3rem; border-radius:3px;
}

.cmd-line-wrap{
  display:flex;
  align-items:flex-start;
  gap:6px;
  margin-top:4px;
}
.cmd-line{
  flex:1; min-width:0;
  font-family:'Fira Code','Courier New',monospace; font-size:0.68rem;
  color:#4b4f5e; line-height:1.5; word-break:break-word;
  background:#fff; border:1px solid #e5e7eb; border-radius:6px;
  padding:5px 8px;
}
.cmd-line .prompt{ color:#0f9884; font-weight:700; margin-right:4px; }

.copy-btn{
  flex-shrink:0;
  display:flex; align-items:center; gap:3px;
  font-family:'Fira Sans',sans-serif;
  font-size:0.62rem; font-weight:700;
  color:#0f9884;
  background:#ffffff;
  border:1px solid #cdeee6;
  border-radius:6px;
  padding:5px 7px;
  cursor:pointer;
  transition:all 0.15s ease;
  white-space:nowrap;
}
.copy-btn:hover{
  background:#f2fbf9;
  border-color:#0f9884;
}
.copy-btn.copied{
  background:#0f9884;
  border-color:#0f9884;
  color:#ffffff;
}

.ref-cwl-box{
  margin-top:5px; background:#ffffff; border:1px solid #e5e7eb; border-radius:6px;
  padding:8px 11px; font-family:'Fira Code','Courier New',monospace; font-size:0.62rem;
  line-height:1.35; color:#374151;
  flex:1; min-height:0;
  max-height:300px;
  overflow-y:auto;
}
.ref-cwl-box .line{ white-space:pre; }
.ref-cwl-box .comment{ color:#9ca3af; }
.ref-cwl-box .key{ color:#2563eb; font-weight:600; }
.ref-cwl-box .sp{ height:4px; }
</style>

<div class="ex-page">

<div class="ex-task">
  <div class="ex-task-label">🎯 Your Task</div>
  <div class="ex-task-text">
    Write a CWL <code>CommandLineTool</code> for the script <code>plot_zone_map.py</code>. Think about
    <b>requirements</b> (Docker), <b>inputs</b>, and <b>outputs</b>.
  </div>
</div>

<div class="ex-columns">

<div class="ex-hints">

<details class="hint-box">
<summary>💡 Hint 1 — What was the regular script call?</summary>
<div class="hint-content">
<div class="cmd-line-wrap">
  <div class="cmd-line"><span class="prompt">$</span>python3 code/plot_zone_map/plot_zone_map.py --ndvi ndvi.csv --fertility fertility.csv --title "Field Management Zones" --output zone_map.png</div>
  <button class="copy-btn" :class="{ copied: copiedIndex === 1 }" @click="copyCommand(cmd1, 1)">
    {{ copiedIndex === 1 ? '✓' : '📋' }}
  </button>
</div>
</div>
</details>

<details class="hint-box">
<summary>💡 Hint 2 — Requirements</summary>
<div class="hint-content">
You can reuse the <code>Dockerfile</code> that we used in the <code>compute_ndvi</code> step.
</div>
</details>

<details class="solution-box">
<summary>✅ Show full solution</summary>
<div class="solution-content">
<div class="cmd-line-wrap">
  <div class="cmd-line"><span class="prompt">$</span>s4n create -c Dockerfile -t demo:v1.0.0 python3 code/plot_zone_map/plot_zone_map.py --ndvi ndvi.csv --fertility fertility.csv --title "Field Management Zones" --output zone_map.png</div>
  <button class="copy-btn" :class="{ copied: copiedIndex === 2 }" @click="copyCommand(cmd2, 2)">
    {{ copiedIndex === 2 ? '✓' : '📋' }}
  </button>
</div>
</div>
</details>

</div>

<div class="ex-reference">

<details class="reference-box">
<summary>📄 Show reference CWL file (compare your result)</summary>
<div class="ref-cwl-box">
<div class="line comment">#!/usr/bin/env cwl-runner</div>
<div class="sp"></div>
<div class="line"><span class="key">cwlVersion</span>: v1.2</div>
<div class="line"><span class="key">class</span>: CommandLineTool</div>
<div class="sp"></div>
<div class="line"><span class="key">requirements</span>:</div>
<div class="line">- <span class="key">class</span>: InitialWorkDirRequirement</div>
<div class="line">&nbsp;&nbsp;listing:</div>
<div class="line">&nbsp;&nbsp;- entryname: code/plot_zone_map/plot_zone_map.py</div>
<div class="line">&nbsp;&nbsp;&nbsp;&nbsp;entry:</div>
<div class="line">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$include: ../../code/plot_zone_map/plot_zone_map.py</div>
<div class="line">- <span class="key">class</span>: DockerRequirement</div>
<div class="line">&nbsp;&nbsp;dockerFile:</div>
<div class="line">&nbsp;&nbsp;&nbsp;&nbsp;$include: ../../Dockerfile</div>
<div class="line">&nbsp;&nbsp;dockerImageId: demo:v1.0.0</div>
<div class="line">- <span class="key">class</span>: InlineJavascriptRequirement</div>
<div class="sp"></div>
<div class="line"><span class="key">inputs</span>:</div>
<div class="line">- id: ndvi</div>
<div class="line">&nbsp;&nbsp;type: File</div>
<div class="line">&nbsp;&nbsp;default:</div>
<div class="line">&nbsp;&nbsp;&nbsp;&nbsp;class: File</div>
<div class="line">&nbsp;&nbsp;&nbsp;&nbsp;location: ../../ndvi.csv</div>
<div class="line">&nbsp;&nbsp;inputBinding:</div>
<div class="line">&nbsp;&nbsp;&nbsp;&nbsp;prefix: --ndvi</div>
<div class="line">- id: fertility</div>
<div class="line">&nbsp;&nbsp;type: File</div>
<div class="line">&nbsp;&nbsp;default:</div>
<div class="line">&nbsp;&nbsp;&nbsp;&nbsp;class: File</div>
<div class="line">&nbsp;&nbsp;&nbsp;&nbsp;location: ../../fertility.csv</div>
<div class="line">&nbsp;&nbsp;inputBinding:</div>
<div class="line">&nbsp;&nbsp;&nbsp;&nbsp;prefix: --fertility</div>
<div class="line">- id: title</div>
<div class="line">&nbsp;&nbsp;type: string</div>
<div class="line">&nbsp;&nbsp;default: Field Management Zones</div>
<div class="line">&nbsp;&nbsp;inputBinding:</div>
<div class="line">&nbsp;&nbsp;&nbsp;&nbsp;prefix: --title</div>
<div class="line">- id: output</div>
<div class="line">&nbsp;&nbsp;type: string</div>
<div class="line">&nbsp;&nbsp;default: zone_map.png</div>
<div class="line">&nbsp;&nbsp;inputBinding:</div>
<div class="line">&nbsp;&nbsp;&nbsp;&nbsp;prefix: --output</div>
<div class="sp"></div>
<div class="line"><span class="key">outputs</span>:</div>
<div class="line">- id: zone_map_png</div>
<div class="line">&nbsp;&nbsp;type: File</div>
<div class="line">&nbsp;&nbsp;outputBinding:</div>
<div class="line">&nbsp;&nbsp;&nbsp;&nbsp;glob: $(inputs.output)</div>
<div class="sp"></div>
<div class="line"><span class="key">baseCommand</span>:</div>
<div class="line">- python3</div>
<div class="line">- code/plot_zone_map/plot_zone_map.py</div>
</div>
</details>

</div>

</div>
</div>

<!--
notes:
- These two slides are functionally the same exercise (one appears to be a
  disabled/backup version) — treat them as the hands-on working slide.

- Kick off the exercise clearly: "Okay, this is your task. You need to wrap
  plot_zone_map.py into a CWL CommandLineTool, just like we did for the
  previous two scripts. Think about three things: what Docker requirement
  it needs, what its inputs are, and what output it produces."

- Give a starting nudge if the room looks unsure: "If you want a starting
  point, just look at the plain script call — that's Hint 1. From there,
  think about what command you'd give to s4n create."

- While people work (~10 min):
  - Circulate if in person, or monitor chat/breakout rooms if remote.
  - Common sticking points to watch for:
    - Forgetting the --title argument has a space in it (needs quotes)
    - Not realizing they can reuse the same Dockerfile from compute_ndvi
      (Hint 2 addresses this directly)
    - Confusion about multiple inputs — remind them plot_zone_map takes
      FOUR inputs: ndvi, fertility, title, and output — more than the
      previous two tools.

- After ~10 minutes, call time: "Let's regroup. Who wants to share the
  command they used?" — Let a volunteer share their s4n create command
  aloud, then reveal the Hint 2 / Solution box together as a group if
  helpful.

- Reveal the reference CWL file: "Let's open up the reference file and
  compare — does everyone's generated file look roughly like this?" Point
  out the four inputs (ndvi, fertility, title, output) and note that title
  and output are both plain strings, not files — a subtle but important
  distinction from the file-type inputs.

- Close out the exercise: "Great work — you've now built all three
  CommandLineTools for this workflow, in two different languages, entirely
  through the command line, without writing a single line of CWL by hand.
  Next, we'll connect these three tools into one full Workflow file."

Timing: ~12-15 min total (10 min working + 3-5 min regroup/review). This is
the biggest time investment of the session — protect this time and resist
the urge to rush the regroup discussion, since seeing others' solutions
reinforces the pattern before moving to the final integration step.
-->