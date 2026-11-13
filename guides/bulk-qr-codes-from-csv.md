# Batch-generate 500 QR codes for $1 (from a CSV) — no watermark, no "pro plan"

Every bulk QR generator has a trap: the free tier stamps its logo on your
codes, caps you at 10–20 codes, or expires your "dynamic" codes after 14
days. For event tickets, product labels, table tents or asset tags, that's
useless — you need **hundreds of static, permanent, print-ready codes**.

Here's the $1.00 way: a CSV in, a ZIP of PNGs out.

## The math

| Route | Real cost |
|---|---|
| Free online generators | 10–20 codes free, then watermark + $10–30/month |
| Dynamic QR SaaS | $15+/month **forever**, codes die if you stop paying |
| Python (`qrcode` + pandas) | Free, ~30 lines, but you own the styling edge-cases forever |
| **DataPulse** | **$1.00 flat per batch — up to 500 codes.** One batch of 500 = $1.00. 100 codes = $1.00 (flat rate). |

With the **$2.00 free credit** every new account gets, you can run two full
500-code batches before paying anything.

## Step by step (no code)

1. Make a CSV. First column is the label/file name, the row is the content
   (URL, text, whatever). Headers are optional:

   ```csv
   label,contents
   table-01,https://yourmenu.example.com/t/01
   table-02,https://yourmenu.example.com/t/02
   asset-1001,ASSET-1001|WIDGET-A|2026-06
   ```

2. Sign up at [datapulse-hazel.vercel.app](https://datapulse-hazel.vercel.app)
   ($2.00 credit, no card).
3. Open the **QR generator** tool, upload the CSV, submit.
4. Download `datapulse-qr-codes.zip` — every row becomes a PNG named after
   its label. Print at any size; QR PNGs scale losslessly for typical print
   runs.

Static codes only: the content is baked into the code, so it works forever
and nothing expires. If you need click analytics you want dynamic codes —
this isn't that, and doesn't pretend to be.

## Step by step (one curl call)

Mint an API key (see the
[datapulse-action README](https://github.com/Bolu-Tife-dev/datapulse-action)
for the one-liner), then:

```bash
curl -X POST https://datapulse-hazel.vercel.app/api/tools/qr-generator/run \
  -H "Authorization: Bearer dpk.YOUR.KEY" \
  -F "file=@batch.csv" \
  -o qr-codes.zip
```

The `X-QRCodes-Count` header confirms how many codes were generated; the
`X-Remaining-Balance` header shows your wallet after the batch.

Limits: 500 entries per batch, 2000 characters per entry. Need 5000? Run ten
batches — $10, or split across two weeks of the free credit if you're
cheeky.

## Cost sanity check

- 500 table-tent codes: **$1.00**
- The same job on a typical "premium QR" plan: $15–25/month, forever
- One-time print run of asset labels: DataPulse is ~2% of the SaaS price and
  there's nothing to cancel afterwards

---

[DataPulse](https://datapulse-hazel.vercel.app) — the Micro-SaaS Bulk Engine.
Pay per job. Codes never expire because they were always yours.
