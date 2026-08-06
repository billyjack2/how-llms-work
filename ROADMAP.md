# Roadmap / what's missing

Gaps and ideas, roughly ordered by how much they'd improve the lesson for the
target audience. Checked items are done.

## Content

- [x] **Agents & tool use** — Part 11, with a step-through agent-loop demo.
- [x] **Hallucination mechanics** — Part 10, tied back to the softmax (Part 1)
  and training incentives (Part 8).
- [x] **RAG mini-demo** — Part 7: query → scored chunks → assembled prompt,
  honestly labeled word-overlap cosine vs real embeddings.
- [x] **Sampling beyond temperature** — top-k / top-p truncation in the Part 1
  sampler, with cut tokens shown and survivors renormalized.
- [x] **Fine-tuning in practice** — LoRA/QLoRA card in Part 12.
- [x] **Running models locally** — llama.cpp/Ollama/GGUF/quantization card.
- [x] **Evaluation literacy** — "How to read a benchmark" note in Part 12.
- [x] **Multimodality** — images-as-tokens card in Part 12.

## Interactivity

- [x] Live network diagram for the digit net (weights, activations, hover
  isolation), now with two hidden layers.
- [x] Nearest-neighbor exploration in the embedding scatter.
- [x] **Glossary popovers** — ~30 terms, dotted underlines, hover/tap cards
  with cross-links to the Part that teaches each concept.
- [x] **Editable attention sentence** — role-preserving word swaps that show
  the hand-built heads read roles and positions, not word identity.
- [x] **Real-tokenizer comparison** — curated subset of genuine GPT-2
  vocabulary, greedy longest-match, labeled as an approximation.
- [x] **Choose-your-own decoding** — the hero pauses and lets the reader pick
  the next token from the second pass on.

## Presentation & infrastructure

- [x] **GitHub Pages deployment** — https://billyjack2.github.io/how-llms-work/
- [x] **Offline fonts** — latin variable-font woff2 subsets embedded as data
  URIs; zero network requests.
- [x] **Mobile pass** — overflow fixed and asserted at 320/375/390px.
- [x] **Accessibility pass** — ARIA on all custom controls, measured contrast
  fixes (heatmap numbers, code-in-panel, warn labels), keyboard paths.
- [x] **Print stylesheet** — clean ~30-page PDF handout, details expanded,
  panels flattened for ink.
- [x] **Presenter mode** — speaker notes per section behind `?presenter=1`
  (or triple-tap `p`).
- [x] **Editorial pass** — em-dash density cut ~88%, consistency fixes.

## Next

- [ ] **og:image** — a social share card (the page currently shares with text
  only).
- [ ] **Self-check quizzes** — 2–3 questions per Part, answers hidden behind
  `<details>`, in the page's honest voice.
- [ ] **Translations** — the single-file format makes per-language forks easy;
  needs a contributor with native fluency per language.
- [ ] **Real device QA** — the mobile pass was emulated; an hour with actual
  phones (especially canvas drawing by finger) would be worth it.
- [ ] **Annual re-dating sweep** — the frontier cards state facts "as of early
  2026"; schedule a yearly pass to re-date or retire cards.
- [ ] **Editable attention, phase 2** — let readers type a full sentence with
  POS auto-tagging, keeping the hand-built vector logic honest.
