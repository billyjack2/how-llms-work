# How LLMs actually work

A free, open-source, single-file interactive lesson on LLM internals — for
anyone curious enough to handle detail, no ML background assumed. It starts
simple (a digit classifier you train in your browser) and ends at the research
frontier.

**Read it live: <https://billyjack2.github.io/how-llms-work/>**

Everything lives in **`how-llms-actually-work.html`**. Open it in a browser;
that's the whole deployment story.

## What's inside

| Part | Topic | Live demo |
|------|-------|-----------|
| 00 | Intro | Animated next-token loop; from the second pass, the reader picks the next token |
| 01 | The core idea: predict the next token | Bigram sampler with temperature and top-k / top-p truncation (real counts, computed live) |
| 02 | Traditional ML, hands on | A 64→16→16→10 digit classifier that **trains in your browser** on the UCI handwritten-digits dataset (800 real samples: 650 train, 150 held out), with a drawable 8×8 canvas and a live network diagram of weights and activations |
| 03 | Tokenization | A BPE tokenizer trained from scratch in-page, side by side with a GPT-2-style production tokenizer (curated real-vocabulary subset) |
| 04 | Embeddings | 2-D scatter sketch of embedding space; hover/tap a word to light up its nearest neighbors |
| 05 | Attention | Scaled dot-product attention computed live on hand-built Q/K/V vectors; three heads, full matrix, causal mask; edit the sentence via role-preserving word swaps or type your own (a correctable rule-based tagger assigns roles) |
| 06 | The transformer, assembled | Architecture diagram with real residual paths and the autoregressive loop |
| 07 | Context windows | Cost calculator (n² comparisons, KV cache, GPU fit, MHA vs GQA), plus a fully-visible RAG pipeline demo |
| 08 | How a chatbot is made | Pretraining → SFT → RLHF/DPO → reasoning RL |
| 09 | Prompting | Editable prompt presets (zero-shot, few-shot, CoT, role); calls a live model inside claude.ai, falls back to canned responses elsewhere |
| 10 | Why models make things up | Hallucination mechanics, tied back to the softmax and training incentives |
| 11 | Agents & tool use | A pre-recorded agent loop you step through turn by turn, context growth included |
| 12 | The research frontier | Fourteen cards: MoE, reasoning RL, dual release, Mamba/SSMs, MLA/NSA/CSA, BitNet, diffusion LMs, byte-level models, interpretability, memory, speculative decoding, LoRA, local models, multimodality |
| 13 | Further reading | Linked, verified sources plus a capstone exercise |

Also built in: self-check quizzes at the end of each Part (answers behind
"show answer" reveals), glossary popovers on ~30 technical terms (hover or tap
the dotted underlines), a presenter mode with speaker notes (`?presenter=1`),
a print stylesheet that produces a clean PDF handout, and a social share card
(`og-image.png`, regenerable from `og-card.html`).

Design intent: every demo computes what it claims to compute — the digit net
really trains, the BPE merges are really learned, the attention softmax is real
arithmetic. Nothing is a mock except where labeled (the embedding scatter is a
hand-made sketch and says so).

## Viewing / presenting

- Double-click the file, or serve it (`python3 -m http.server`). No build step,
  no dependencies, and no network requests at all: fonts are embedded, so the
  page works fully offline.
- Part 09's "Run against a live model" only reaches the API when the page is
  viewed inside claude.ai; everywhere else it shows the pre-recorded fallback
  responses (by design — no API key ships with this file).

## Working on the file (read before editing)

- **It is one big HTML file on purpose** — portability is the feature. Inline
  CSS in `<head>`, one inline `<script>` before `</body>`. Keep it
  self-contained: no CDNs, no external JS.
- **Warning:** the inline script holds `const DIGIT_DATA="…"` (search for it;
  its line number drifts as the file grows), a ~51,000-character hex string
  (the training set), and an 800-char label string after it. Don't read those
  lines into an editor/agent context whole, and never reformat them.
- Design tokens are CSS variables at the top of the stylesheet (`--glow` teal
  accent, `--amber`, `--blue`, `--violet`; dark panel surfaces `#0E1621` /
  `#0A1119`, hairlines `#243449`). Demos are dark "instrument panels" on a light
  paper page; labels use JetBrains Mono via `.mini` / `.dim`.

### Verification recipe

1. Syntax-check the inline script:
   ```sh
   awk '/^<script>$/{f=1;next} /^<\/script>$/{f=0} f' how-llms-actually-work.html > /tmp/page.js
   node --check /tmp/page.js
   ```
2. Render with headless Chrome and *look at the screenshot*:
   ```sh
   "/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
     --headless=new --disable-gpu --window-size=1240,2400 \
     --virtual-time-budget=30000 --screenshot=out.png "file:///path/to/test.html"
   ```
   Caveats learned the hard way: anchor navigation and smooth scrolling do
   nothing under virtual time — to screenshot a mid-page section, append a
   script to a **test copy** that removes the sections above it and calls
   `window.scrollTo`. To catch runtime errors, append
   `window.addEventListener('error', e => { document.title = 'JSERR: ' + e.message; })`
   and grep `--dump-dom` output for `JSERR`.
3. Interactions can be driven in the test copy with dispatched `PointerEvent`s
   (the digit canvas, hover states) and `.click()` (buttons).

## Contributing

Corrections, better explanations, new demos, translations — all welcome via
issues and PRs. The bar for changes: demos must really compute what they claim
(no mocks unless labeled), claims should carry dates, and the page must stay a
single self-contained file.

## Roadmap

Ideas and known gaps live in [ROADMAP.md](ROADMAP.md).

## License

[MIT](LICENSE).
