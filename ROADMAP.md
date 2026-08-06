# Roadmap / what's missing

Gaps and ideas, roughly ordered by how much they'd improve the lesson for the
target audience (engineers without ML background). Checked items are done.

## Content gaps

- [ ] **Agents & tool use.** The biggest omission for a 2026 engineering
  audience: function calling, the model-emits-JSON → runtime-executes → result
  re-enters-context loop, MCP, and why agent reliability compounds per-step
  error rates. Deserves its own Part, between Prompting and the Frontier.
- [ ] **Hallucination mechanics.** The page explains sampling (Part 1) but never
  closes the loop: the model always emits a distribution, there is no "I don't
  have this fact" state in the architecture, and RLHF can reward confident
  guessing. One honest section, tied back to Parts 1 and 8.
- [ ] **RAG mini-demo.** Part 7 argues for RAG but never shows it. A toy demo —
  a few paragraphs chunked, a query, cosine-scored retrieval, the winning chunk
  pasted into a prompt template — would make it concrete.
- [ ] **Sampling beyond temperature.** Top-k / top-p truncation as an
  interactive addition to the Part 1 bigram demo (the text mentions them; the
  demo doesn't show them).
- [ ] **Fine-tuning in practice.** LoRA/QLoRA in one card: what adapters are,
  why they're cheap, when fine-tuning beats prompting (and when it doesn't).
- [ ] **Running models locally.** llama.cpp / Ollama / GGUF, what quantization
  actually does to weights (ties to the BitNet card), what fits on a laptop.
  Highly shareable with exactly this audience.
- [ ] **Evaluation literacy.** How to read benchmarks skeptically: saturation,
  contamination, the gap between leaderboard and use case. The frontier section
  ends with three questions for AI news; evals deserve the same treatment.
- [ ] **Multimodality.** One card: images/audio as tokens in the same
  transformer, why that works at all.

## Interactivity gaps

- [x] Weight visualization for the digit net (live diagram of nodes and
  weighted connections; activations flow as you draw).
- [x] Nearest-neighbor exploration in the embedding scatter (Part 4).
- [ ] **Glossary popovers.** Dotted-underlined technical terms ("perceptron",
  "softmax", "logits", "KV cache"…) with hover/tap definition cards and
  cross-links to the relevant Part. In progress.
- [ ] **Editable attention sentence.** Part 5's tokens are fixed because the
  Q/K/V vectors are hand-built. A constrained editor (swap nouns/adjectives
  from a word bank) could keep the vectors honest while adding play.
- [ ] **Real-tokenizer comparison.** Embed a few hundred GPT-2/cl100k merges to
  tokenize the user's input the way a production model actually would, next to
  the toy BPE.
- [ ] **Choose-your-own decoding.** Let the reader pick the next token in the
  hero demo occasionally, to feel the branching factor.

## Presentation & infrastructure

- [ ] **GitHub remote + Pages deployment** — a URL is much easier to share with
  friends/family than a file.
- [ ] **Offline fonts.** Google Fonts is the page's only network dependency;
  either embed WOFF2 subsets as data URIs or accept the system-font fallback.
- [ ] **Mobile pass.** The drawing canvas, wide tables, and the network diagram
  need a real phone check; `touch-action` is set but untested on devices.
- [ ] **Accessibility pass.** Keyboard operation of the custom controls (seg
  buttons, sliders are fine; canvas drawing has no keyboard path), ARIA labels
  audit, contrast check on `.dim` text.
- [ ] **Print/PDF stylesheet** for handing out; demos would need static
  fallback captions.
- [ ] **Presenter mode.** Speaker notes per section behind a `?presenter=1`
  flag, for using the page as a talk deck.
