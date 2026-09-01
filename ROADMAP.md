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
- [x] **Self-check quizzes** — 2–3 mechanism questions per Part (01–12),
  answers behind `<details>`, in the page's honest voice.

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
- [x] **Editable attention, phase 2** — type a full sentence (12-word cap); a
  toy rule-based tagger assigns each word's role, guesses are marked and
  correctable, and the same hand-built vector logic runs unchanged.

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
- [x] **Editorial pass** — em-dash density cut ~88%, consistency fixes; a
  second full read-over (Aug 2026) fixed factual, clarity, and voice issues.
- [x] **og:image** — 1200×630 social share card (`og-image.png`, regenerable
  from `og-card.html`), full og:/twitter: meta in both HTML files.
- [x] **Frontier-card masonry** — the Part 12 cards stack per column, so an
  open card no longer leaves whitespace beside itself.

## Next

- [ ] **Translations** — the single-file format makes per-language forks easy;
  needs a contributor with native fluency per language.
- [ ] **Real device QA** — the mobile pass was emulated; an hour with actual
  phones (especially canvas drawing by finger) would be worth it.
- [x] **Annual re-dating sweep (Sep 2026)** — frontier cards and footer restated
  as of September 2026; `LIVE_MODEL` is `claude-sonnet-5` with thinking
  disabled so the Part 9 demo stays snappy. Re-date or retire cards yearly; a
  retired API model ID fails silently into the canned fallback.

## Ideas (from the August 2026 review)

Ranked by value to the reader. All respect the constraints: single
self-contained file, zero network requests, every demo really computes what it
claims, no ML background assumed.

- [ ] **A real tiny transformer, running live** — Part 6; large. The one
  structural gap: Parts 1–6 teach every component, but no demo runs an actual
  transformer. Train a 2-layer, ~32-dim, word-level transformer offline on the
  page's existing corpus and embed its weights as hex like `DIGIT_DATA`; the
  page then does honest forward passes: real learned attention heatmaps
  (contrast with Part 5's hand-built heads), real logits, real sampling.
- [ ] **Train the embeddings for real** — Part 4; medium. The scatter is the
  page's only labeled mock. Learn genuine 2-D embeddings in-browser from
  corpus co-occurrence (a few hundred visible SGD steps), watching points
  drift from noise into clusters.
- [ ] **RLHF ranking demo, reader as the rater** — Part 8; medium. Show 2–3
  candidate answers, let the reader rank them, fit a tiny logistic reward
  model on their rankings live, and show it scoring unseen answers, including
  a confident, wrong, pleasant one that wins. Sets up Part 10 mechanically.
- [ ] **Confidence-on-garbage experiment** — Part 10; small. One button: feed
  the reader's trained digit net 100 random-noise grids and plot the histogram
  of max-softmax confidence. "There is no no-answer bucket" becomes a measured
  number, computed on the network the reader personally trained.
- [ ] **Context-length toggle on the n-gram sampler** — Part 1; small-medium.
  A "context: 1 word / 2 words" switch (trigram counts) plus a live readout of
  distinct contexts and the fraction seen exactly once; the reader watches
  coverage collapse with one extra word of context, which is the whole
  motivation for neural LMs.
- [ ] **Neuron feature microscope** — Part 2; small. Hovering a hidden-layer-1
  neuron renders its 64 incoming weights as an 8×8 amber/blue tile: what
  pattern does this neuron like? Real learned stroke detectors appear, and
  some tiles look like nothing: an honest first taste of superposition,
  bridging to the Part 12 interpretability card.
- [ ] **Speculative decoding, actually demonstrated** — Part 12; medium. Use
  the bigram model as draft and a trigram model as verifier with the real
  accept/reject rule; show acceptance rate and verify by sampling statistics
  that the output matches the verifier alone. First frontier card whose claim
  the reader can watch hold.
- [ ] **Measured n² on your device** — Part 7; small. Next to the theoretical
  cost curve, time attention-shaped dot-product workloads at several sequence
  lengths in the browser and plot the measured milliseconds.
- [ ] **RoPE decay mini-plot** — Part 5; small. Head A already computes
  rotary-style q·k scores; plot that dot product against token distance, live
  from the same vectors, grounding Part 7's claim about position handling by
  showing the tendency instead of asserting it.
