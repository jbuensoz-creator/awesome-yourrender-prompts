# Contributing to Awesome YourRender Prompts

Thanks for your interest in contributing. This collection lives by one principle: **every prompt must produce publication-ready output**.

## How to submit a prompt

1. Fork this repository
2. Add your prompt to the appropriate category file in `prompts/<category>.json`
3. Use this exact JSON structure:

```json
{
  "id": <next-available-int>,
  "title": "Short descriptive name",
  "content": "The actual prompt text",
  "description": "What this prompt produces (1-2 sentences)",
  "sourceMedia": ["https://example.com/preview.jpg"],
  "needReferenceImages": false
}
```

4. Open a Pull Request with:
   - **Title**: `[<category>] <short prompt name>`
   - **Body**: link to a sample output you generated, and which model(s) it was tested on

## Quality bar

Before submitting, verify:

- ✅ The prompt **produces a clean output on the first or second try** — no "lucky" outputs
- ✅ At least **one preview image is hosted publicly** in `sourceMedia`
- ✅ Tested on at least **2 of the major models** (Nano Banana Pro, Seedance 2.0, Veo 3, Kling, Sora 2)
- ✅ The output is **publication-ready** — meaning a marketing team or content creator could ship it as-is
- ✅ No copyrighted characters, brands, or living individuals (unless explicitly licensed)

## What gets rejected

- Prompts that produce "interesting experiments" but not publishable output
- Prompts that only work on one specific model with one specific seed
- Low-effort dumps from other public collections (we already have those — see `references/` in our parent skill)
- Prompts with no preview image
- Prompts produced by an AI tool's "auto-enhance" feature without human curation

## What gets prioritized

- Prompts tested on **real client deliverables** (with permission to share)
- Prompts that work across **multiple AI models** (model-agnostic)
- Prompts with **editable variables** (e.g., `[PRODUCT]`, `[SCENE]`) that make them reusable
- Prompts that fit the **YourRender.ai 7-Step methodology** (Concept → Design → Publish → Empire → Studios → Public → Client Success)

## Recognition

Every accepted contribution is credited with the author's GitHub handle in the prompt's metadata. Top contributors get featured in the [YourRender.ai blog](https://yourrender.ai/blog) and on our social channels.

## Questions?

Open an issue or reach out at [hello@yourrender.ai](mailto:hello@yourrender.ai).

— *The YourRender.ai team*
