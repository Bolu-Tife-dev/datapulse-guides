# Upscale a photo 4× for $0.30 — when "AI upscaler" sites want $19/month

You have a small or soft image — an old scan, a cropped screenshot, a product
photo the client sent at 800px — and you need it usable at 3000+ px. Every
"free AI upscaler" site wants an account, a watermark removal fee, or a
monthly plan.

DataPulse upscales 1×–4× (output capped at 4096 px on the longest side) for
**$0.30 per image**, with preprocessing that decides how aggressive to be
based on how soft your source actually is.

## The math

| Route | Real cost |
|---|---|
| "Free" upscaler sites | Watermarked output; paid tiers $10–29/month |
| Photoshop Super Resolution / enhance | Part of a $22.99+/month subscription |
| Local (Real-ESRGAN etc.) | Free, but you need a GPU and an afternoon of setup |
| **DataPulse** | **$0.30/image, no account extras, output up to 4096 px** |

The **$2.00 free credit** on signup = **6 images free** before you pay
anything.

## What it does to your image

Not a plain resize. The tool measures the sharpness of your input
(Laplacian variance) and adapts:

- **Very soft / blurred sources** get a restoration pass first (up to a full
  restore level), then upscale — this rescues old scans and low-bitrate
  screenshots
- **Normal photos** get a standard enhancement pass
- **Already crisp sources** skip heavy processing — upscale only
- The scale factor is capped so the output never exceeds 4096 px on the
  longest side (inputs must be under 40 MP and below 4096 px input side)

Output is a PNG, attachment-disposition, ready to download or wire into a
script.

## Step by step (no code)

1. Sign up at [datapulse-hazel.vercel.app](https://datapulse-hazel.vercel.app)
   — $2.00 credit, no card.
2. Open the **Image Upscaler** tool, drop your image, submit.
3. Download the upscaled PNG. Repeat for each image; the wallet shows the
   running cost ($0.30 each) and remaining balance.

## Step by step (one curl call)

Mint an API key (see the
[datapulse-action README](https://github.com/Bolu-Tife-dev/datapulse-action)
for the one-liner), then:

```bash
curl -X POST https://datapulse-hazel.vercel.app/api/tools/image-upscaler/run \
  -H "Authorization: Bearer dpk.YOUR.KEY" \
  -F "image=@photo.jpg" \
  -o photo-upscaled.png
```

`X-Remaining-Balance` tells you your wallet after the job.

## When this is the wrong tool

- **Posters larger than 4096 px** — split into tiles or use a dedicated
  print workflow
- **Heavily damaged photos** needing generative fill — that's a different
  (and much more expensive) class of model
- **Bulk of 10,000 images daily** — at that point run your own GPU pipeline;
  $0.30 × 10k/day is Real-ESRGAN money, not SaaS money

For everything else — client photos, scans, marketplace images, old
screenshots — $0.30 beats a subscription you'd use twice.

---

[DataPulse](https://datapulse-hazel.vercel.app) — the Micro-SaaS Bulk Engine.
Pay per job, sharp pictures, no watermark.
