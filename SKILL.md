---
name: ppt-image-first
description: Build presentation plans for PPT / slides / decks through a conversation-first workflow, then propose multiple visual directions with preview images before writing deck specs. Use when the user asks to create a PPT, presentation, deck, 答辩稿, 路演 deck, 产品介绍 PPT, 汇报 PPT, or when the user has only a topic or rough materials and needs help clarifying structure, style, and page planning before generation.
---

# PPT Image First

Use this skill to turn a vague PPT request into a generation-ready, image-first deck plan.

## I/O Contract

- Input: a PPT topic, rough goal, existing notes/materials, or complete report-like narrative.
- Optional anchors: audience, page count or duration, school/company/lab/course/brand identity, use occasion, source files, and style constraints.
- Output: a confirmed content basis, visual style previews, deck specs, generated page visuals, review surface, and final PPT after approval.
- Confirmation gates: `需求确认`, `风格确认`, `生成前确认`, and final review approval.
- Default ratio: generate preview images and final page visuals in `16:9` unless the user explicitly requests another ratio.

## Mode Selection

Start by choosing the lightest mode that can satisfy the request. Do not ask the user to configure this unless the tradeoff matters.

- `快速草案`: use when the user wants a quick outline or rough direction. Keep intake short, skip heavy preview iteration, and still preserve the required confirmation gates before generation.
- `标准提案`: default for most PPT creation requests. Run the full conversation-first, preview-first workflow.
- `高保真图像优先`: use when visual quality, style exploration, or final slide imagery is the core value. Expect richer previews, style refinement, and review/retouch rounds.

Read `references/modes.md` if the request is ambiguous, speed-sensitive, or likely to be over-served by the full workflow.

## Workflow Phases

Follow these phases in order and do not skip the confirmation gates:

1. Intake: clarify lightly, identify anchors, output a short baseline judgment, then get `需求确认`.
2. Content basis: create or extract `content_report.md` unless the user already supplied complete report-like content; show a synthesized judgment, not the raw file by default.
3. Style preview: align style boundaries, propose directions, generate `首页 / 目录页 / 正文页` previews for each direction, support refinement, then get `风格确认`.
4. Planning lock: run `风格反演确认`, then write `design_spec.md`, `slide_blueprint.md`, and `spec_lock.md` in that order; summarize and get `生成前确认`.
5. Generation review: generate page visuals, optionally run candidate selection, open the review HTML, retouch as needed, and export the final PPT only after approval.

Read `references/workflow.md` for stage-by-stage execution details.

## Progressive Loading

- Intake and baseline: read `references/conversation_framework.md` only when you need the conversation-first intake pattern.
- Mode choice: read `references/modes.md` when deciding between fast, standard, and high-fidelity paths.
- Style proposals: read `references/style-system.md` when producing proposal cards or interpreting V1-V8 internally.
- Preview/review UI: read `references/preview-flow.md` before producing style previews, candidate-picker pages, or review pages.
- Content basis: read `templates/content_report_reference.md` before writing `content_report.md`.
- Planning files: read `templates/design_spec_reference.md`, `templates/slide_blueprint_reference.md`, and `templates/spec_lock_reference.md` immediately before writing those files.

## Working Principles

- Treat the user like a client and yourself like the proposing design agent.
- Do not force the user to configure design parameters manually; translate their natural-language intent into design decisions.
- Ask for real-world identity anchors when relevant, but treat them as grounding context rather than style questions.
- Keep intake lightweight; do not turn content basis or style alignment into a long questionnaire.
- Use style vectors internally, but present front-stage options as concise proposal cards plus image previews.
- Use the content basis for previews and planning rather than generic placeholder structures.
- Mark inferred claims carefully; do not present unsupported precise data, experiment results, citations, or institutional conclusions as user-provided facts.
- Show summaries, proposal cards, previews, and review surfaces by default; show raw planning files only when useful or requested.

## Hard Rules

- Preview-first: final style confirmation should be based on generated `首页 / 目录页 / 正文页` previews, not text-only choices.
- Shells are mandatory: use `assets/preview_shell/index.html`, `assets/candidate_picker_shell/index.html`, and `assets/review_shell/index.html` as the base UIs for their stages.
- Open the local preview, candidate-picker, review, and final PPT files immediately when those stages produce them; if opening fails, state the blocker and provide the path.
- Do not write `slide_blueprint.md` before style direction and `风格反演确认` are complete.
- Keep generation image-first when the confirmed direction depends on generated page visuals; do not silently fall back to shape-by-shape PPT construction or hand-drawn code substitutes.
- Treat generated page visuals as complete by default; post-generation overlays default to zero unless they are traceable to approved blueprint fields.
- Before full generation, ask whether the user wants one final image per slide or multiple final candidates per slide.
- Do not export the final PPT immediately after first-pass generation; export only after the reviewed pages are approved.

## Output Hierarchy

Use these layers consistently:

- `content_report.md` = upstream content basis when the user did not provide complete report-like material.
- `design_spec.md` = global deck rationale and confirmed visual system.
- `slide_blueprint.md` = page-by-page intent and content plan.
- `spec_lock.md` = execution constraints and final generation guardrails.

`content_report.md` supports the 3 core planning files; it does not replace them. `spec_lock.md` is always the last core planning file.
