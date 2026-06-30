# RDM project page

Static project website for **Representation Distribution Matching for One-Step Visual Generation**.
Single self-contained `index.html` (inline CSS + JS), plus an `assets/` folder. No build step.

## Preview locally

```bash
cd website
python3 -m http.server 8731
# open http://localhost:8731
```

## Before publishing, fill in these placeholders

All currently point to `#` and show a "link coming soon" hint when clicked.
Search `index.html` for `data-link` and replace the four `href="#"` values:

- `data-link="paper"`  → the paper PDF / OpenReview URL
- `data-link="arxiv"`  → the arXiv abstract URL
- `data-link="code"`   → the code repository URL

Other things you may want to edit:
- **Venue tag** "ICLR 2026" appears in the hero eyebrow and the footer. Change if the
  status is "Under review" or a preprint.
- **BibTeX** key `feng2026rdm` and the `booktitle` in the citation block.
- **Open Graph image** `<meta property="og:image">` in `<head>` (currently `assets/samples/sample-12.jpg`).

## Assets

- `assets/samples/sample-01..12.jpg` — top hero marquee. Cherry-picked one-step FLUX samples (from `promo/`).
- `assets/samples-bottom/sample-01..12.jpg` — bottom gallery. A second cherry-picked set (from `promo_bottom/`).
- `assets/figs/teaser.jpg` — paper teaser (FLUX 4-step vs 1-step + performance curve).
- `assets/figs/dino_overfit.jpg` — single-encoder gaming figure.
- `assets/cmp/teacher-01..48.jpg`, `student-01..48.jpg` — the 48 head-to-head pairs
  (4-step teacher vs our 1-step), extracted from `promo_aesthetic_teacher_vs_1step_v2.html`.
  `assets/cmp/pairs.json` holds the per-pair theme, prompt, and PickScore.

## Pages

- `index.html` — the project page. The "Our one step vs the four-step teacher" section shows 6
  curated pairs and links to:
- `comparisons.html` — standalone page with all 48 pairs grouped by theme. Regenerate it from the
  extracted images with `scratchpad/gen_compare.py` if the pair set changes.

The two sample sets are independent: the top marquee and bottom gallery read from different
folders, so you can swap either without touching the other (`var samples` vs `var galSamples`
in the inline script).

## Deploy

Any static host works. For GitHub Pages, push the contents of `website/` to a `gh-pages`
branch (or set Pages to serve `/website`). The page is fully static and needs no server.

## Design notes

Dark "measurement instrument" aesthetic: the generated images carry all the saturated color,
the UI stays near-monochrome. The signature element is the **distance-to-real ruler** that turns
the `SW r14` metric (real data = 1.00) into a structural device. Type is Space Grotesk (display)
+ Space Mono (every number and label) + Inter (body). Amber = real/target, blue = generated,
carried from the paper's own method figure. Copy follows the paper's no-dashes style rule.
