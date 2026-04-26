# ppt-image-first

[中文](./README.md) | **English**

Conversation-first, image-first PPT workflow for building presentation plans, style previews, review loops, and generation-ready slide specs.

`ppt-image-first` is designed for PPT / slides / decks that should not jump straight into rigid templates or direct slide assembly. It first clarifies the deck, builds a content basis, proposes visual directions with real previews, supports refinement, and only then moves into locked planning and downstream generation.

> **Output note: this is an image-first workflow.** By default, the workflow uses **GPT Image 2** to generate full-slide page visuals, then places those page images into a PPTX container for delivery. It is not a fully editable PowerPoint generator that recreates every text box, shape, chart, and decoration as native PowerPoint objects. The result is closer to a high-fidelity visual deck: suitable for presenting, sharing, and image-level retouching, but slide text and design elements are usually not individually editable as native PPT elements.

## Quick examples

### 1. Workflow overview slide

![Workflow overview slide](./docs/images/workflow-overview-slide.png)

### 2. Thesis defense / report cover example

![Meteorology defense cover example](./docs/images/sample-meteorology-defense-deck.png)

### 3. Campus / red-theme deck example

![Campus red-theme PPT example](./docs/images/sample-red-campus-deck.png)

### 4. Technical research body-page example

![Technical research body-page example](./docs/images/sample-tech-research-body-page.png)

## Demo PPT

The repository also includes a downloadable presentation that was directly created around this workflow:

- [Download demo PPT (ppt-image-first-demo-deck.pptx)](./docs/demo/ppt-image-first-demo-deck.pptx)

This deck is about `ppt-image-first` itself, so it works well as a quick sample for checking the workflow's page quality, narrative structure, and overall finish.

---

## What it does

This skill is built for requests like:

- "Help me make a PPT"
- "Turn this report into a presentation"
- "Make a thesis defense deck"
- "Create a product intro PPT"
- "Generate style directions before writing the final slides"
- "I only have a topic and rough notes — help me turn it into a real deck"

Instead of forcing the user into a parameter form, it follows a staged workflow:

1. light intake
2. baseline judgment
3. requirement confirmation
4. pre-style content research / `content_report.md`
5. style-boundary alignment
6. multi-direction visual preview generation
7. style refinement if needed
8. style confirmation
9. style inversion confirmation
10. planning files
11. pre-generation confirmation
12. generation branch selection
13. review and retouch loop
14. final export

---

## Why this exists

Many PPT workflows fail in one of 2 ways:

- they become **too template-driven**, so the output looks polished but generic
- they become **too structure-light**, so the deck looks good but says very little

`ppt-image-first` is built to avoid both.

Its core idea is:

- keep the conversation front-end light
- build content depth before style when materials are thin
- use real preview images before asking the user to choose a direction
- treat generated page visuals as the main output path, not as background plates for manual patching

---

## Core principles

### 1. Conversation-first

The user is treated like the client. The agent is the proposing design side.

That means:

- the first intake stays light
- the workflow avoids long questionnaires
- the user reacts to judgments, directions, previews, and refinements
- the workflow does not expose raw internal controls unless necessary

### 2. Image-first

The workflow assumes that visual direction should be tested with **actual generated preview images**, not just text descriptions, wireframes, or placeholder shells.

Final generation follows the same logic: it prioritizes using **GPT Image 2** to render complete slide pages and then packages those rendered pages into PPTX. This preserves visual consistency and finish, but it does not promise that every element is a native editable PowerPoint object.

### 3. Content before styling when needed

After `需求确认`, the skill inserts a **pre-style content basis stage** unless the user already provided a complete report-like narrative.

That stage produces `content_report.md`, which gives later preview pages and planning files a real content source.

### 4. Preview before lock-in

The skill does not ask the user to choose a final style from text alone. It first generates preview sets for:

- 首页
- 目录页
- 正文页

### 5. Review is part of the workflow

The first generated deck is not treated as final delivery. The skill includes a dedicated review-and-retouch round using a review HTML shell.

---

## Workflow overview

### Stage 1 — Intake and baseline judgment

Collect only the essentials:

- purpose
- audience
- rough length
- available materials
- real identity anchors such as school / company / lab / course / brand

Then output a short baseline judgment and stop for **需求确认**.

### Stage 1.25 — Pre-style content research

If the user does not already provide a complete report-like narrative, generate a grounded `content_report.md`.

This stage is used to:

- deepen thin topics
- structure scattered material
- make previews content-bearing
- ground later planning files

### Stage 1.5 — Style-boundary alignment

Ask only 3 short questions:

- bright / dark / middle
- normal professional / clearly stylized
- how many directions to preview

### Stage 2 — Style proposal and preview

Generate multiple style directions and real preview images for:

- cover
- TOC
- body page

### Stage 2.5 — Style refinement

If the user likes a direction but wants changes, continue from that direction instead of forcing final selection.

### Stage 2.75 — Style inversion confirmation

Read the chosen preview images as evidence of what the user actually liked, and extract:

- what should clearly continue
- what looked good but needs confirmation
- what was probably one-off and should not be hard-locked

### Stage 3 — Planning files

Generate in this order:

1. `design_spec.md`
2. `slide_blueprint.md`
3. `spec_lock.md`

Then stop for **生成前确认**.

### Stage 4 — Generation

Ask whether the user wants:

- one final image per slide
- or multiple candidates per slide

If the user chooses multiple candidates, the candidate-picker shell is used before the final review stage.

### Stage 5 — Review and retouch

Use the review shell as the default review surface.

If the user is satisfied, finish the review. If not, they can copy structured feedback back into the chat and continue the retouch loop.

---

## Bundled workflow assets

This skill ships with fixed workflow shells that are meant to be reused, not replaced casually:

- `assets/preview_shell/index.html`
- `assets/candidate_picker_shell/index.html`
- `assets/review_shell/index.html`

These shells support:

- preview comparison
- candidate selection
- review and retouch collaboration

---

## Planning artifacts

The skill uses 4 main artifacts across the workflow:

### `content_report.md`

Pre-style content basis used when the user does not already provide a complete report-like narrative.

### `design_spec.md`

Deck-level rationale and global direction.

### `slide_blueprint.md`

Page-by-page intent, content payload, and visual strategy.

### `spec_lock.md`

Execution constraints, grounding policy, and what downstream generation is allowed or not allowed to do.

---

## What makes this workflow different

### Not template-first

It does not start from fixed page templates or a rigid layout family.

### Not form-first

It avoids turning PPT creation into a long configuration questionnaire.

### Not text-mockup-first

Preview means real image previews by default.

### Not shallow by default

If the topic is thin, the skill adds a content-basis stage before style.

### Not patch-overlay-driven

It avoids using generated images as simple backgrounds and then rebuilding the slide with ad hoc overlay text and decorations.

---

## Repository structure

```text
ppt-image-first/
├─ SKILL.md
├─ README.md
├─ README.en.md
├─ references/
│  ├─ workflow.md
│  ├─ conversation_framework.md
│  ├─ preview-flow.md
│  └─ ...
├─ templates/
│  ├─ content_report_reference.md
│  ├─ design_spec_reference.md
│  ├─ slide_blueprint_reference.md
│  └─ spec_lock_reference.md
└─ assets/
   ├─ preview_shell/
   ├─ candidate_picker_shell/
   └─ review_shell/
```

---


## Good fit

This workflow is a good fit for:

- thesis defense decks
- research presentations
- project reports
- product introduction decks
- pitch decks
- training decks
- proposal decks
- internal review / recap decks

Especially when:

- the user has only a topic or rough notes
- the deck needs stronger content grounding
- the visual direction should be chosen from actual previews
- the final deck should stay aligned with approved preview logic

---

## Notes

- The workflow assumes `16:9` by default unless the user explicitly asks for another ratio.
- Preview pages are expected to be content-bearing, not empty placeholders.
- The workflow intentionally includes multiple confirmation points instead of collapsing everything into one pass.
- The review stage is part of the main workflow, not an optional afterthought.

---

## Acknowledgements

This project acknowledges the [Linux.do community](https://linux.do/) for its open-source sharing and promotion culture.
