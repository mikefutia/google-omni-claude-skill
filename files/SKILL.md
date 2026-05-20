---
name: flow-ugc-ads
description: Generate multi-shot UGC video ad production packages for Google Flow. Takes a product image plus an ad angle and outputs everything needed to run a full production session in Flow's Agent mode: a realistic creator image prompt, asset-tagged shot prompts, the full dialogue script, a single Agent briefing instruction, and an ElevenLabs voiceover script. Use whenever the user wants to create a UGC ad in Google Flow, generate a creator-style video ad, or turn a product photo into a multi-shot vertical ad without using an API. Also trigger on phrases like "Flow UGC ad," "Google Flow ad," "Flow production package," or when the user drops a product image and mentions Flow or Gemini Omni.
---

# Google Flow UGC Ad Generator

Generates complete production packages for multi-shot UGC video ads in Google Flow. One product image plus one ad angle produces everything the user needs to run a full Agent mode session in Flow — creator prompt, shot list, tagged prompts, Agent instruction, and voiceover script.

## What this skill does

1. Takes a product image path and ad angle from the user
2. Optionally reads `brand/brand-dna.md`, `brand/brand-voice.md`, `brand/icp-cards.md` if they exist — skips silently if not
3. Generates a realistic AI creator image prompt optimized for ChatGPT Images 2.0 or Nano Banana Pro
4. Writes a 5-shot direct response script with dialogue for each scene
5. Produces five asset-tagged Flow prompts ready to paste directly into Flow
6. Writes a single Agent mode briefing instruction covering the full production session
7. Produces an ElevenLabs-ready voiceover script for post-production audio

This skill does NOT call any APIs. It produces the production package. The user runs the actual generation in Flow's browser UI.

## Before you start

The user needs:
- A Google AI Pro subscription ($19.99/month) at labs.google.com/flow
- A product image saved locally (JPG or PNG)
- Optionally: an existing creator image, or they generate one using the character prompt this skill outputs

No API keys. No code. No terminal. This is a UI tool.

## Workflow

### Step 1 — Intake

Collect from the user:

1. **Product image** — file path or description (required)
2. **Product name + one-line description** — if not provided, ask
3. **Ad angle** — pick one or ask:
   - `testimonial` — creator speaks to camera about results (default)
   - `car/on-the-go` — creator in car or commuting, convenience angle
   - `unboxing` — creator reveals and reacts to product
   - `lifestyle-demo` — creator using product in natural environment
   - `problem-solution` — before state, product intro, after state
4. **Creator description** — brief description (age, gender, vibe). If not provided, default to: "27-year-old woman, relatable fitness-oriented, not model-perfect"
5. **Brand/product category** — supplement, beauty, apparel, food/bev, home goods, etc. Informs which angle and which creator archetype fits best.

Do not ask for everything at once. Product image + angle is enough to start. Ask for missing details naturally.

### Step 2 — Check for brand context

Look for:
- `brand/brand-dna.md`
- `brand/brand-voice.md`
- `brand/icp-cards.md`

If any exist, read them silently. Use them to sharpen dialogue voice and ICP targeting. Do not mention this to the user. If none exist, proceed — this skill works with just a product image.

### Step 3 — Generate the creator image prompt

Output a character image prompt the user can paste into ChatGPT Images 2.0 or Nano Banana Pro.

Follow this formula exactly:

```
Candid iPhone photo of a [age]-year-old [gender], [specific physical detail — hair color/texture with natural flyaways, freckles or not, etc.], [minimal/natural/no] makeup, wearing [specific casual outfit — real clothing, not "stylish"], [environment detail — sitting in car / standing in kitchen / etc.]. Shot from [slight angle — low angle slightly off-center / slightly above eye level]. [Specific lighting — soft overcast daylight through window / warm morning kitchen light / overhead fluorescent in gym]. Slightly imperfect exposure. Real, unretouched skin texture. Natural hair flyaways. No studio lighting. Editorial-style realism.
```

Rules:
- Never use "beautiful," "gorgeous," "stunning," or model-descriptors
- Always include a specific environment, even in the character reference shot
- Always include at least one deliberate imperfection (flyaways, freckles, uneven lighting)
- Always include "Candid iPhone photo" — one of the strongest realism signals
- Match the creator archetype to the product category (see `references/characters.md`)

Tell the user: save the generated image as `creator.png` and upload it to their Flow project along with their product image. Both filenames should be descriptive: `creator.png` and `[product-name].jpg`.

### Step 4 — Write the 5-shot DR script

For the chosen angle, write a complete shot list. Each shot gets:

```
Shot N/5 — [Shot name]
Environment: [where the creator is — specific room/setting/context]
Action: [exactly what's happening — one action only per shot]
Product in frame: [yes/no — and if yes, how]
Dialogue: [what the creator says — ~3 words per second, UGC voice]
```

**Direct response structure (default — testimonial angle):**

| Shot | Job | Environment | Product |
|------|-----|-------------|---------|
| 1 — Hook | Stop the scroll with a single claim | Kitchen / bathroom / neutral | Yes — held toward camera |
| 2 — Problem | Make the viewer feel the pain | Bedroom / desk / car | No |
| 3 — Discovery | Introduce the product naturally | Kitchen / bathroom | Yes — opening/interacting |
| 4 — Transformation | Show the result. Specific, not vague | Gym / outdoors / work | No |
| 5 — CTA | One action, remove friction | Back to Shot 1 environment | Yes — held toward camera |

**Dialogue rules:**
- UGC voice: "Okay I need to talk about this" not "Introducing our new product"
- ~3 words per second of screen time. A 7-second shot = ~21 words max
- First line is the hook — must work without sound (captions carry it on autoplay)
- Product name appears in Shot 3 or later, never Shot 1
- CTA is punchy: "link is below" / "you literally have nothing to lose" — never "shop now" or "buy today"
- If `brand/brand-voice.md` was loaded, mirror its sentence patterns

See `references/angles.md` for shot-by-shot breakdowns of all five preset angles.

### Step 5 — Write the asset-tagged Flow prompts

For each shot, produce a prompt ready to paste into Flow. Every prompt tags both the creator image and the product image by filename.

**Prompt structure:**

```
Vertical UGC video, [creator.png] [environment + outfit detail], [action]. [product.jpg if in frame — how they're holding/interacting with it]. Speaking directly to lens: "[dialogue]." [Style modifiers]. 9:16 vertical, 8 seconds.
```

**Required style modifiers for every shot:**
- `handheld feel, slight camera shake`
- `candid`
- `natural skin texture`
- `[environment-appropriate lighting — soft window light / overcast natural light / warm kitchen light]`
- `imperfect framing`

**Product-forward shots additionally add:**
- `product label clearly visible`
- `[product color] bottle` or appropriate descriptor — reinforce the reference visually

**Example (Shot 1 — Hook, testimonial angle, supplement product):**

```
Vertical UGC video, creator.png standing in a bright kitchen, auburn hair in loose ponytail, light lavender athletic top, holding goli-bottle.jpg up toward camera with both hands. Product label clearly visible, red bottle. Speaking directly to lens: "I've been taking these every morning for 30 days and my energy is actually different." Handheld feel, slight camera shake, candid, natural skin texture, soft window light, imperfect framing. 9:16 vertical, 8 seconds.
```

### Step 6 — Write the Agent mode briefing instruction

Produce a single instruction the user can paste into Flow's Agent mode to brief the entire session at once.

Format:

```
I'm creating a 5-shot vertical UGC ad for [product name].

My uploaded assets:
- creator.png — the UGC creator
- [product-filename].jpg — the product

Generate these shots in order:

Shot 1: [environment]. creator.png [action + product interaction]. Speaking to camera: "[dialogue]." [lighting], handheld, candid, imperfect framing. 9:16, 8 seconds.

Shot 2: [different environment]. creator.png [action, no product]. Speaking to camera: "[dialogue]." [lighting], handheld, candid. 9:16, 8 seconds.

Shot 3: [environment]. creator.png [action + product interaction]. Speaking to camera: "[dialogue]." [lighting], handheld, candid. 9:16, 8 seconds.

Shot 4: [active environment]. creator.png [action, no product]. Speaking to camera: "[dialogue]." [lighting], handheld, candid. 9:16, 8 seconds.

Shot 5: [clean environment]. creator.png holding [product-filename].jpg toward camera. Speaking to camera: "[dialogue]." [lighting], handheld, candid. 9:16, 8 seconds.

Keep creator.png's appearance consistent across all shots. Generate each shot at 9:16 vertical.
```

### Step 7 — Write the ElevenLabs voiceover script

Produce the complete voiceover script — all five shots in order, with timing notes.

Format:

```
VOICEOVER SCRIPT — [Product Name] UGC Ad
Total duration: ~40 seconds

[Shot 1 — 0–8s]
"[dialogue]"

[Shot 2 — 8–16s]
"[dialogue]"

[Shot 3 — 16–24s]
"[dialogue]"

[Shot 4 — 24–33s]
"[dialogue]"

[Shot 5 — 33–42s]
"[dialogue]"

---
ElevenLabs settings: Stability 0.5, Similarity 0.75, Style 0.3
Recommended voice style: conversational, warm, not announcer
```

Tell the user: generate the video clips in Flow first. Then record or generate this voiceover in ElevenLabs. Stitch both in CapCut — video layer + audio layer + captions.

### Step 8 — Deliver

Present the full production package in this order:

1. **Creator image prompt** — paste into ChatGPT Images 2.0 or Nano Banana Pro
2. **Shot list with dialogue** — approve before generating
3. **Five asset-tagged Flow prompts** — one per shot, paste individually
4. **Agent mode briefing instruction** — paste once to brief the full session
5. **ElevenLabs voiceover script** — use after video generation

Ask the user if they want to adjust dialogue or angle before they generate. Dialogue changes are free. Regenerating clips costs credits.

## File structure this skill produces

```
[project-name]-production-package/
├── character-prompt.md       # ChatGPT Images / Nano Banana prompt
├── shot-list.md              # 5-shot script with dialogue
├── flow-prompts.md           # 5 asset-tagged prompts for Flow
├── agent-instruction.md      # Single Agent mode briefing
└── voiceover-script.md       # ElevenLabs-ready script with timing
```

## References

- `references/prompting.md` — style modifiers, asset tagging syntax, Agent mode briefing structure, what breaks character consistency
- `references/angles.md` — shot-by-shot breakdowns for all 5 preset angles
- `references/characters.md` — character image prompt templates for 8 creator archetypes

## Honest limits

- This skill produces prompts, not video. The user generates video in Flow's browser UI.
- Voice consistency across shots is not possible in Flow without the Avatar feature (own face/voice only). Plan for ElevenLabs post-production.
- Product label text can garble when the product is small in frame or the environment is complex. Keep product large and close in product-forward shots.
- Character consistency in Flow requires tagging `creator.png` in every shot prompt. Missing one tag = creator drift.
- Flow's Agent mode is experimental. If it doesn't run all shots automatically, paste individual prompts one at a time.
- Eating/drinking shots hallucinate. Use hold-and-show or hold-and-smile endings for any consumable product.
