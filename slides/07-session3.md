---
layout: fairagro
title: "Session 3: Executing the workflow"
routeAlias: session3
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
  linkStyle default stroke:#385723,stroke-width:2px;
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
</div> <style> </style> <div class="session mt-8"> <div class="session-title">🙌 Hands-On-Session 3 — Execute the Workflow</div> <div class="session-steps"> <div class="step"><span class="step-num">1</span> Create an <code>inputs.yml</code> with inputs for the entire workflow </div> <div class="step"><span class="step-num step-num-highlight">2</span> Execute the workflow locally with SciWIn-Client or SciWIn-Studio</div> </div> </div> 
<style scoped>
 .box {
  border: 1.5px solid #0f9884;
  border-radius: 14px;
  padding: 1.25rem 1.4rem;
  background: linear-gradient(90deg, rgba(15,152,132,0.07) 0%, rgba(168,200,60,0.07) 100%);
  box-shadow: 0 4px 12px rgba(15, 152, 132, 0.08);
  height: 100%;
  transition: transform 0.2s;
}
.box-highlight {
  border-color: #A8C83C;
  background: #a7c83c3d;
  box-shadow: 0 4px 14px rgba(168, 200, 60, 0.25);
}
.box h3 {
  margin-top: 0;
  font-family: monospace;
  font-size: 1.05rem;
  color: #0b6f60;
}
.box ul {
  margin-top: 0.75rem;
  padding-left: 1.1rem;
}
.box li {
  margin-bottom: 0.4rem;
  font-size: 0.85rem;
  line-height: 1.35;
  color: #333;
}
.lang {
  display: inline-block;
  font-size: 0.65rem;
  padding: 0.15rem 0.55rem;
  border-radius: 6px;
  background: #0f9884;
  color: #fff;
  font-weight: 600;
  margin-bottom: 0.5rem;
}
.session {
  border-radius: 14px;
  border: 1.5px solid #0f9884;
  padding: 1.1rem 1.5rem;
  background: linear-gradient(90deg, rgba(15,152,132,0.07) 0%, rgba(168,200,60,0.07) 100%);
  box-shadow: 0 4px 12px rgba(15, 152, 132, 0.08);
}
.session-title {
  font-weight: 700;
  font-size: 1.05rem;
  color: #0b6f60;
  margin-bottom: 0.65rem;
}
.session-steps {
  display: flex;
  flex-direction: column;
  gap: 0.45rem;
}
.step {
  font-size: 0.92rem;
  display: flex;
  align-items: baseline;
  gap: 0.6rem;
  color: #333;
}
.step-num {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 1.5rem;
  height: 1.5rem;
  border-radius: 50%;
  background: #0f9884;
  color: #ffffff;
  font-weight: 700;
  font-size: 0.78rem;
  flex-shrink: 0;
}
.step-num-highlight {
  background: #A8C83C;
  color: #1a1a1a;
}
.step code {
  background: #0f988415;
  padding: 0.15rem 0.4rem;
  border-radius: 5px;
  color: #0b6f60;
  font-weight: 600;
}
 </style>

<!--
notes:
- Bridge from Session 2: "Welcome back for the last stretch. Last session,
  you finished connecting the workflow in SciWIn-Studio — all five edges,
  from raw inputs to the final zone map. This session is about actually
  running it."

- Point at the diagram: "Same workflow picture as before, fully connected
  now — three tools, wired together, ready to execute."

- Walk through the "Hands-On Session 3" box:
  - Step 1: "First, we need to give this workflow actual data to run
    against — that means creating an inputs.yml file."
  - Step 2 (highlighted): "Then, we'll actually execute the whole pipeline
    — either with SciWIn-Client on the command line, or from inside
    SciWIn-Studio directly."

- Bridge: "Let's start with generating that inputs file."

Timing: ~1 min. This is a short orientation slide — the payoff of this
session is seeing the workflow actually run end-to-end, so don't linger
here.
-->

---
layout: fairagro
title: "SciWIn-Client: Create inputs.yml file"
---

<script setup>
const lines1 = [
  {
    type: 'cmd',
    text: 'cd workflows/workflow/'
  },
  {
    type: 'cmd',
    text: 's4n execute make-template workflow.cwl'
  },
  {
    type: 'info',
    text: 'reflectance:\n  class: File\n  location: ../../data/reflectance.csv\nsoil:\n  class: File\n  location: ../../data/soil.csv'
  },
  {
    type: 'cmd',
    text: 's4n execute make-template workflow.cwl > inputs.yml'
  },
]
</script>

<div class="h-100">

<TerminalDemo :lines="lines1" />

</div>

<!--
notes:
- Before running: "cd into the workflow folder, then one command —
  s4n execute make-template workflow.cwl. This inspects the workflow's
  declared inputs and generates a ready-to-fill template for us."

- As the output appears: "It picked up both top-level inputs we defined —
  reflectance and soil — and pre-filled the file paths pointing at our
  actual data. We didn't have to remember the exact input names or types
  ourselves."

- Point at the final command: "Redirect that output into inputs.yml, and
  we now have a real, runnable inputs file for this workflow."

- Bridge: "With that file in hand, we're ready to actually execute the
  workflow."

Timing: ~1 min. Quick, mechanical step — don't over-explain, the value is
obvious once they see the pre-filled paths.
-->

---
layout: fairagro
title: "SciWIn-Client: Execute locally"
---

<script setup>
const lines1 = [
  {
    type: 'cmd',
    text: 's4n execute --engine local workflow.cwl inputs.yml'
  },
  {
    type: 'output',
    text: `Starting execution of step compute_ndvi
Starting execution of step compute_fertility
Executing: Rscript code/compute_fertility/compute_fertility.R --output fertility.csv --soil /tmp/1f879e4a/inputs/soil-stgf8d06d2e/soil.csv
Computed fertility index for 140 grid cells.
Fertility index range: 0.051 - 0.941

Executing: python3 code/compute_ndvi/compute_ndvi.py --output ndvi.csv --reflectance /tmp/fc213ae8/inputs/reflectance-stgd0665402/reflectance.csv
#0 building with "default" instance using docker driver

#1 [internal] load build definition from Dockerfile
#1 transferring dockerfile: 137B 0.0s done
#1 DONE 0.0s

#2 [internal] load metadata for docker.io/library/python:3.12-slim
#2 DONE 0.6s

#3 [internal] load .dockerignore
#3 transferring context: 2B 0.0s done
#3 DONE 0.0s

#4 [1/2] FROM docker.io/library/python:3.12-slim@sha256:78387bc3881b8273120a12ebe6c1ab22b018ccc2c9adf565ae1ac9b536e184ea
#4 resolve docker.io/library/python:3.12-slim@sha256:78387bc3881b8273120a12ebe6c1ab22b018ccc2c9adf565ae1ac9b536e184ea 0.0s done
#4 DONE 0.0s

#5 [2/2] RUN pip install --no-cache-dir pandas==2.2.2 matplotlib==3.9.0 numpy==1.26.4
#5 CACHED

#6 exporting to image
#6 exporting layers done
#6 writing image sha256:2c3ce7708a70468f9582ac40683a7c4582f807c5b72089a321562d17d19b69ce done
#6 naming to docker.io/library/demo:v1.0.0 done
#6 DONE 0.0s
Docker build successful
Computed NDVI for 140 grid cells.
NDVI range: 0.380 - 0.669

Starting execution of step plot_zone_map
Executing: python3 code/plot_zone_map/plot_zone_map.py --fertility /tmp/d58c0d45/inputs/fertility-stg3969610f/fertility.csv --ndvi /tmp/d58c0d45/inputs/ndvi-stg8256c2a5/ndvi.csv --output zone_map.png --title Field Management Zones
#0 building with "default" instance using docker driver

#1 [internal] load build definition from Dockerfile
#1 transferring dockerfile: 137B 0.0s done
#1 DONE 0.0s

#2 [internal] load metadata for docker.io/library/python:3.12-slim
#2 DONE 0.4s

#3 [internal] load .dockerignore
#3 transferring context: 2B 0.0s done
#3 DONE 0.0s

#4 [1/2] FROM docker.io/library/python:3.12-slim@sha256:78387bc3881b8273120a12ebe6c1ab22b018ccc2c9adf565ae1ac9b536e184ea
#4 resolve docker.io/library/python:3.12-slim@sha256:78387bc3881b8273120a12ebe6c1ab22b018ccc2c9adf565ae1ac9b536e184ea done
#4 DONE 0.0s

#5 [2/2] RUN pip install --no-cache-dir pandas==2.2.2 matplotlib==3.9.0 numpy==1.26.4
#5 CACHED

#6 exporting to image
#6 exporting layers done
#6 writing image sha256:2c3ce7708a70468f9582ac40683a7c4582f807c5b72089a321562d17d19b69ce done
#6 naming to docker.io/library/demo_python:latest done
#6 DONE 0.0s
Docker build successful
Saved plot to zone_map.png
zone
0    32
1    38
2    38
3    32

{
  "zone_map_png": {
    "class": "File",
    "location": "file:///home/user/demo/workflows/workflow/zone_map.png",
    "path": "/home/user/demo/workflows/workflow/zone_map.png",
    "basename": "zone_map.png",
    "dirname": "/home/user/demo/workflows/workflow",
    "nameroot": "zone_map",
    "nameext": ".png",
    "checksum": "sha1$73492e39b3dffcb1aeb3a10a1e5dc4c5de1d5faf",
    "size": 97273
  }
}`
  },
]
</script>

<div class="h-100">

<TerminalDemo :lines="lines1" />

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
- Before running: "One command runs the entire pipeline —
  s4n execute --engine local workflow.cwl inputs.yml. That's it. No
  manual steps, no copying files between tools by hand."

- As the log scrolls, narrate the shape of it rather than every line:
  "Watch the step names as they start — compute_ndvi and compute_fertility
  kick off, each building its own Docker image on the fly and running
  inside it. This is the portability payoff: neither of us needed Python
  or R installed locally, SciWIn handled the whole environment."

- Point out the two computed results mid-log: "There's Ben's fertility
  index and Anna's NDVI range, computed exactly like in our live-coding
  demos — except now it's happening automatically, as part of one
  pipeline, in the right order."

- Point at plot_zone_map starting only after both previous steps finish:
  "Notice plot_zone_map doesn't start until both compute_ndvi and
  compute_fertility are done — SciWIn worked out that dependency for us
  from the workflow file, we never told it to wait."

- Point at the final JSON block: "And this is the payoff — a structured,
  traceable record of the final output: zone_map_png, its exact file
  location, and a checksum. That checksum means anyone can verify they got
  byte-for-byte the same result."

- Land the moment: "This is Anna and Ben's original problem, solved —
  two scripts, two languages, zero manual file-copying, running as one
  reproducible pipeline with a single command."

- Bridge: "Let's step back and talk about what made this possible, and how
  to carry these habits into your own work."

Timing: ~2-2.5 min. Let the log scroll and breathe a little — this is the
technical climax of the whole workshop, so let the audience actually watch
it happen rather than narrating over every single line.
-->


---
layout: fairagro
title: "SciWIn-Studio: Select inputs.yml"
---

<img src="/select_input.png" class="h-100 w-full object-contain mx-auto" />


---
layout: fairagro
title: "SciWIn-Studio: Start workflow execution"
---

<img src="/start_wf.png" class="h-100 w-full object-contain mx-auto" />


---
layout: fairagro
title: "SciWIn-Studio: Run workflow"
---

<img src="/run_wf.png" class="h-100 w-full object-contain mx-auto" />



---
layout: fairagro
title: "Execute a workflow in SciWIn-Studio"
disabled: true
---

<div class="fa-bar"></div>

<div class="studio-tour">

  <div class="studio-gif-wrap">
    <img src="/run_workflow.gif" alt="Creating and connecting a CWL workflow visually in SciWIn-Studio" class="studio-gif" />
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

