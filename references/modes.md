# Mode Guidance

Use the lightest workflow that still protects output quality. Choose a mode internally unless the user's request makes the tradeoff worth asking about.

## Quick Draft (`快速草案`)

Use when:
- the user asks for an outline, rough PPT plan, first draft, or quick direction
- the deck is exploratory and final visuals are not the main value yet
- the user emphasizes speed over polish

Behavior:
- keep intake to the minimum needed to identify purpose, audience, and rough page range
- produce a short baseline judgment and get `需求确认`
- create a compact content basis or structured extraction, not a long report, unless the topic needs grounding
- offer fewer style directions by default, usually 1-2
- still do not generate final PPT pages before the required confirmation gates
- if the user only needs planning, stop after the useful plan instead of forcing generation

## Standard Proposal (`标准提案`)

Use when:
- the user asks to make a PPT, deck, presentation, 汇报, 答辩稿, 路演 deck, 产品介绍 PPT, or similar deliverable
- the user provides a topic or partial materials but expects a usable finished deck
- there is no strong reason to optimize only for speed or only for visual fidelity

Behavior:
- follow the full workflow in `references/workflow.md`
- default to 3 style directions when the user gives no preview count
- use the normal content basis, style preview, planning lock, generation, and review flow
- keep summaries front-stage and planning files backstage unless the user asks to inspect them

## High-Fidelity Image-First (`高保真图像优先`)

Use when:
- the user asks for strong visual impact, image-first slides, distinctive style exploration, poster-like slides, or high-end presentation design
- the user is comparing style directions or wants polished generated page visuals
- visual consistency and review/retouch quality matter more than speed

Behavior:
- preserve the full preview-first workflow
- expect style refinement rounds if the first directions are not enough
- use the selected preview images as primary visual evidence during `风格反演确认`
- keep deck-level continuity strict across later page prompts
- use the candidate-picker path when the user wants multiple final options per slide
- keep review HTML as the main collaboration surface before final PPT export

## Escalation and De-escalation

- Move from `快速草案` to `标准提案` when the user asks to turn the plan into a real deck.
- Move from `标准提案` to `高保真图像优先` when the user reacts mainly to visual direction, polish, or generated slide quality.
- Move downward when the user says they only need an outline, a quick structure, or no visuals yet.
- Do not hide important tradeoffs. If a lighter mode would skip something the user likely expects, say so briefly and ask before skipping it.
