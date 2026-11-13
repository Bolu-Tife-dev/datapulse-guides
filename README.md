# DataPulse Guides

Practical, no-fluff guides for bulk jobs that usually cost a subscription:
converting documents, generating codes at scale, and fixing images — for
cents, not $29/month.

**[DataPulse](https://datapulse-hazel.vercel.app)** is a pay-per-job bulk
engine: no subscription, no watermark, no "free trial that ends after 2
pages". Every new account starts with **$2.00 free credit** — enough to run
every guide below at least once before paying anything.

| Guide | Job | Real cost |
|---|---|---|
| [Convert 300 PDFs to Markdown for $1.50](guides/pdf-to-markdown-bulk.md) | Document → clean Markdown for LLM pipelines, Obsidian, docs sites | $0.05/page, capped at $1.50/doc |
| [Batch-generate 500 QR codes for $1](guides/bulk-qr-codes-from-csv.md) | CSV in → ZIP of print-ready PNGs out | $1.00 flat per batch of up to 500 |
| [Upscale a photo 4× for $0.30](guides/batch-image-upscaling.md) | 1×–4× AI upscaling, output up to 4096 px | $0.30/image |

## Why pay-per-job

Subscription tools price for the user who needs them daily. Most people need
them **twice a month**. DataPulse charges per completed job, debits a prepaid
wallet atomically, and keeps nothing after the job runs. Failed jobs are
refunded automatically.

## For developers: CI integration

The [datapulse-action](https://github.com/Bolu-Tife-dev/datapulse-action)
GitHub Action converts PDFs to Markdown on every push — self-tested on every
commit against the live API. There is also a plain REST endpoint for scripts
(PDF, QR, and image tools share the same wallet and API keys).

---

All prices in this repository reflect DataPulse's live pricing (verified
against the service itself). No affiliate links, no fake discounts — the
product is the link.
