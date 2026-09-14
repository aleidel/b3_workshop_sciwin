---
layout: fairagro
title: Workflows
routeAlias: workflows
---

<div class="fa-bar"></div>

<style>
.wf-why-box{
  margin-top:1.5rem;
  border-radius:14px;
  padding:14px 16px 14px;
  background:linear-gradient(180deg,#f2fbf9 0%,#e6f7f3 100%);
  border:1px solid #cdeee6;
  box-shadow:0 2px 10px rgba(15,152,132,0.08);
  width:100%;
  box-sizing:border-box;
}
.wf-why-outer{
  border:1.5px dashed #7fd0bf;
  border-radius:12px;
  padding:16px 16px 12px;
  background:#ffffff;
  position:relative;
}
.wf-why-label{
  position:absolute; top:-9px; left:12px;
  background:#ffffff; padding:0 6px;
  font-size:0.68rem; font-weight:700; color:#0f9884;
  text-transform:uppercase; letter-spacing:.03em;
}
.wf-why-list{
  margin:0; padding-left:1.3em; list-style-type:none;
}
.wf-why-list li{
  position:relative;
  line-height:1.6;
  margin-bottom:0.4em;
  padding-left:0.4em;
}

.wf-why-list li strong{ color:#0f9884; }

.wf-punchline{
  margin-top:1.2rem;
  display:flex; align-items:center; justify-content:center; gap:10px;
  padding:10px 14px;
  border-radius:12px;
  background:#F8CBAD;
  border:1.5px solid #823909;
  box-shadow:0 2px 8px #F8CBAD;
  font-size:1rem;
  color:#F8CBAD;
}
.wf-punchline b{ color:#F8CBAD; }

.raise-hand-wrap { margin-top: 0.5rem; }

.raise-hand-wrap .txt,
.raise-hand-wrap p.txt {
  font-size: 0.95rem !important;
  line-height: 1.3 !important;
  color: #0b6f60;
  font-weight: 600;
  margin: 0;
  text-align: center;
}

.raise-hand-wrap .bridge-txt{
  font-size: 0.8rem !important;
  font-weight: 500 !important;
  font-style: italic;
  color: #5c6067 !important;
}
.raise-hand-wrap .bridge-txt b{ color:#0f9884; font-style:normal; font-weight:700; }

.wf-question-corner{
  position:absolute;
  bottom:34px;
  left:calc(40% + 2rem);
  z-index:50;
  text-align:center;
  pointer-events:none;
}
.wf-question-corner pre{
  color:#0f9884;
  margin:0;
  font-family: "Fira Sans", sans-serif;
  font-size:0.95rem;
  white-space:normal;
}


</style>

<div class="flex gap-8 items-start">

<div style="flex:0 0 40%;">

<p>Describes a <b>set of steps</b> that is executed<span v-click="1">, their <b>inputs and outputs</b></span><span v-click="2">, and the <b>relationships</b> between them</span></p>

<Box
  label="Why Use a Workflow?"
  :start-click="3"
  :items="[
    { strong: 'Clarity:', text: 'Visualize structure and data flow' },
    { strong: 'Automation:', text: 'Save time on repetitive, recurring tasks' },
    { strong: 'Collaboration:', text: 'Reuse, extend, or swap components built by colleagues' },
    { strong: 'Flexibility:', text: 'Combine Python, R, Bash, etc. in a single pipeline' },
  ]"
/>




</div>


<div style="flex:1; position:relative; min-height:480px;">

<div v-click.hide="1" class="absolute inset-0">


<div class="w-full max-w-[100%] mx-auto">


```mermaid
---
config:
  theme: base
  look: neo
  themeVariables:
    primaryColor: '#C5E0B4'
    primaryTextColor: '#1c1a1a'
    secondaryColor: '#ffff'
    lineColor: '#385723'
    fontSize: 12px
    tertiaryTextColor: '#ffff'
    fontFamily: 'Fira Sans, trebuchet ms, verdana, arial'
---
flowchart TB
  linkStyle default stroke:#FFFFFF,stroke-width: 2px;
  subgraph inputs[Workflow Inputs]
    direction TB
    reflectance(reflectance)
    soil(soil)
  end
  subgraph outputs[Workflow Outputs]
    direction TB
    zone_map_png(zone_map_png)
  end
    compute_ndvi(compute_ndvi)
  reflectance --> |reflectance|compute_ndvi
    compute_ndvi_output(ndvi.csv)
  compute_ndvi_output --> |output|compute_ndvi
    compute_fertility(compute_fertility)
  soil --> |soil|compute_fertility
    compute_fertility_output(fertility.csv)
  compute_fertility_output --> |output|compute_fertility
    plot_zone_map(plot_zone_map)
  compute_ndvi --> |ndvi|plot_zone_map
  compute_fertility --> |fertility|plot_zone_map
    plot_zone_map_title(Field Management Zones)
  plot_zone_map_title --> |title|plot_zone_map
    plot_zone_map_output(zone_map.png)
  plot_zone_map_output --> |output|plot_zone_map
  plot_zone_map --> |zone_map_png|zone_map_png
  style inputs fill:#FFFFFF,stroke-width:2px;
  style reflectance stroke:#ffff,fill:#ffff,stroke-width:2px;
  style soil stroke:#ffff,fill:#FFFFFF,stroke-width:2px;
  style outputs fill:#FFFFFF,stroke-width:2px;
  style zone_map_png stroke:#FFFFFF,fill:#FFFFFF,stroke-width:2px;
  style compute_ndvi stroke:#385723,stroke-width:2px;
  style compute_ndvi_output font-size:9px,fill:#FFFFFF, stroke:#FFFFFF,stroke-width:2px;
  style compute_fertility stroke:#385723,stroke-width:2px;
  style compute_fertility_output font-size:9px,fill:#FFFFFF, stroke:#FFFFFF,stroke-width:2px;
  style plot_zone_map stroke:#385723,stroke-width:2px;
  style plot_zone_map_title font-size:9px,fill:#FFFFFF, stroke:#FFFFFF,stroke-width:2px;
  style plot_zone_map_output font-size:9px,fill:#FFFFFF, stroke:#FFFFFF,stroke-width:2px;
```

</div>

</div>

<div v-click="[1, 2]" class="absolute inset-0">


<div class="w-full max-w-[100%] mx-auto">

```mermaid
---
config:
  theme: base
  look: neo
  themeVariables:
    primaryColor: '#C5E0B4'
    primaryTextColor: '#231f20'
    secondaryColor: '#FFFF'
    lineColor: '#385723'
    fontSize: 12px
    tertiaryTextColor: '#231f20'
    fontFamily: 'Fira Sans, trebuchet ms, verdana, arial'
---
flowchart TB
  linkStyle default stroke:#ffff,stroke-width: 2px;
  subgraph inputs[Workflow Inputs]
    direction TB
    reflectance(reflectance)
    soil(soil)
  end
  subgraph outputs[Workflow Outputs]
    direction TB
    zone_map_png(zone_map_png)
  end
    compute_ndvi(compute_ndvi)
  reflectance --> |reflectance|compute_ndvi
    compute_ndvi_output(ndvi.csv)
  compute_ndvi_output --> |output|compute_ndvi
    compute_fertility(compute_fertility)
  soil --> |soil|compute_fertility
    compute_fertility_output(fertility.csv)
  compute_fertility_output --> |output|compute_fertility
    plot_zone_map(plot_zone_map)
  compute_ndvi --> |ndvi|plot_zone_map
  compute_fertility --> |fertility|plot_zone_map
    plot_zone_map_title(Field Management Zones)
  plot_zone_map_title --> |title|plot_zone_map
    plot_zone_map_output(zone_map.png)
  plot_zone_map_output --> |output|plot_zone_map
  plot_zone_map --> |zone_map_png|zone_map_png
  style inputs fill:#EEEEEE,stroke-width:2px;
  style reflectance stroke:#0f9884,fill:#6FC1B5,stroke-width:2px;
  style soil stroke:#0f9884,fill:#6FC1B5,stroke-width:2px;
  style outputs fill:#EEEEEE,stroke-width:2px;
  style zone_map_png stroke:#823909,fill:#F8CBAD,stroke-width:2px;
  style compute_ndvi stroke:#385723,stroke-width:2px;
  style compute_ndvi_output font-size:9px,fill:#cfeae6, stroke:#9FD6CE,stroke-width:2px;
  style compute_fertility stroke:#385723,stroke-width:2px;
  style compute_fertility_output font-size:9px,fill:#cfeae6, stroke:#9FD6CE,stroke-width:2px;
  style plot_zone_map stroke:#385723,stroke-width:2px;
  style plot_zone_map_title font-size:9px,fill:#cfeae6, stroke:#9FD6CE,stroke-width:2px;
  style plot_zone_map_output font-size:9px,fill:#cfeae6, stroke:#9FD6CE,stroke-width:2px;
```



</div>

</div>
<div v-click="2" class="absolute inset-0">


<div class="w-full max-w-[100%] mx-auto">

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
    fontSize: 12px
    tertiaryTextColor: '#231f20'
    fontFamily: 'Fira Sans, trebuchet ms, verdana, arial'
---
flowchart TB
  linkStyle default stroke:#385723,stroke-width: 2px;
  subgraph inputs[Workflow Inputs]
    direction TB
    reflectance(reflectance)
    soil(soil)
  end
  subgraph outputs[Workflow Outputs]
    direction TB
    zone_map_png(zone_map_png)
  end
    compute_ndvi(compute_ndvi)
  reflectance --> |reflectance|compute_ndvi
    compute_ndvi_output(ndvi.csv)
  compute_ndvi_output --> |output|compute_ndvi
    compute_fertility(compute_fertility)
  soil --> |soil|compute_fertility
    compute_fertility_output(fertility.csv)
  compute_fertility_output --> |output|compute_fertility
    plot_zone_map(plot_zone_map)
  compute_ndvi --> |ndvi|plot_zone_map
  compute_fertility --> |fertility|plot_zone_map
    plot_zone_map_title(Field Management Zones)
  plot_zone_map_title --> |title|plot_zone_map
    plot_zone_map_output(zone_map.png)
  plot_zone_map_output --> |output|plot_zone_map
  plot_zone_map --> |zone_map_png|zone_map_png
  style inputs fill:#EEEEEE,stroke-width:2px;
  style reflectance stroke:#0f9884,fill:#6FC1B5,stroke-width:2px;
  style soil stroke:#0f9884,fill:#6FC1B5,stroke-width:2px;
  style outputs fill:#EEEEEE,stroke-width:2px;
  style zone_map_png stroke:#823909,fill:#F8CBAD,stroke-width:2px;
  style compute_ndvi stroke:#385723,stroke-width:2px;
  style compute_ndvi_output font-size:9px,fill:#cfeae6, stroke:#9FD6CE,stroke-width:2px;
  style compute_fertility stroke:#385723,stroke-width:2px;
  style compute_fertility_output font-size:9px,fill:#cfeae6, stroke:#9FD6CE,stroke-width:2px;
  style plot_zone_map stroke:#385723,stroke-width:2px;
  style plot_zone_map_title font-size:9px,fill:#cfeae6, stroke:#9FD6CE,stroke-width:2px;
  style plot_zone_map_output font-size:9px,fill:#cfeae6, stroke:#9FD6CE,stroke-width:2px;
```
</div> </div> </div> </div> <div class="wf-question-corner" v-click="8"> <pre>🙋 <b>Has anyone ever used workflow tools?</b></pre> </div> 

<!--
notes:
- Start with the definition on screen: "A workflow describes a set of steps
  that is executed." Point to the diagram on the right — at this point it's
  shown in plain grey/white, just the boxes and arrows, no data flow
  highlighted yet. Say: "Think of it as a blueprint — here we have three
  steps: compute_ndvi, compute_fertility, and plot_zone_map."

- [Click 1] The text updates to add "...their inputs and outputs." At the same
  time, the diagram highlights the input nodes (reflectance, soil) in teal and
  the output node (zone_map_png) in orange.
  → Say: "Every workflow step needs something to consume and something to
  produce. Here, reflectance and soil data go in, and a zone map image comes
  out at the end."

- [Click 2] The text adds "...and the relationships between them." The diagram
  now colors in the connecting arrows (green), showing the full data flow.
  → Say: "But a workflow isn't just a list of steps — it's the connections
  between them. Notice how compute_ndvi's output feeds into plot_zone_map,
  and so does compute_fertility's output. This is exactly the kind of
  combination Anna and Ben need — Anna's NDVI step and Ben's fertility step
  feeding into one shared visualization, even though they were written
  separately, possibly in different languages."

- Pause briefly here to let the diagram sink in — this is the "aha" visual
  that ties back to Anna & Ben's story from the motivation slide.

- [Click 3 onward] Transition to the "Why Use a Workflow?" box. The four
  benefits appear one at a time — pace yourself to one per short beat:
  - "Clarity" → visualize structure and data flow (point back at the diagram
    as a live example of this benefit)
  - "Automation" → no more manually re-running scripts in the right order
  - "Collaboration" → reuse or swap out someone else's step, like plugging in
    Ben's R script next to Anna's Python script
  - "Flexibility" → mix Python, R, Bash, etc. in the same pipeline — directly
    solves the "different programming languages" problem from the motivation
    slide

- [Click 8] Deliver the punchline with a bit of humor/timing: "🤯 But there
  are over 300 workflow tools..." Let that land — pause for a laugh or groan.
  → Bridge line: "So the good news is: workflows solve our problem. The bad
  news is now we have a new problem — which one do we pick? That's exactly
  what we'll look at next."

Timing: ~3 min total. The diagram animation is doing a lot of the explaining
visually, so don't over-narrate each color change — just narrate the *meaning*
behind each transition and let it reinforce the definition being built up in
the text on the left.
-->