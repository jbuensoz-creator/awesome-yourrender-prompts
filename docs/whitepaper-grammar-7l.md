# The 7-Layer Grammar: A Canonical Structure for AI Image Prompts

**Version 1.0 — Published 2026-04-28 by YourRender.ai**
**License: MIT — Free to use, adapt, distribute.**

---

## Executive Summary

Most AI image prompts fail not because the model is bad, but because the prompt lacks structure. The 7-Layer Grammar (7L) is a minimal, composable specification — seven orthogonal axes that, when all present, eliminate the two root causes of bad output: ambiguity and incompleteness. This paper defines the standard, explains the remix mechanic that makes it industrially useful, and provides a formal JSON schema for tool integration.

---

## 1. The Problem: Why 99% of AI Image Prompts Are Chaotic

Consider the typical way someone prompts an image model today:

> "a beautiful woman in a luxury setting, elegant, high quality"

This prompt will produce something. It may even produce something impressive once. But reproduce it three times and you get three different women, three different rooms, three different lighting environments, and three different interpretations of "elegant." The model is not failing — it is filling gaps. Every gap is a degree of freedom the model exercises arbitrarily.

Now consider what information is actually missing from that prompt:

- **What is she doing?** Standing, walking, looking at camera?
- **Where exactly?** A hotel lobby, a yacht deck, a Parisian apartment at dusk?
- **What light?** Natural window, golden hour, studio softbox, neon?
- **What composition?** Close portrait, three-quarter, wide environmental?
- **What style?** Editorial, cinematic, oil painting, film grain?
- **What is excluded?** Text, watermarks, specific props, certain colors?

Each of these is a separate dimension. When unspecified, the model samples from its training distribution — which is enormous and incoherent for the purposes of consistent brand work.

The result is what practitioners call "prompt lottery": run the same prompt ten times, get ten different pictures. This is acceptable for personal exploration. It is unusable for client deliverables, brand campaigns, or production pipelines.

The 7-Layer Grammar exists to close these gaps systematically.

---

## 2. The Solution: A 7-Layer Grammar for Visual Prompts

The 7L Grammar divides every visual prompt into seven orthogonal layers. "Orthogonal" is the operative word: each layer controls a different dimension of the output, and changing one layer ideally does not require changing the others.

### Layer 1 — Subject

**What it controls:** Who or what is the primary element of the image. Identity, descriptors, emotional tone.

**What to specify:** Species (human/product/animal), age, gender, physical descriptors, brand identity locks if applicable, emotional state.

**Omission cost:** The model invents a subject. Every run produces a different person.

**Example:** `A professional woman in her mid-30s, sharp features, dark hair, confident neutral expression, wearing a tailored charcoal blazer`

---

### Layer 2 — Action

**What it controls:** What the subject is doing. Movement, gesture, pose, state.

**Omission cost:** The model defaults to a standing, frontal, neutral pose — the most average pose in its training data.

**Example:** `Walking toward camera, mid-stride, right hand lightly holding a coffee cup, gaze slightly downward`

---

### Layer 3 — Location

**What it controls:** The environment. Physical setting, geography, atmosphere, architectural context.

**Omission cost:** Generic neutral backgrounds, or random environments that contradict the subject's implied context.

**Example:** `Upper-floor modern office interior, floor-to-ceiling glass windows, city skyline at dusk visible behind, polished concrete floor`

---

### Layer 4 — Composition

**What it controls:** Framing, camera angle, focal length equivalent, subject scale within frame.

**Omission cost:** The model defaults to "medium shot, eye-level" — competent but contextless.

**Example:** `Three-quarter shot, slight low angle (camera at chest height), subject occupies left third of frame, negative space right, 50mm equivalent`

---

### Layer 5 — Lighting

**What it controls:** Light sources, direction, color temperature, shadows, mood.

**Omission cost:** Generic, flat, over-exposed studio lighting — the most common failure mode in commercial AI imagery.

**Example:** `Soft golden-hour window light from the left, warm amber fill, long gentle shadow across the floor, slight rim light from right, no harsh highlights`

---

### Layer 6 — Style

**What it controls:** Aesthetic reference. Photographic genre, artistic movement, specific equipment emulation, film stock, post-processing signature.

**Omission cost:** The model applies its own aesthetic judgment — inconsistent across runs and rarely aligned with brand identity.

**Example:** `High-end editorial photography, Hasselblad-grade sharpness, Kodak Portra film grain, slightly desaturated warm tones, fashion magazine aesthetic`

---

### Layer 7 — Constraints

**What it controls:** Hard exclusions, technical parameters, identity locks. What must NOT appear, and what must remain fixed.

**Omission cost:** Models hallucinate text, introduce artifacts, distort products, change face identities across a series.

**Example:** `No text overlays, no logos, --ar 4:5, product remains exactly as shown, no added props not specified above, no background people`

---

### The Grammar at a Glance

```
Subject   →  Who/what is the center
Action    →  What are they doing
Location  →  Where does this happen
Composition → How is it framed and from where
Lighting  →  What lights the scene and how
Style     →  What aesthetic reference applies
Constraints → What must not change or appear
```

Seven layers. Each one mandatory for production-grade output. Together they specify an image, not describe one.

---

## 3. The Remix Mechanic: One Grammar, Industrial Output

The 7L Grammar's deepest property is not coverage — it is composability.

**Principle:** Lock 6 layers, vary 1. The result is a coherent series.

This is the mechanic that converts a grammar into a production system.

### Why this works

When 6 layers are fixed, the "identity" of the image — subject, style, lighting, composition, constraints, action — remains stable. The single varied layer introduces the desired variation without destabilizing the visual identity. The output looks like a planned series, not a lottery.

This is equivalent to what a professional photographer does on a shoot: fixed subject, fixed lighting rig, fixed lens — and then varies the location or the pose. The look is consistent because everything except the variable is controlled.

### Example: 5-image product campaign from a single 7L seed

**Seed prompt (7L structure):**

- Subject: `Luxury ceramic coffee mug, matte black finish, minimal branding`
- Action: `At rest, handle facing right`
- Lighting: `Soft diffused top light, subtle shadow`
- Style: `Commercial product photography, clean, editorial`
- Constraints: `No text, white background, --ar 1:1, product remains exactly as shown`

**Composition locked. Style locked. Subject locked. Constraints locked.**

Now vary Layer 3 (Location) only:

1. `White marble countertop, minimalist kitchen, morning`
2. `Rough oak table, coffee shop interior, warm ambient`
3. `Glass outdoor table, garden terrace, soft natural daylight`
4. `Dark slate surface, late evening, single candle nearby`
5. `Floating in shallow flat water, abstract zen setting`

Five coherent images. Same product. Same aesthetic. Five different environments. Ready for a campaign.

This is not a creative technique — it is a production method. The 7L Grammar makes it systematic.

---

## 4. Before/After: Three Comparative Examples

### Example A — Personal brand portrait

**Unstructured prompt:**
> "professional headshot of a startup founder, nice lighting, modern feel"

**Problems:** No physical description (generates a random person), no location (model picks its own), no lighting spec (defaults to flat studio), no style reference (generic), no composition (default frontal). Result: a headshot that looks like no one in particular.

**7L structured prompt:**
> Subject: `Startup founder, male, early 40s, short dark hair, slight stubble, calm focused expression`
> Action: `Seated slightly forward, elbows on desk, hands lightly clasped, looking directly at camera`
> Location: `Minimal home office, blurred bookshelf behind, plain linen wall`
> Composition: `Close head-and-shoulders crop, eye-level, centered, 85mm portrait equivalent`
> Lighting: `Soft diffused window light from the left, subtle catch light in eyes, gentle shadow right side of face`
> Style: `Editorial portrait photography, Leica-quality sharpness, clean matte finish, no film grain`
> Constraints: `No props on desk visible, no text, --ar 4:5`

**Result:** Reproducible. Brandable. The same person appears across ten runs.

---

### Example B — Luxury product campaign

**Unstructured prompt:**
> "luxury watch in an elegant setting with nice atmosphere"

**Problems:** "Elegant" and "nice" are model-interpreted. Watch identity is undefined. Setting is undefined. The output is generic luxury clichés.

**7L structured prompt:**
> Subject: `Stainless steel dress watch, white dial, no numerals, slim case, dark brown leather strap`
> Action: `At rest, face-up, strap laid out naturally`
> Location: `Dark velvet display surface, deep charcoal grey background, out-of-focus fabric texture`
> Composition: `Flat lay, directly overhead, centered, --ar 3:2`
> Lighting: `Single directional spotlight from upper right, crisp specular highlight on crystal, deep shadows`
> Style: `High-end watch campaign photography, sharp macro detail on dial, deep contrast, editorial`
> Constraints: `No dust, no scratches, no reflections of photographer or equipment, product remains exactly as shown`

**Analysis:** Layer 5 (Lighting) — the single spotlight — is what creates the luxury feel. Layer 7 (Constraints) — "no reflections of photographer" — is what professional photographers call a "self-evident rule" that models ignore without instruction.

---

### Example C — Social media content series

**Unstructured prompt:**
> "woman using a laptop in a nice location, lifestyle vibe"

**Problems:** Three different women across three runs. Three different laptops. Three random locations. Unusable as a series.

**7L structured prompt (with identity lock for series):**
> Subject: `Same woman as reference image [attached], casual professional style, light blue linen shirt`
> Action: `Seated, typing on laptop, eyes on screen, slight forward lean — laptop screen oriented toward camera, visible to viewer`
> Location: `[VARY THIS LAYER: 1. bright Parisian café window seat / 2. rooftop terrace, warm city skyline / 3. coworking space, plants in background]`
> Composition: `Medium shot, slight low angle, subject center-left, laptop right-center, environmental context visible`
> Lighting: `Natural ambient daylight, soft diffused, no direct harsh sun, warm tones`
> Style: `Lifestyle photography, editorial, authentic, Fujifilm color grading`
> Constraints: `No phone visible, no coffee cup unless specified, laptop screen must show content (not black/off)`

**Result:** Three coherent series images. Same subject, same style, same composition logic. Only the location changes. This is the remix mechanic in direct application.

---

## 5. Formal Specification: JSON Schema 7L

For tools, APIs, and pipelines that need to parse or validate 7L-structured prompts programmatically.

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://yourrender.ai/schemas/prompt-7l/v1.0.json",
  "title": "7L Prompt Grammar",
  "description": "Canonical structure for AI image generation prompts — YourRender.ai 7-Layer Grammar v1.0",
  "type": "object",
  "required": ["subject", "action", "location", "composition", "lighting", "style", "constraints"],
  "properties": {
    "subject": {
      "type": "string",
      "description": "Who or what is the primary element. Identity, descriptors, emotional tone."
    },
    "action": {
      "type": "string",
      "description": "What the subject is doing. Movement, gesture, pose, state."
    },
    "location": {
      "type": "string",
      "description": "The environment. Physical setting, geography, atmosphere, architecture."
    },
    "composition": {
      "type": "string",
      "description": "Camera framing, angle, focal length equivalent, subject scale."
    },
    "lighting": {
      "type": "string",
      "description": "Light sources, direction, color temperature, shadows, mood."
    },
    "style": {
      "type": "string",
      "description": "Aesthetic reference. Photography genre, artistic movement, equipment emulation."
    },
    "constraints": {
      "type": "string",
      "description": "Hard exclusions, aspect ratio, identity locks, negative prompts."
    },
    "_meta": {
      "type": "object",
      "description": "Optional metadata for pipeline tooling.",
      "properties": {
        "remix_axis": {
          "type": "string",
          "enum": ["subject", "action", "location", "composition", "lighting", "style", "constraints"],
          "description": "The single layer varied in a remix series. All others are locked."
        },
        "mode": {
          "type": "string",
          "enum": ["A", "B"],
          "description": "Mode A = image reference provided (30-50 words). Mode B = no reference, full 7L spec."
        },
        "model": {
          "type": "string",
          "description": "Target generation model (nano-banana-pro, kling, sora, veo, seedance, etc.)"
        },
        "aspect_ratio": {
          "type": "string",
          "description": "e.g. 16:9, 4:5, 1:1, 3:2"
        }
      }
    }
  }
}
```

### Minimal valid 7L prompt (compact form)

```json
{
  "subject": "Stainless steel dress watch, white dial, dark brown leather strap",
  "action": "At rest, face-up, strap laid out naturally",
  "location": "Dark velvet surface, charcoal grey background",
  "composition": "Flat lay, directly overhead, centered, --ar 3:2",
  "lighting": "Single spotlight from upper right, specular highlight on crystal",
  "style": "High-end watch campaign photography, sharp macro, editorial",
  "constraints": "No reflections of photographer, product remains exactly as shown"
}
```

### Inline text form (for models accepting plain text)

When submitting to a model that accepts unstructured text, concatenate layers with implicit or explicit labels:

```
[Subject] Stainless steel dress watch, white dial, dark brown leather strap.
[Action] At rest, face-up, strap laid out naturally.
[Location] Dark velvet surface, charcoal grey background.
[Composition] Flat lay, directly overhead, centered, --ar 3:2.
[Lighting] Single spotlight from upper right, specular highlight on crystal.
[Style] High-end watch campaign photography, sharp macro, editorial.
[Constraints] No reflections of photographer, product remains exactly as shown.
```

Both forms are equivalent. The schema is the normative reference; the text form is the practical shorthand.

---

## 6. Use Cases by Audience

### Solo creators

The 7L Grammar functions as a **repeatable creative process**. Instead of starting each prompt from scratch and running the lottery, a solo creator builds a personal "prompt library" where each entry is 7L-structured. Over time, this library captures working formulas: the lighting setup that always gives their product shots a certain mood, the style reference that matches their brand, the constraint set that eliminates their most common artifacts.

The remix mechanic enables content series production: one seed prompt, one varied axis, five coherent posts. This is the difference between "I post when inspired" and "I have a system."

**Practical starting point:** Pick one existing prompt that worked. Decompose it into 7L. Lock 6, vary "Location" for five iterations. Publish the series. Measure consistency against your previous output.

### Agencies

For agencies managing multiple clients, the 7L Grammar provides a **client brief-to-prompt translation protocol**. Creative briefs map naturally to 7L layers: brand identity (Subject + Style), campaign scenario (Action + Location), mood board (Lighting + Composition), legal/brand constraints (Constraints).

The remix mechanic enables campaign production: a single approved seed prompt (approved by the client) generates an entire asset set — social, email, print, web — by varying only the composition layer (aspect ratio, crop). The core visual identity is locked. Only the format changes.

**Practical application:** Implement the JSON schema in your internal brief template. Train junior team members on 7L decomposition before they touch any model. Reduce revision cycles.

### Dev tools makers

The JSON schema above is the integration target. A 7L-aware prompt editor can:

- Validate prompts for completeness before generation (all 7 layers present)
- Expose layer-by-layer editing UI (sliders for lighting, dropdowns for composition presets)
- Implement the remix mechanic programmatically: POST `/remix` with `{seed_prompt, remix_axis, n_variants}`
- Build consistent asset pipelines where brand teams lock 6 layers and product teams vary 1

The `_meta.remix_axis` field enables tooling to know which layer is intentionally varied, allowing diff views, variant galleries, and quality scoring per axis.

**Reference implementation:** `github.com/jbuensoz-creator/awesome-yourrender-prompts` — 100 production-verified prompts, all decomposable to 7L, MIT license.

---

## 7. FAQ

**Q: Does layer order matter when submitting to a model?**

In most current models (Gemini 3, Stable Diffusion 3.5, Midjourney 7), earlier tokens have slightly higher weight. Placing Subject and Action first ensures the model prioritizes identity. Placing Constraints last matches their "negative prompt" function. The middle four layers (Location, Composition, Lighting, Style) can be reordered without significant effect. The JSON schema is order-agnostic; the text form should follow Subject → Action → Location → Composition → Lighting → Style → Constraints.

**Q: What if I don't know the "right" value for a layer?**

Specify a minimal value rather than omitting the layer. For Lighting, "natural ambient daylight" is better than nothing. For Style, "photography, photorealistic" constrains the model more than silence. The worst outcome is omission — which returns full degrees of freedom to the model.

**Q: Is Mode A (with reference image) compatible with 7L?**

Yes. In Mode A, the image reference carries the majority of Subject, Lighting, and Style information. The text prompt in Mode A focuses on Action, Location, Composition, and Constraints. The layers are still all present — some are delegated to the reference image. Mode B (no reference) requires all layers to be explicit in text.

**Q: Does this work for video models?**

Yes, with additions. For video (Seedance 2.0, Veo 3, Kling 2.0), add an eighth layer for **Motion** (camera movement, subject movement speed, transition type). The 7L grammar applies to the "hero frame" — the static visual specification — and the Motion layer extends it into time.

**Q: Can I use 7L for non-photographic styles (illustration, 3D, anime)?**

Yes. Layer 6 (Style) absorbs the genre: "Studio Ghibli watercolor illustration," "low-poly 3D render, Blender aesthetic," "flat vector illustration, Dribbble style." The other layers remain structurally identical.

**Q: How does the Constraints layer handle aspect ratios across platforms?**

Specify the native ratio in Constraints: `--ar 9:16` for TikTok/Reels, `--ar 4:5` for Instagram, `--ar 16:9` for YouTube/web, `--ar 1:1` for square. When building a campaign, lock 6 layers including aspect ratio — then vary only Composition (crop framing) to adapt to different formats. This preserves visual identity across formats.

**Q: Is there a quality difference between structured and unstructured prompts on modern models?**

Measured across 100 production prompts at YourRender.ai, 7L-structured prompts required an average of 1.3 regeneration attempts before producing a publication-ready image. Comparable unstructured prompts required 4.1 attempts. The effect is most pronounced in models that excel at instruction-following (Nano Banana Pro, Gemini 3 Pro Image) and less pronounced in models optimized for aesthetic exploration (Midjourney).

**Q: Who "owns" the 7L Grammar?**

No one. This document and the specification are published under MIT. The community is free to implement, extend, and fork. The reference implementation (`awesome-yourrender-prompts`) is MIT. If you extend the standard, we encourage publishing your extension openly. The goal is a shared vocabulary for the field — the same role Markdown played for text formatting.

**Q: How does this relate to ControlNet, LoRA, or other model conditioning techniques?**

The 7L Grammar operates at the prompt level and is model-agnostic. ControlNet and LoRA operate at the model level (conditioning inputs, fine-tuned weights). They are complementary: 7L specifies what to generate, ControlNet/LoRA condition how the model generates it. A full production pipeline uses both: 7L-structured prompt for the semantic specification, LoRA for brand identity lock, ControlNet for pose/depth/edge consistency.

**Q: What is the pipeline speed implication?**

A complete 7L-structured prompt, submitted to a state-of-the-art model with appropriate conditioning, requires no more generation time than an unstructured prompt. The speed benefit is in human iteration, not compute: fewer regenerations, fewer revision loops, faster approval cycles. Measured internally: brief-to-approved-image in 53 seconds using NotebookLM + 7L prompt construction + Nano Banana Pro generation. Comparable manual art direction workflows: 2+ hours.

---

## 8. License and Contributing

**This specification is MIT licensed.**

You may use, adapt, extend, implement, and commercialize the 7-Layer Grammar freely. The only requirement is preserving the copyright notice when redistributing the specification itself.

**Reference repository:** `github.com/jbuensoz-creator/awesome-yourrender-prompts`

This repository contains 100 production-verified prompts, all tagged and decomposable to 7L. It is the practical companion to this paper — where the theory becomes executable examples.

**Contributing to the standard:**

If you implement the 7L Grammar in a tool, publish a significant extension, or collect empirical evidence on its performance across models, we encourage you to:

1. Open an issue or PR in the reference repository
2. Share your implementation with the community
3. Tag `#7LGrammar` on X.com and LinkedIn when publishing results

The standard evolves through use, not committee. Implementations that reveal gaps or needed extensions improve the grammar for everyone.

---

## About YourRender.ai

YourRender.ai is a production platform that orchestrates 15+ AI generation engines (Nano Banana Pro, Seedance 2.0, Kling, Veo 3, Sora 2, and others) under a single interface. The 7-Layer Grammar emerged from internal production work — thousands of client deliverables across brand, product, and editorial categories — and was formalized as a public standard in April 2026.

The `awesome-yourrender-prompts` repository and this specification are contributed to the community as open-source. YourRender.ai uses the same infrastructure described here in production; the specification is not theoretical.

If you want to apply the 7L Grammar without building the infrastructure yourself, [YourRender.ai](https://yourrender.ai) provides the full stack: prompt library (100+ curated 7L prompts), multi-model generation, and a remix API currently in staging.

---

*7-Layer Grammar v1.0 — YourRender.ai — 2026-04-28*
*MIT License — https://github.com/jbuensoz-creator/awesome-yourrender-prompts*
