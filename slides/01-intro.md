---
layout: fairagro
title: Motivation
routeAlias: motivation
---

<div class="fa-bar"></div>

<style>
.encounter-wrap{
  display:flex;
  align-items:center;
  justify-content:center;
  gap:32px;
  margin: 0.25rem 0 0.7rem;
}

.researcher-card{
  display:flex;
  flex-direction:column;
  align-items:center;
  gap:8px;
}

.researcher-card img{
  height:150px;
  width:150px;
  object-fit:contain;
  padding:8px;
  border-radius:50%;
  border:4px solid #ffffff;
  background:#ffffff;
  box-shadow:0 6px 18px rgba(15,152,132,0.18);
  box-sizing:border-box;
}

.researcher-card .name{
  font-size:0.95rem;
  font-weight:700;
  color:#0b6f60;
  letter-spacing:.02em;
}

.researcher-card .role{
  font-size:0.72rem;
  font-weight:600;
  color:#0f9884;
  background:#e9f7f4;
  border:1px solid #a9ded3;
  padding:2px 10px;
  border-radius:20px;
}

.researcher-card .dataset{
  font-size:0.7rem;
  color:#666;
  font-style:italic;
}

.encounter-connector{
  display:flex;
  align-items:center;
  justify-content:center;
  width:44px;
  height:44px;
  border-radius:50%;
  background:linear-gradient(135deg,#0f9884,#0b6f60);
  color:#ffffff;
  font-size:1.3rem;
  font-weight:700;
  box-shadow:0 4px 12px rgba(15,152,132,0.3);
  flex-shrink:0;
  margin-bottom: 30px;
}

.wf-why-box-wrap{
  margin-top:-1.4rem;
}

.wf-why-box-wrap .txt,
.wf-why-box-wrap p.txt {
  font-size: 1.2rem !important;
  line-height: 1.5 !important;
  color:#0f9884;
  font-weight:500;
  margin:0;
  text-align:center;
}
.wf-why-box-wrap .txt b{
  color:#0b6f60 !important;
  font-weight:700;
}

.teaser-line{
  text-align:center;
  font-size:0.95rem;
  color:#5c6067;
  font-style:italic;
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

<div class="encounter-wrap">
  <div class="researcher-card">
    <img src="/researcher1.png" alt="Anna" />
    <span class="name">Anna</span>
    <span class="role">🛰️ Remote Sensing</span>
    <span class="dataset">drone imagery of a wheat field</span>
  </div>

  <div class="encounter-connector">🤝</div>

  <div class="researcher-card">
    <img src="/researcher2.png" alt="Ben" />
    <span class="name">Ben</span>
    <span class="role">🌱 Soil Science</span>
    <span class="dataset">soil samples from the same field</span>
  </div>
</div>

<div class="wf-why-box-wrap">
  <Box label="How It Started">
    <p class="txt">
      Anna and Ben are studying <b>the same field</b> from two different angles.
      They want to <b>combine their data</b> into a single management map, but neither has ever run the other's code and they use different programming languages.
    </p>
  </Box>
</div>

<div class="image-credit">
  Icons by Amethyst Studio, <a href="https://thenounproject.com/creator/AmethystStudio/" target="_blank">The Noun Project</a> — <a href="https://creativecommons.org/licenses/by/3.0/deed.de" target="_blank">CC BY 3.0</a>
</div>

<!--
notes:
- Introduce the running example for the whole day: "Everything we do today
  follows one story, so let me introduce the two people at the center of
  it: Anna and Ben."

- Point at each researcher card in turn: "Anna works in remote sensing —
  she flies drones over a wheat field and collects reflectance imagery. Ben
  is a soil scientist, walking the same field taking physical soil
  samples."

- Point at the handshake connector: "One day they realize something —
  they're studying the exact same field, from two completely different
  angles."

- Read/paraphrase the "How It Started" box: "They want to combine their
  data into a single management map. Sounds simple — except neither of
  them has ever run the other's code, and they work in different
  programming languages entirely."

- Bridge: "This is the problem we're going to solve today, step by step —
  and by the end, Anna and Ben's workflow will be running as one single,
  reproducible pipeline. But first, let's talk about why this is harder
  than it sounds."

Timing: ~1.5 min. Keep this light and story-driven — it's the emotional
hook for the day, not technical content yet.
-->

---
layout: fairagro
title: The analysis script
---

<div class="fa-bar"></div>

<style>
.script-name{
  font-size:1rem;
  font-weight:600;
  margin-bottom:0.35rem;
  color:#0b6f60;
  display:flex;
  align-items:center;
  gap:8px;
}
.script-name .owner-badge{
  font-size:0.7rem;
  font-weight:700;
  color:#0f9884;
  background:#e9f7f4;
  border:1px solid #a9ded3;
  padding:1px 9px;
  border-radius:20px;
}

/* ---- Code block styling to match brand ---- */
.slidev-code, code[lang] {
  border-radius: 10px !important;
  border: 1.5px solid #d7ece8;
  box-shadow: 0 4px 14px rgba(15,152,132,0.08);
  font-size: 1.15rem !important;
  line-height: 1.5 !important;
}

/* ---- Legend cards ---- */
.problem-legend{
  display:flex; gap:10px; flex-wrap:wrap;
}
.problem-item{
  display:flex; align-items:flex-start; gap:7px;
  padding:6px 11px; border-radius:10px;
  background:#fafdfc; border:1.2px solid #e1efec;
  flex:1; min-width:190px;
}
.problem-item .dot{
  flex-shrink:0; width:9px; height:9px; border-radius:50%; margin-top:4px;
}
.problem-item .txt{ font-size:0.78rem; line-height:1.3; color:#333; }
.problem-item .txt b{ font-weight:700; }

.dot.purple{ background:#0f9884; }
.dot.red{ background:#A8C83C; }
.dot.orange{ background:#0b6f60; }

.problem-item.purple.active{ background:#e9f7f4; border-color:#a9ded3; }
.problem-item.purple.active .txt b{ color:#0f9884; }

.problem-item.red.active{ background:#f4f9e3; border-color:#cfe08a; }
.problem-item.red.active .txt b{ color:#7c9425; }

.problem-item.orange.active{ background:#e5f2ef; border-color:#a0cec2; }
.problem-item.orange.active .txt b{ color:#0b6f60; }

/* ---- Discussion (bridge line included inside) ---- */
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
</style>

<div class="script-name">
  🛰️ Anna's script that she sends to Ben
</div>


<code lang="python">

import <span v-mark="{ at: 1, color: '#0f9884', type: 'underline' }">pandas</span> as pd

df = pd.read_csv("<span v-mark="{ at: 2, color: '#A8C83C', type: 'underline' }">/home/anna/projects/wheat_2023/reflectance_final_v2.csv</span>")

df["ndvi"] = (df["nir"] - df["red"]) / (df["nir"] + df["red"])

out = df[["col", "row", "ndvi"]]

out.to_csv("<span v-mark="{ at: 2, color: '#A8C83C', type: 'underline' }">/home/anna/projects/wheat_2023/output/ndvi_results_USE_THIS_ONE.csv</span>", index=False)

</code>


<div class="problem-legend">

<div class="problem-item purple" v-click="1">
  <div class="dot purple"></div>
  <div class="txt"><b>Version drift:</b> no record of which package versions were used</div>
</div>

<div class="problem-item red" v-click="2">
  <div class="dot red"></div>
  <div class="txt"><b>Hard-coded paths:</b> absolute paths tied to one machine</div>
</div>

<div class="problem-item orange" v-click="3">
  <div class="dot red"></div>
  <div class="txt"><b>Cryptic output:</b> "USE_THIS_ONE" — is there a v1? a v3? nobody knows</div>
</div>

</div>

<div class="raise-hand-wrap" v-click="4">
  <Box label="Discussion">
    <p class="txt">
      🙋 Have you ever gotten a script you couldn't understand or rerun?
    </p>
  </Box>
</div>

<!--
notes:
- Show Anna's script and walk through it line by line — don't rush, let each
  issue land before revealing the next annotation.

- Line 1 (import pandas): Ask "Which version of pandas is this? Anna doesn't
  know either — she just has whatever was installed on her laptop months ago."
  → click to reveal "Version drift" — no record of package versions used,
  so Ben can't reproduce the same environment.

- Lines with file paths: Point out the absolute path
  "/home/anna/projects/wheat_2023/...". Ask "What happens when Ben runs this
  on his machine?" → It breaks immediately, because the path only exists on
  Anna's computer.
  → click to reveal "Hard-coded paths."

- Final line ("ndvi_results_USE_THIS_ONE.csv"): This gets a laugh usually —
  ask "Has anyone seen a filename like this before?" Point out that it implies
  there were other versions, v1, v2, maybe a "final_final" — but there's no
  documentation of what changed or why this one is "the one."
  → click to reveal "Cryptic output."

- Summarize: "So Ben got a script that:
   1) he can't guarantee will produce the same result (unknown dependencies),
   2) won't even run on his machine (hard-coded paths),
   3) and even if it runs, he doesn't know if he's using the right output file."

- Pause and open the discussion box: "Show of hands — has this happened to you?
  Either you sent someone a script like this, or you received one?"
  Let a few people share brief examples if time allows (~30 sec).

- Bridge to the rest of the day: "By the end of today, we want to fix exactly
  these three problems. And on top of that — we'll look at how Ben could even
  combine his own R script with Anna's Python script into one reproducible
  workflow."

Timing: ~2–3 min total. Don't linger too long on any one problem — the goal is
to get quick recognition/nods from the audience, not deep technical discussion.
This slide sets up the "pain" that the rest of the session will solve.
-->