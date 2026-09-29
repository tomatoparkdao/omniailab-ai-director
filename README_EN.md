<div align="right">

[简体中文](README.md) ｜ **English**

</div>

# OmniAiLab AI Film & TV Director

> © OmniAiLab ｜ Developer: Mochiball ｜ Platform: [omniailabx.com](https://www.omniailabx.com/)

**A film-industry-grade, end-to-end AI director Skill.** Hand it a locked script and it walks you from script breakdown all the way to a finished film, following real production standards. **Works for both live-action realism and animation**, from a 30-second short to a feature with a hundred-plus scenes.

| Item | Value |
|---|---|
| Skill invocation name (unique ID) | `omniailab-ai-director` |
| Display name | OmniAiLab AI Film & TV Director |
| Version | v2.0.30 |
| Publisher / Developer | OmniAiLab / Mochiball |
| License | MIT (see [LICENSE](LICENSE)) |
| Companion manual | [Feishu doc](https://zcn03zgas1zl.feishu.cn/wiki/P2fhwADXvil24UkNkDCcw1x2nbA) (Chinese) |
| Open-source repo (public) | [github.com/tomatoparkdao/omniailab-ai-director](https://github.com/tomatoparkdao/omniailab-ai-director) |

The invocation name is **all-lowercase with hyphens** (`omniailab-ai-director`) — it is not the display name. Tools with native Skill support work best with the invocation name; tools without it will still trigger on a natural-language description (implicit invocation is allowed).

---

## In one sentence

Hand it a locked script and it takes you from script breakdown to finished film following film-industry standards. At the end of every stage you only need to reply "confirm" or "change this part."

- **Scope · any medium** — live-action photoreal pipelines, plus pure animation / 2D cartoon / 3D game-engine render style / 3D + hand-painted hybrid.
- **Scope · any length** — 30-second shorts, single-episode short dramas, brand films, narrative music-video segments, all the way up to features with dozens or hundreds of scenes, tens of minutes to two hours-plus (**features no longer need to be split into episodes**).
- **Default medium** — live-action photoreal (used when unspecified). For animation / hybrid projects, P1 first performs a **medium determination** and writes it into the "whole-film style lock"; from then on that declaration is the single source of truth for medium — modeling, brushwork, motion and lighting follow the **Animation & Hybrid Medium layer**, and motion obeys **animation principles** (squash & stretch / anticipation / follow-through & overlap / arcs / exaggeration), with physical accuracy yielding to expressive motion.

---

## Quick start

### 1. Where to install it

Copy the **entire `omniailab-ai-director` folder** (including `SKILL.md`, `VERSION`, `openai.yaml`, `references/`, `examples/`) into the matching directory below, then start a new session.

| Tool | Where to put it | How to invoke |
|---|---|---|
| **Codex** (recommended) | No native skill directory: drop the folder into your project, e.g. `<your project>/skills/omniailab-ai-director/`, then add one line to `AGENTS.md` in the project root:<br>`For film production tasks: first read skills/omniailab-ai-director/SKILL.md and follow its workflow.` | Say "start making the film per SKILL.md". |
| **Claude / Claude Code** | Personal: `~/.claude/skills/omniailab-ai-director/`<br><br>Project: `<your project>/.claude/skills/omniailab-ai-director/` | Type **`/omniailab-ai-director`**, or describe the task (e.g. "run the full film pipeline for this script"). |
| **WorkBuddy** | User level (global): `~/.workbuddy/skills/omniailab-ai-director/`<br><br>Project level: `<your project>/.workbuddy/skills/omniailab-ai-director/` | It appears in the skill list in a new session; just say **`$omniailab-ai-director 开始`**. |

> **Copy the whole folder — never just `SKILL.md`.** The four sub-skills (ACTING / EMOTION / LIRA / CINEDANCE), all specialized layers (COMBAT combat / BLOCKING blocking / AESTHETICS / PROMPT-DOCTRINE / ASSET-SYSTEM / SCENE-ENGINE / OPTICS / FEATURE-PRODUCTION / MUSIC-SCENE / ANIMATION / DOCUMENTARY / PROMO / ONBOARDING), the visual-language library, the 7 ready-made prompt sets, the documentary templates, **all 14 promo directions in full detail**, **7 real promo samples** and **49 case-study figures** all live in `references/` and `examples/`. Skip one directory at runtime and the chain breaks.

**Install by cloning (recommended)**

```bash
git clone https://github.com/tomatoparkdao/omniailab-ai-director.git \
  ~/.workbuddy/skills/omniailab-ai-director
```

The repository is **public** and always tracks the latest skill version; update later with `git pull` in that folder. Issues are welcome in the repo.

### 2. Where the script comes from (pick one)

1. **You upload a locked script** — it reads it and enters P0 directly.
2. **You give nothing and just say "start"** — it first asks one question: "do you have a script, or just a one-line idea?" It will **not** auto-load the built-in script. Say "run the default project" only if you want to see the sample *Floor 17* (a 30-second suspense short).
3. **You give a one-line idea or title** (e.g. "make a space thriller short") — it first writes a locked script for you to confirm, then enters P0. Script length is kept to 30 seconds – 5 minutes.

### 3. Start command

Just say "start" — instead of asking "what is your script?", it asks "do you have a script, or just a one-line idea?". It will **not** run the built-in script by default; say "run the default project" or "do Floor 17" to use the sample.

### 4. Two things to settle before you start

- **The story must be locked.** It only works with a locked script: no rewriting the story, adding characters, adding dialogue or changing the ending. Major mid-course story changes (especially adding/removing characters or scenes) invalidate every asset already generated.
- **Decide delivery specs first.** Defaults are 1080p / 16:9 / 24fps / MP4. If you need vertical or square (mobile, product packaging art, etc.), say so at P1 — changing specs after P1 also causes asset rework.

### 5. You only ever reply two ways

1. **"confirm / pass / locked / continue"** — releases the next stage. Anything else does not open the gate.
2. **"change item X to …"** — it stays in the current stage and redoes it in place.

**Want only one capability?** Name it directly; the full pipeline is optional:

| What you want | Just say |
|---|---|
| Image prompts | "image only — give me the prompt for this shot" |
| Video prompts | "video prompt only — how do I shoot this shot" |
| Performance design | "performance only — how should this character play this scene" |
| Emotion control | "emotion only — how do I play this crying scene" |
| Look selection | "give me the look menu" / "use D01 + C04 + R01 + S2" |
| Aesthetic recommendation | "which film aesthetic fits this scene" |
| Fight choreography | "how should this fight go — give me a high-energy fight prompt" |
| Blocking / staging | "how should these people stand" / "the positions shifted again in the next shot" |

> **The more specific the request, the less rework.** Three things matter most: ① the full locked script; ② delivery specs (aspect ratio, resolution, frame rate, duration); ③ hard constraints (what must not appear, what must appear). Give these up front and you save far more than patching later.

---

## Pipeline overview

Eight stages form one **serial chain**: **P0 → P0A → P1 → P2 characters → P2 props → P3 → P4 → P5 → P6**. Every link ends with a **confirmation gate** — until you explicitly say "confirm / pass / locked / continue", it stays locked in place.

| Stage | What it does | What you get |
|---|---|---|
| **P0 + P0A** | Receive script + ten-item breakdown + whole-film emotion curve | Project intake summary, ten-item breakdown, one 16:9 black-background emotion curve |
| **P1** | Lock whole-film cinematography, environment colour strategy, sound bible; proactively propose 2–3 aesthetic recipes | The "whole-film style lock" text — the fixed prefix for every downstream prompt |
| **P2 characters** | Character/state master-plate production list → dependency-batched 9:16 character plates → batch 16:9 character sheets | Character master plates, character sheets, performance master files |
| **P2 props** | Key-prop list → 3:4 single-item product archive shots | Prop master plates |
| **P3** | Scene list → 16:9 empty-scene master plates → 5-colour environment palettes | Scene master plates, environment palettes (with HEX), spatial direction chain |
| **P4** | Shot breakdown → full shot list → blocking baseline → 16:9 first frames for every shot | Shot list, blocking data, all first frames, per-shot performance passages |
| **P5** | Performance passage + emotion layer + spatial data → final video prompts and parameter table | Per-shot video prompts, OmniAiLab parameter table |
| **P6** | Batch generation on the OmniAiLab canvas, voice, BGM, edit, export | Finished MP4, all assets, QC report |

> **Gates are hard rules.** P0 and P0A must run in the same turn — P0 is never confirmed separately. From P0A onward, each stage ends with fixed wording and only "confirm" unlocks the next step. To change something, stop and change it in place, then confirm — **do not try to make it finish several stages in one sentence.**

---

## Stage-by-stage details

### P0 + P0A | Project intake and script breakdown

Reads the whole script, outputs the P0 intake summary, and in the **same reply** completes the first 9 items of P0A (country/era, world rules, character bios, spatial chain, state chain, etc.). It then computes emotion nodes and generates item 10 — the 16:9 black-background emotion curve.

**What you do:** almost nothing; wait for it to deliver in one go. Check two things — the curve's **node count** and its **breathing zone**.

**Deliverables:** intake summary + ten-item breakdown + whole-film emotion curve.

**Its confirmation wording:**

> [Please confirm] Do you confirm the above P0A script breakdown and creative baseline (including the whole-film emotion curve)? Point out any specific items to change.
> [Next step after confirmation] Establish the P1 whole-film cinematography, environment colour strategy and sound bible.

**Pitfalls**

- Don't wait for P0 to be confirmed separately — **it won't be**; it continues straight into P0A.
- The emotion curve should have **8–14 nodes (max 16)** and at least **one genuine breathing zone**. If you see "high energy throughout with no low point" or "a release point appearing out of nowhere", send it back.
- The emotion curve is not decoration — P6's BGM in/out points and P4's rhythm checks depend on it. Get it wrong and everything downstream skews.

### P1 | Creative baseline (the single most important confirmation)

After judging the script's genre, it **proactively proposes 2–3 aesthetic recipe candidates** (ID + name + why it fits + suggested placement + trade-off). Once you pick, it delivers one complete recommendation — one primary film reference (at most one supplementary), capture medium and lens family, aspect ratio and frame rate, light sources and materials, environment colour strategy, whole-film ambience principles and music bible.

**What you do:** choose one as the primary aesthetic and at most one supplementary, or just say "no need" and it falls back to standard sourcing. Then confirm the style-lock text.

**Deliverables:** the "whole-film style lock" text — **every downstream image and video prompt must carry it verbatim at the start.**

**Its confirmation wording:**

> [Please confirm] Do you confirm the above P1 cinematography, environment colour strategy and sound bible? Point out changes directly.
> [Next step after confirmation] First list the 9:16 character/state master-plate production list; confirm scope and dependency batches before generating.

**Pitfalls**

- **No images and no audio are generated at this stage** — no palette chart, no audio files, no BGM. If you expect images here, you are at the wrong stage.
- The style lock, once confirmed, is a **frozen** fixed prefix and **cannot be changed afterwards**. Changing it means going back to P1, which reworks every downstream asset. Treat it as the one confirmation to read carefully.
- "No need" is a legitimate option. If the script has no recipe-grade need, it says so explicitly — don't force an aesthetic.
- **Settle "the hard things" at plate time.** Lens character (anamorphic-type optics), night-scene darkness, and in-frame printed text must all be solved at the **scene plate / first frame** stage and frozen into the style lock. Chasing them later in video prompts only makes the model drift shot to shot.
- **Colour is tuned in the prompt, not in post.** The whole-film style prefix is **pasted shot by shot**; it carries the palette, exposure and contrast, grain, and camera-movement character. The criterion for choosing a film/print stock is "**which colour the shadows lean toward**" — pick the one leaning toward the film's dominant colour, not the "more expensive" one. Models warm up cool footage, and the root cause is usually a warm source in the reference image (which gets amplified); **writing "no yellow" does not work at all** — use a positive "colour constitution sentence." For a light source you cannot crop out of the reference, write "**it is switched off in this film**."
- **Animation / hybrid projects must do a "medium determination" first.** P1 must determine the medium (photoreal / stylised 3D / 2D / hybrid) and write it into the style lock; that declaration becomes the only medium reference. Also lock the **whole-film lighting formula** (animation line = golden-hour side-backlight + long shadows) and the **style split** (moving objects get clean solid volume; heavy brushwork is reserved for the environment). Generate without a medium determination and every downstream asset gets reworked.

### P2 character assets

First a 9:16 character/state master-plate production list (asset type, upstream dependencies, suggested batch, necessity, reason to generate). After you confirm scope, **batch 1 covers only dependency-free or base characters**; once base characters are locked, blood relatives, variants, costume changes, injuries and age states follow. After everything is confirmed, it generates 16:9 character sheets for all confirmed characters in one pass, and builds a performance master file per main character.

**What you do:** confirm or edit the list; review every batch's images carefully.

**Deliverables:** 9:16 character master plates, 16:9 character sheets, performance master files.

**Its confirmation wording:**

> [Please confirm] Are the above character assets all locked? Point out specific characters and locations to change.
> [Next step after confirmation] Extract the key-prop list and generate key-prop master plates.

**Pitfalls**

- Character sheets are **not a separate item and do not get a second list** — they are generated in one pass only after all 9:16 characters are confirmed. Don't push for a standalone sheet.
- **Don't skip batches.** If an upstream (e.g. a parent character) is unconfirmed and you write downstream "blood relative" prompts, changing upstream wastes all of it.
- Character consistency is inherited downstream from **genuinely confirmed images**, so every batch must be reviewed carefully — approve one wrong image and everything after is wrong.

### P2 key props

First a **non-batched** table of final prop candidates (plot function, identity/continuity anchor, necessity, reason to generate). After you confirm or edit, it generates 3:4 portrait single-item product archive shots. No three-view sheets, no people or hands in frame.

**What you do:** confirm the prop list; review each master plate.

**Deliverables:** prop master plates (each with its prompt).

**Pitfalls**

- Props **have no batch concept** (unlike characters), but the list must be confirmed before generating — don't let it start drawing.
- A prop image should read as a "product archive shot" — clean, single item, identifiable detail. Images containing people or hands cannot serve as prop master plates.

### P3 scene assets

Extracts scenes from the script's spatial chain and outputs a production list (scene name, plot function, lighting state, interaction points, necessity). After you confirm, it generates a 16:9 **empty-scene master plate (no people)** for each required scene, with different lighting states in the same space generated separately. After all are confirmed, it extracts a 5-colour environment palette per main scene (dominant / shadow / midtone / light-source colour / accent, labelled with HEX) and outputs the spatial direction chain and scene-character-prop interaction points.

**What you do:** confirm the scene list; review each plate and palette.

**Deliverables:** scene master plates, 5-colour environment palettes (with HEX), spatial direction chain.

**Pitfalls**

- Empty-scene master plates **must contain no people** — that is the basis for overlaying blocking and first frames later.
- Different lighting states in the same space **need separate images** (day / night / rain). Don't expect one image to cover everything.
- Palettes must be **labelled with HEX**, otherwise they cannot be referenced later and the work is wasted.

### P4 | Shot design and first-frame generation

Breaks shots by dramatic beat (6–10 shots for a 30-second short; 15–30 shots for 1–3 minutes), outputs a full shot list (shot number, duration, shot size, angle, camera move, frame content, characters/props, scene, sound, emotional intensity). **Multi-person or multi-object shots first establish a "blocking baseline"**, then each shot takes values from it. It generates a 16:9 first frame per shot and rewrites character master files into per-shot performance passages with emotion propositions and beats.

**What you do:** confirm the shot list and **all** first frames.

**Deliverables:** shot list, blocking data, all first frames, per-shot performance passages, emotion beats.

**Its confirmation wording:**

> [Please confirm] Are the above shot list and all first frames locked? Point out specific shot numbers to change.
> [Next step after confirmation] Enter P5 and generate video prompts and OmniAiLab parameters for each shot.

**Pitfalls (this stage has the most)**

- **Blocking is the biggest failure area.** One scene must first have a "blocking baseline"; every later shot reads from it and **only changes the fields that genuinely changed**, with unchanged characters inherited and frozen. **Without evidence of a coordinate change, no character's position, facing or pose may be altered.** This is the cure for "last shot on the left, next shot runs right" — if you see drift again, just say "check blocking, run the cross-shot continuity protocol."
- **Fight shots must fill in a "shot contract" first** (narrative purpose → shot size → camera position / observation axis → A/B frame positions → primary camera move → trigger point → end point → hand-off state), then fix A/B sides and three spatial anchors, and only then choreograph the action. Don't just write "the two start fighting."
- First-frame prompts **must carry the P1 style prefix**; upload references by priority: **confirmed character plates > scene master plates > prop master plates** (max 6 images per node).
- If the frame contains **Chinese text** (signage, street signs, packaging, on-screen text) or the output is a full storyboard board, switch image generation to **image2.5** — otherwise Chinese glyphs and layout break.
- **The first frame is the final exposure and optics.** Its exposure determines every later shot's exposure, so don't plan to darken in the video stage. Keep **sky out of the composition** (any sky reliably drifts toward blue hour); frame windows so the opposite wall fills them. In-frame text is also finalised here. Also: **every asset used in this shot must already be named and locked** — any "tweak the wording on the fly" breaks consistency.

### P5 | Video prompts and OmniAiLab parameters

Every shot has **two mandatory upfront layers** — ① use ACTING to rewrite the character master file into a "performance passage for this shot" (objective, obstacle, tactic, beats, listening, subtext, body and voice); ② use EMOTION to write the "emotion proposition + emotion beats + eye-line landing points + voice envelope" and complete character permission isolation and visual vocabulary purification. **Only when both layers are ready**, together with this shot's blocking / camera coordinates, reference tags and storyboard requirements, does CINEDANCE compose the final video prompt. It then outputs the parameter table.

**What you do:** confirm all video prompts and the parameter table.

**Deliverables:** per-shot video prompts + parameter table (shot number, model, duration, ratio, input method, reference list).

**Its confirmation wording:**

> [Please confirm] Do you confirm all the above video prompts and OmniAiLab parameters? Point out specific shot numbers to change.
> [Next step after confirmation] Enter P6 to batch-generate video in the OmniAiLab canvas, produce audio, and edit and export the film.

**Pitfalls**

- **Never skip ACTING and EMOTION and write video prompts directly**, and never bolt emotion on afterwards as a "supplement". This is the hard prerequisite this Skill stresses repeatedly — skipping it means giving up performance and emotion control.
- **Image-to-video is mandatory**; direct text-to-video is forbidden (except pure black or text-only shots). Generate a first frame per shot first, then the video.
- Model selection: character shots → **Seedance 2.5**; VFX / transformation → **Kling O3**; prop close-ups → **Vidu**; fallback / trial → **Wan 2.6 / Seedance 2.0 Fast**.
- Aspect ratio, resolution, duration and model name all belong in the platform UI — **never in the prompt text**.
- Fight shots need a complete **action chain** (attack intent → body and weapon motion → opponent response → contact feedback → displacement result → environmental aftermath): paired attack/defence, closed physical loop, no crossing the axis, one primary camera move per phase, and **no ending on a posed freeze**.
- **Write prompts in the fixed block order and self-check against the eleven iron rules.** Block order (16 blocks): scene context → enabled references → whole-film locks → location map (GEO spatial map) → **eye-line and gaze** → first-frame state and spatial occupancy → format mode → lens (optics) → camera → action timing → performance task → physics → lighting → **sound and dialogue** → style and image quality → **positive lock**. **Dialogue goes only in the "sound and dialogue" block; the action block must contain not a single word of dialogue.** Iron rules in brief: say what is there, not what isn't; bind geometry to the frame, not to objects; one reaction per beat; imply scale through cues (prop scale as "value + relationship"); countable events need evidence; write action as a physical beat chain; adjacent shots must differ in size and angle; check countable body parts; for unwanted things in references, "switch them off"; **never write ages**; maintain a **banned-word dictionary**. **All constraints go into the final "positive lock" block — never in negative form.**
- **Physics and continuity must be written down.** Door / window / opening geometry must be **repeated in full every shot**; prop scale gets "**value + relationship**"; walking gets a **gait lock**, side-by-side gets "shoulder to shoulder on the same depth line", and a single walk across shots gets **consistent camera speed**; fights use a **frame chain + single-take, per-second timeline**.
- **Animation projects add the "animation-principle five-set" per shot.** Squash & stretch, anticipation, follow-through & overlap, arcs, moderate exaggeration — **write them explicitly; the model defaults to averages.** Modelling can keep photoreal texture, but motion follows animation principles, and **physical accuracy yields to expressive motion**; reuse the same lighting wording verbatim shot by shot.

### P6 | Generation, editing and export

Guides you through creating a project on OmniAiLab (omniailabx.com) and uploading all pre-production assets to the asset library; builds the canvas as "script → images → video → audio → editing → export". **Confirm all first frames first, then batch-queue video generation**, checking and retrying shot by shot. AI voice-over (matched to character timbre), BGM (entering/exiting per the emotion curve), layered sound effects (ambience / action / accent). Assemble by shot, layer audio tracks, add subtitles. Export 1080p / 16:9 / 24fps / MP4 / H.264, then run item-by-item QC.

**What you do:** follow the guidance on the platform; confirm all first frames before batch generation.

**Deliverables:** finished MP4 + full asset pack + QC report.

**Pitfalls**

- **Always confirm every first frame before batch generation.** One wrong first frame wastes an entire generated video — the most expensive rework there is.
- BGM in/out points must **follow the P0A emotion curve**, not a feeling — mark only the nodes needing push / reversal / build-up / release.
- **Editing and sound follow five phases.** Rough arrangement → rough cut → generation supervision → fine cut → **final cut**; after final cut, no new generation except emergency fixes. Transitions are designed: match by **movement direction + sound**, leave 8 frames of headroom and tailroom per segment, and cut on the frame where the covering element **fills ≥90% of frame**. Colour is **unified**, not graded shot by shot.

---

## Sub-skills and specialized layers

You don't need all of them every time. **To do just one small thing, say "only do …"** and it calls only that sub-skill, skipping the full pipeline.

### The four sub-skills

| Sub-skill | File | Responsibility |
|---|---|---|
| **ACTING** | `references/ACTING SKILL.md` | Turns abstract emotion into camera-visible behaviour: objective, obstacle, tactic, beats, listening, physical tasks, subtext, eye-line and vocal identity |
| **EMOTION** | `references/EMOTION SKILL.md` | Writes emotion as a character processing an event within a relationship: emotion proposition, internal/external lines, emotion beats, eye-line landing points, voice envelope; plus character permission isolation, contact boundaries, visual-vocabulary purification and generation-failure repair |
| **LIRA** | `references/LIRA SKILL.md` | Optimises image generation / editing prompts and routes models; look comes from the visual-language library, whole-film aesthetics from the aesthetics recipe library |
| **CINEDANCE** | `references/CINEDANCE SKILL.md` | Turns shot requirements into executable video prompts, controlling first frame, spatial staging, eye-lines, optics, lighting, physics and continuity |

### Specialized (mounted) layers — not counted as separate sub-skills

| Layer | File | One-line summary |
|---|---|---|
| **STYLE** visual-language library | `references/STYLE SKILL.md` | **Dictionary**: D director visual languages / P general photographic styles / C capture stocks / R print stocks / S style strength |
| **AESTHETICS** recipe library | `references/AESTHETICS SKILL.md` | **Recipe book**: A01–A07 seven whole-film aesthetics; **proactively triggered** — P1 always proposes 2–3 candidates |
| **COMBAT** | `references/COMBAT SKILL.md` | Attack/defence choreography, closed physical loops, three spatial anchors, shot contracts |
| **BLOCKING** | `references/BLOCKING SKILL.md` | Cross-shot blocking lock: one baseline per scene + `locked` freeze + drift diagnosis; **mandatory for multi-person shots** |
| **PROMPT-DOCTRINE** | `references/PROMPT-DOCTRINE SKILL.md` | Fixed 16-block order + eleven iron rules + solve hard things in the still frame + how to write physics and continuity |
| **ASSET-SYSTEM** | `references/ASSET-SYSTEM SKILL.md` | Text + image paired assets, `@char_/@loc_/@prop_/@staging_` naming, "new state = new asset", voice lock |
| **SCENE-ENGINE** | `references/SCENE-ENGINE SKILL.md` | Five-element dramatic engine (objective / obstacle / tactic / reversal / value shift) + script stress test; **diagnose only, never rewrite** |
| **OPTICS** | `references/OPTICS SKILL.md` | Seven field-of-view anchors (8/18/29/47/84/107°), lens decision tree, multi-shot lens consistency statement |
| **FEATURE-PRODUCTION** | `references/FEATURE-PRODUCTION SKILL.md` | Four shot-table card groups, per-scene opening ritual, asset stress tests, iteration discipline, statute-style locks |
| **MUSIC-SCENE** | `references/MUSIC-SCENE SKILL.md` | Sing-first-then-perform with lip sync: cut 12-second blocks, black-frame video files, disable generated audio, hard lip lock |
| **PROMO** | `references/PROMO SKILL.md` | Dispatch across 14 commercial-short directions (brand ad / TVC, brand short, stream MG, product film, UI motion, title sequence, motion design, game PV, music short, creator video, education, drawing timelapse, video deconstruction, voice clone) + six-step flow and commercial hard rules; **video generated with MiniMax H3 on the OmniAiLab canvas** |
| **ONBOARDING** | `references/ONBOARDING SKILL.md` | **Settle the format first**: a routing table for film / short drama / animation / documentary / promo / title / MV / game PV / UI motion / creator video / education + a three-question convergence method |
| **DOCUMENTARY** | `references/DOCUMENTARY SKILL.md` | Observational documentary: eight spec items, de-dramatised narration, 6–12 s shots with three-tier camera moves, natural-light logic and airborne texture, cross-shot character consistency, colour-system extraction; **enabled when the conversation is a documentary**, while generation methods stay on the existing film-grade layers |
| **ANIMATION** | `references/ANIMATION SKILL.md` | Medium determination, previs vs generation division of labour, hybrid aesthetic split, light defines style, 360° turnaround video, animation principles first |
| **Case-study library** | `examples/case-studies/` | Finished prompt blocks from six commercial-grade AI film projects + "problem → solution" lists, **copy-paste ready** |
| **Documentary templates** | `examples/documentary/` | Seven ready-to-use documentary prompt templates: character turnaround / look board / location / prop / colour card / first frame / video |
| **Case-study figures** | `examples/images/` | 49 method diagrams (how a three-panel character sheet is laid out, how states are separated, what a staging diagram looks like, what colour drift looks like, what "a moving prop behaving like a decal" looks like) + a keyword→figure lookup in `INDEX.md`; ~2.4 MB |
| **Promo sample library** | `examples/promo-cases/` | Raw briefs and finished prompts from **7 real MiniMax H3 films**, organised by direction (brand ad ×4, visual design ×2, UI motion ×1), with a source-record → sub-skill → file mapping table |

### Dispatch quick reference

| What you want to do | What it calls |
|---|---|
| Images only (asset generation or image editing) | LIRA (look from the STYLE library) |
| Video prompts only | CINEDANCE |
| Performance design only | ACTING |
| Emotion only (crying / laughing / anger / fear / disappointment / farewell / reunion / silent reactions; or fixing dead eyes, stray tears, emotion bleed, accidental kissing, dialogue clipping, intensity jumps) | EMOTION |
| Look selection only ("give me the look menu", "D01+C04+R01+S2") | STYLE library |
| Aesthetic selection only ("what style for this scene", "give me aesthetic advice") | AESTHETICS library |
| Fight choreography only ("how should this fight go") | COMBAT layer |
| Blocking / staging only ("how should these people stand", "the positions shifted again") | BLOCKING layer |
| "How do I write this prompt so it doesn't break" | PROMPT-DOCTRINE layer |
| "How do I build / name assets so they don't drift" | ASSET-SYSTEM layer |
| Ready-made sentences / what others got wrong | Case-study library (`examples/case-studies/`) |
| Want to see what a rule actually looks like / "I don't get it" | Case-study figures (`examples/images/`; lookup table in `images/INDEX.md`) |
| Want to copy a **real, already-produced** promo sample / see how a direction is actually written | Promo sample library (`examples/promo-cases/`, organised by direction) |
| Script structure only ("does this scene work", "where is it weak") | SCENE-ENGINE layer |
| Lens choice / lens drift only ("how wide should this lens be") | OPTICS layer |
| How to organise a feature ("how to manage 100+ scenes") | FEATURE-PRODUCTION layer |
| Singing / rap sections ("lip sync is off", "how do I make it sing our song") | MUSIC-SCENE layer |
| Animation / hybrid medium ("can this be animated", "moving objects look like stickers") | ANIMATION layer |
| Documentary only ("I want to make a documentary", "how do I shoot real people", "how to use natural light") | DOCUMENTARY layer |
| Commercial short / promo only ("I need a promo", "a brand ad", "logo animation", "UI motion", "title sequence", "game PV") | PROMO line (pick a direction first) |
| "I do not know what to make" / "where do I start" | ONBOARDING layer (settle the format) |

**Full shot chain:** ACTING → EMOTION → BLOCKING (blocking first) → LIRA (+ STYLE look) → CINEDANCE. **Fight shots** route through COMBAT before CINEDANCE. **Before writing, pass the PROMPT-DOCTRINE fixed block order and iron rules; name and lock every character / scene / prop per ASSET-SYSTEM first.**

---

## Model reference

These are the whole-film's single source of truth. **Do not mix in model names from other platforms.**

| Purpose | Model |
|---|---|
| Character generation / consistency | Seedream 5.0 |
| Scene / environment master plates | Flux |
| Prop / product master plates | Nano Banana Pro (香蕉Pro) |
| Image editing (first choice) | Nano Banana Pro (香蕉Pro) |
| Rough AI texture repair | Seedream |
| Local micro-edits / location viewpoint changes | Qwen Image |
| Images: general generation (common) | image2 |
| Images: Chinese text / covers / posters / storyboards | **image2.5** |
| Video: characters | Seedance 2.5 |
| Video: VFX / transformation | Kling O3 |
| Video: prop close-ups | Vidu |
| Video: fallback / trial | Wan 2.6 / Seedance 2.0 Fast |

> **Hard image-model constraint:** whenever Chinese text appears in frame (signage, packaging, posters, covers, books, screens / subtitle boards, street signs) or the deliverable is itself a cover, poster or storyboard (full shot-breakdown board), **always prefer image2.5** — its Chinese glyph shapes and layout are the strongest (stronger than Nano Banana Pro), and its character consistency and storyboard continuity are best too. Use image2 for general generation. **Do not treat Nano Banana Pro as the default choice for these tasks.**

---

## Pitfall table

These **29** items are ordered by "likelihood × severity". Scan them before the P1, P4 and P5 confirmations.

| # | Pitfall | Correct approach |
|---|---|---|
| 1 | Multi-person blocking drifts across shots: on one side in the last shot, gone in the next | One blocking baseline per scene, read per shot, change only changed fields, freeze unchanged characters; no coordinate-change evidence, no blocking edits |
| 2 | Skipping performance and emotion when writing video prompts | ACTING must produce the shot's performance passage + EMOTION the emotion layer, then CINEDANCE composes |
| 3 | Chinese in frame but using the default image model | Chinese text / covers / posters / storyboards → always prefer image2.5 |
| 4 | Writing 16:9, 10 seconds or a model name into the prompt body | Ratio, resolution, duration and model name belong in the platform UI, never the body |
| 5 | Stacking "no XX" / "exclude XX" in prompts | Always express positively ("exclude digital feel" → "photochemical film texture") |
| 6 | Writing film stock as real capture ("shot on 70mm film") | Write "70mm film **simulation** texture"; don't pretend it is physical film |
| 7 | Writing a director's name in the prompt ("X's style") | Names are internal retrieval tags only; convert to concrete visual traits for delivery |
| 8 | Referencing a non-existent image (`{{Image 3}}` without uploading) | With no real reference, delete all asset numbers and inheritance wording |
| 9 | Wanting to change the look after the style lock | The lock is frozen; changing it means going back to P1 |
| 10 | Emotion curve is high-energy throughout with no breathing zone | 8–14 nodes, at least one genuine breathing zone, no invented release |
| 11 | Skipping character batches: writing downstream states before upstream confirmation | Unlock by dependency batch; blood relatives / variants / costume / injury / age only after base characters are locked |
| 12 | Writing "the two start fighting" for a fight shot | Fill the shot contract, fix A/B sides and three spatial anchors, then choreograph the spine and physical loop |
| 13 | Asking for five confirmations at once to finish in one go | Show only the step needing confirmation each round; only a genuine confirmation unlocks the next |
| 14 | Treating confirmed images as drafts and regenerating them | Confirmed means frozen and depended upon downstream; regenerating invalidates everything downstream |
| 15 | Writing "lens character" into video prompts (wanting anamorphic), then lenses drift shot to shot | Bake optical character into the **scene plate**; in video prompts you cannot even write "no flare" — naming flare summons flare |
| 16 | Night scenes won't go dark; the model keeps giving dusk | **Bake the darkness into the plate** (2–3 stops down, crushed blacks, one cold rim light) + **crop the sky out** |
| 17 | Overwriting a new state onto an old asset (costume change / injury on the same image) | **New state = new asset + new name**; keep the old asset — overwriting robs every prior shot of its reference |
| 18 | Cool footage gets pulled warm; "no yellow" does nothing | Use a positive **"colour constitution sentence"**; for uncroppable glowing objects in references write "**it is switched off in this film**"; choose stock by where the shadows lean |
| 19 | Stairs vanish and a character jumps up in one move; walking slides or floats | Write ascent as physics + **name openings as objects that must exist**; add a **gait lock**; write "shoulder to shoulder on the same depth line" for side-by-side; **consistent camera speed** across shots |
| 20 | Splitting a fight across generations always stutters; editing can't save it | **Frame chain** (segment N's last frame = N+1's first) + a hero shot that is **single-take, per-second timeline, with slow motion explicitly banned**; **name every action and give it a vector** |
| 21 | Generating without a script health check, discovering mid-way that a scene doesn't work | Run the **five-element engine** first for its **single weakest point** and three-layer fixes; hunt **inert reversals**. **Diagnose only, never rewrite** |
| 22 | Faces, voices, seating and eye-lines all drift across dozens of shots in one room | **Sound bible** (a VOICE LOCK block per character, pasted verbatim) + asset **scene suffixes** + beat timing per segment + eye-line as its own block |
| 23 | Shot size and perspective drift (wide-angle feel comes and goes) | Choose lenses by **content type** (FOV anchors 8/18/29/47/84/107°); never mix incompatible content categories in one beat; write a **lens consistency statement** |
| 24 | Heroes teleport, swap places, or the camera jumps across the room | Give every scene an **opening ritual**: a one-second fixed-blocking wide master + a **GEO spatial map** + a **compass sentence** (never cross the 180° line) |
| 25 | A shot stalls for a dozen versions and gets worse | **Ten-to-fifteen rule**: past that it isn't wording — **change the shot**; iterate **one change at a time** and **log everything** |
| 26 | Lip sync is off in sung / rap sections, or generation is blocked by copyright checks | Sing first, perform second: cut the final mix into **12-second blocks**, make **black-frame video files**, **disable generated audio in settings**; then write a **hard lip lock** and **mouth ownership** |
| 27 | Moving objects look like "stickers", surfaces go dead, brushwork looks flattened | Moving objects get **clean solid volume**; heavy brushwork is reserved for the environment; hybrid aesthetics need a **"split declaration"** |
| 28 | Hand-painted / stylised environments look flat, stuffy, volume-less; a different shot no longer looks like the same film | Switch to **golden-hour side-backlight + long, crisp shadows**; and use **one lighting wording for the whole film, reused verbatim shot by shot** |
| 29 | Static character sheets can't hold cross-generation consistency; characters get invented by the model | Animation lines use a **360° turnaround video** (turn / expression / voice) as the primary character reference; **every moving asset must pass a video test first** |

---

## Repository layout

```text
omniailab-ai-director/
├── SKILL.md                     # Master dispatcher: P0→P6 trunk, gates, sub-skill mapping, model reference
├── VERSION                      # Version number
├── openai.yaml                  # Interface metadata (display_name / default prompt / implicit invocation)
├── LICENSE                      # MIT
├── README.md                    # Simplified Chinese
├── README_EN.md                 # This file (English)
├── references/                  # Specification layer: four sub-skills + all specialized layers + dictionaries
│   ├── ACTING SKILL.md
│   ├── EMOTION SKILL.md
│   ├── LIRA SKILL.md
│   ├── CINEDANCE SKILL.md
│   ├── STYLE SKILL.md
│   ├── AESTHETICS SKILL.md
│   ├── aesthetic-recipes.md
│   ├── COMBAT SKILL.md
│   ├── BLOCKING SKILL.md
│   ├── blocking-stage-schema.md
│   ├── blocking-weapon-library.md
│   ├── PROMPT-DOCTRINE SKILL.md
│   ├── ASSET-SYSTEM SKILL.md
│   ├── SCENE-ENGINE SKILL.md
│   ├── OPTICS SKILL.md
│   ├── FEATURE-PRODUCTION SKILL.md
│   ├── MUSIC-SCENE SKILL.md
│   ├── ANIMATION SKILL.md
│   ├── DOCUMENTARY SKILL.md
│   ├── PROMO SKILL.md
│   ├── ONBOARDING SKILL.md
│   ├── promo/                   # 14 promo directions (78 files, original detail folders preserved)
│   ├── story_bible.md / emotion_curve.md / creative_baseline.md
│   ├── character_assets.md / prop_assets.md / scene_assets.md
│   ├── storyboard.md / video_prompts.md / omniailab_production.md
│   ├── director-styles.md / photo-styles.md / capture-films.md / print-films.md
│   ├── shot-emotion-engine.md / performance-palette.md
│   ├── generation-guardrails.md / seedance-production.md
│   └── (38 specification documents in total; plus 78 direction files under promo/)
└── examples/                    # Finished-work layer: copy-paste ready
    ├── floor17_script.md        # Sample script "Floor 17" (30-second suspense short; only on request)
    ├── aesthetics/              # Ready-made prompts for the seven A01–A07 aesthetics
    ├── case-studies/            # Six commercial-grade AI film case studies + README stage index
    ├── documentary/            # Seven ready-to-use documentary prompt templates
    ├── promo-cases/            # Seven real promo samples + index (organised by direction)
    └── images/                  # 49 case-study figures + INDEX.md (keyword → figure lookup), ~2.4 MB
```

> **Specifications live in `references/`; copy-paste-ready finished work lives in `examples/case-studies/`; the visible look of it lives in `examples/images/`.** Whenever it's a question of "how exactly do I write this sentence", take a finished block from `examples/case-studies/` first. Whenever it's a question of "what does that actually look like", show the figure from `examples/images/` (see the keyword lookup table in its `INDEX.md`). Whenever it's a question of "how is a given commercial-short direction actually written", take a sample from `examples/promo-cases/` first.

---

## Deliverables

After a full run you get:

1. The final MP4
2. All first frames (packaged)
3. All video segments (packaged)
4. OmniAiLab canvas project link
5. Final QC report
6. Project asset pack (character / prop / scene images + all prompt documents)

---

## FAQ

**Q: I want to change the look mid-way.**
A: Go back to P1. Downstream assets are invalidated as a consequence, so settle the look at P1.

**Q: It keeps asking for confirmation — can it just finish in one go?**
A: Gates are an anti-rework mechanism, not process decoration. Each confirmation point carries a batch of dependent deliverables — skipping it magnifies the error into the next stage.

**Q: Can I use only one part?**
A: Yes. Say "images only", "blocking only", "fight choreography only" — see the dispatch table above; it skips the full pipeline.

**Q: Must generation happen on OmniAiLab?**
A: Sub-skills handle "how to describe it" (prompt construction and model selection); actual generation runs on OmniAiLab, and model naming follows the table above. You may also generate on an external platform, but align model names with this reference.

**Q: Can I change the script mid-way?**
A: Only details that **don't change assets**. Once characters, scenes or the ending change, previously generated assets must be redone.

**Q: I don't want the aesthetic proposal — can I skip it?**
A: Yes. Reply "no need" and it continues with standard sourcing; with no match it says so rather than forcing one.

---

## Recommended tools and models

This Skill is a pure-text specification and is not bound to any one model — it runs on any tool or model. But the pipeline is long (P0→P6, dozens of generation instructions), so **the stronger the model, the less likely it is to lose context or miss a gate mid-run.**

| Tool | Best used for |
|---|---|
| **Codex** (recommended) | Running the full P0→P6: strong engineering, direct project-file access, batch asset-list processing and scripted output organisation |
| **Claude** | Script breakdown, prompt refinement, long-form documents (native Skill support, stable long-text rewriting) |
| **WorkBuddy** | Running the full P0→P6: read/write files and run scripts in-session, with each stage's output landing on disk |

**Model guidance**

- **Preferred:** the latest generation such as GPT-5.6 or DeepSeek V4 — steadier long-context and instruction following, less mid-run "amnesia" or missed gates.
- **Workable:** any reasoning model with ≥64K context can complete the pipeline, but double-check outputs at each gate.
- **Not recommended:** lightweight models on the full pipeline (the P0A ten-item breakdown is the easiest place to lose items).

> Which models you can actually choose depends on your account; models cycle fast and this Skill needs no change — it specifies "how", not "with whom".

---

## Companion manual

This README is a complete mirror of the manual. The manual itself (with per-stage confirmation wording, the pitfall table and the quick-reference tables) lives in a Feishu doc, version-synced with the Skill:

- **Manual (Chinese):** <https://zcn03zgas1zl.feishu.cn/wiki/P2fhwADXvil24UkNkDCcw1x2nbA>

> **Mandatory sync:** every Skill update (version number, trunk workflow, model reference, or sub-skill wiring) must be reflected in that manual **and** in both READMEs, keeping version numbers aligned.

---

## License

This repository is released under the **MIT License** — see [LICENSE](LICENSE). You may freely use, modify and distribute it, including commercially, provided the copyright and permission notice is retained.

> Note: each file in this Skill retains the header/footer notice `© OmniAiLab ｜ Developer: Mochiball`. That notice identifies the source and preserves brand attribution; **it does not impose any restriction beyond the MIT License.**

---

## Credits

- Publisher and maintainer: **OmniAiLab** ([omniailabx.com](https://www.omniailabx.com/))
- Developer: **Mochiball**
- The methods in the case-study library are **distilled and rewritten in Chinese** from public post-mortems of several commercial-grade AI film projects — method extraction only, no verbatim reuse, with attribution unified under OmniAiLab.
- This Skill uses only **OmniAiLab**'s own platform capabilities and introduces no third-party platform dependencies.

---

<div align="right">

[简体中文](README.md) ｜ **English**

</div>

> © OmniAiLab ｜ Developer: Mochiball ｜ omniailabx.com
