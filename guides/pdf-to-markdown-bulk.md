# Convert 300 PDFs to Markdown for $1.50 — no subscription, no Adobe

You found this page because you have a folder of PDFs and you want Markdown:
for an LLM/RAG pipeline, an Obsidian vault, a docs site, or because copy-paste
from a PDF gives you broken line breaks and phantom page numbers.

Here's the honest math on every route, then the $1.50 route.

## Your options, priced honestly

| Route | What it really costs |
|---|---|
| Manual copy-paste | 300 PDFs × 2–5 min of cleanup = **days** |
| Adobe Acrobat Pro | **$19.99+/month**, and batch export needs the desktop app |
| "Free" online converters | Free for 2 pages, then $9–20/month, and your files sit in their cloud |
| Write a pipeline yourself | pdfplumber/PyMuPDF is free but you'll spend a weekend on headers, footers, page numbers, hyphenation and list detection |
| **DataPulse** | **$0.05/page, capped at $1.50 per document.** A 300-page document = $1.50. Ten 30-page documents = $1.50. |

New accounts get **$2.00 free credit** — a 300-page document converts for
free, and you'll still have $0.50 left.

## What "clean Markdown" means here

The converter is tuned for real-world documents, not clean-born PDFs:

- Running heads and footers repeated on most pages are **dropped**
- Standalone page numbers are **removed**
- Hyphenated line-breaks are **rejoined** (`conver- sion` → `conversion`)
- ALL-CAPS lines, numbered headings (`3.2 Something`), and `Chapter/Section`
  lines become **Markdown headings**
- Bullets (`-`, `•`, `·`) and numbered lists are **rebuilt** as proper lists

Limits: 500 pages and 15 MB per document; larger files need splitting.

## Route 1 — drag and drop (no code)

1. Sign up at [datapulse-hazel.vercel.app](https://datapulse-hazel.vercel.app)
   — you get $2.00 credit, no card required.
2. Open the **PDF → Markdown** tool, drop your PDF, submit.
3. Download the `.md` file. Pages → one document; headings/lists preserved.

## Route 2 — GitHub Actions (runs on every push)

If your PDFs live in a repo (specs, manuals, papers), this converts them in
CI and commits the Markdown:

```yaml
steps:
  - uses: actions/checkout@v4
  - name: Convert PDFs to Markdown
    uses: Bolu-Tife-dev/datapulse-action@main
    with:
      api-key: ${{ secrets.DPULSE_API_KEY }}
      files: "docs/manual.pdf specs/*.pdf"
      output-dir: markdown
```

Setup and key minting are in the
[action's README](https://github.com/Bolu-Tife-dev/datapulse-action#usage).
The Action is self-tested on every commit against the live API — the badge on
that repo is green or it isn't.

## Route 3 — one curl call

The same engine is a REST endpoint. Mint an API key (see the Action README),
then:

```bash
curl -X POST https://datapulse-hazel.vercel.app/api/tools/pdf-markdown/run \
  -H "Authorization: Bearer dpk.YOUR.KEY" \
  -F "pdf=@report.pdf" \
  -o report.md
```

The response is the Markdown itself; the `X-Remaining-Balance` header tells
you what your wallet holds. If the wallet is empty you get HTTP 402 with the
exact shortfall — top up via Paystack (cards accepted) and retry.

## For 300 separate files

Loop it:

```bash
for f in pdfs/*.pdf; do
  curl -X POST https://datapulse-hazel.vercel.app/api/tools/pdf-markdown/run \
    -H "Authorization: Bearer dpk.YOUR.KEY" \
    -F "pdf=@$f" -o "markdown/$(basename "${f%.pdf}").md"
  sleep 2
done
```

300 × 30-page documents at $1.50 flat each = **$450**? No — **$0.05/page × 30
= $1.50 each only if they're exactly 30 pages.** A 30-page document costs
$1.50 because of the cap: 30 × $0.05 = $1.50. A 10-page document costs $0.50.
300 ten-page documents cost **$150** — less than three months of Acrobat,
with no subscription left over afterwards.

If a conversion fails after charging (server error mid-job), the wallet
refunds automatically. Insufficient balance never charges you.

---

[DataPulse](https://datapulse-hazel.vercel.app) — the Micro-SaaS Bulk Engine.
Pay per job, keep your files, cancel nothing.
