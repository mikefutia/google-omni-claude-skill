# Flow Prompting Reference

How to write prompts that produce UGC output in Google Flow instead of commercial output.

---

## The Core Problem

Without specific style modifiers, Gemini Omni Flash defaults to commercial-looking output: perfect lighting, perfectly centered framing, polished skin, studio-quality composition. That's the opposite of what converts on Meta and TikTok. UGC converts because it looks real. Your prompts have to deliberately introduce imperfection.

---

## Required Style Modifiers (Every Shot)

Add all of these to every prompt:

| Modifier | What it does |
|----------|-------------|
| `handheld feel, slight camera shake` | Removes the locked-off tripod look |
| `candid` | One of the strongest realism signals — tells the model this isn't a set piece |
| `natural skin texture` | Prevents the "plastic skin" AI tell |
| `imperfect framing` | Gemini centers everything without this — real UGC is never perfectly composed |
| `[environment-specific lighting]` | Replaces the default studio light inference |

**Lighting options by environment:**
- Kitchen: `soft morning window light` / `warm overhead kitchen light`
- Car: `soft overcast daylight through windshield` / `warm afternoon side light`
- Bathroom: `natural vanity light` / `warm bathroom overhead`
- Gym: `overhead fluorescent, slightly harsh` / `natural light from window`
- Outdoors: `overcast natural light` / `direct afternoon sun, slight squint`
- Bedroom: `soft morning light through curtains` / `bedside lamp, warm`

---

## Asset Tagging Syntax

Reference uploaded assets by their exact filename in the prompt. Flow identifies the asset and uses it as a visual reference.

**Format:** just the filename inline — no brackets, no special syntax.

```
creator.png standing in a bright kitchen holding goli-bottle.jpg...
```

**Rules:**
- Filename must match exactly what you uploaded (case-sensitive)
- Tag both creator AND product in every shot, even if product isn't the focus
- For environment-only shots (no product in frame), still tag the creator

**What breaks it:**
- Forgetting to tag the creator image = character drift between shots
- Forgetting to tag the product = model hallucinates a generic product
- Using a vague filename like `image1.jpg` — use descriptive names

---

## Dialogue Pacing

Budget approximately 3 words per second of screen time.

| Shot length | Max dialogue |
|------------|-------------|
| 6 seconds | ~18 words |
| 7 seconds | ~21 words |
| 8 seconds | ~24 words |
| 9 seconds | ~27 words |

Over-scripted dialogue rushes and sounds like a script. Under-scripted leaves dead air. Stay within the budget.

---

## UGC Dialogue Patterns

Write dialogue like a real person texts — not like a brand writes copy.

**Green:**
- "Okay I need to talk about this."
- "Bro, these finally came in."
- "I've been waiting to post this."
- "This is my new favorite thing."
- "Hear me out."
- "I was skeptical but..."
- "Week two and I'm already noticing a difference."

**Red:**
- "Introducing our new innovative product..."
- "Experience the difference with..."
- "Clinically proven to..."
- "Shop now and save..."
- Anything that sounds like it was written by a brand

**CTA patterns that work:**
- "Link is below."
- "You literally have nothing to lose."
- "Just try it for 30 days."
- "I'll link it."
- "Trust me on this one."

**CTA patterns that kill the UGC feel:**
- "Shop now"
- "Buy today"
- "Use code [X] for [Y]% off" (save this for caption, not dialogue)
- "Visit our website"

---

## Agent Mode Briefing Structure

When using Agent mode, structure your instruction like a director's brief — not a single-shot prompt.

**Template:**

```
I'm creating a [N]-shot vertical UGC ad for [product].

My uploaded assets:
- creator.png — the UGC creator
- [product].jpg — the product

Generate these shots in order:

Shot 1: [one sentence: environment + action + dialogue]. [lighting], handheld, candid, imperfect framing. 9:16, 8 seconds.

Shot 2: [same structure]. [lighting], handheld, candid. 9:16, 8 seconds.

[continue for each shot]

Keep creator.png consistent across all shots.
```

**What makes Agent mode better than standard prompts:**
- It holds the full production context across all shots
- It maintains asset references without you re-tagging every time
- It can iterate on shots without you re-briefing from scratch
- It handles the production loop — if a shot looks wrong, you can say "redo Shot 3 with warmer lighting" and it knows which shot and which assets

---

## Hard Categories — What to Avoid and How to Work Around It

Some shot types reliably hallucinate in Gemini Omni Flash:

**Eating / drinking:**
Problem: food disappears, color appears on wrong surfaces, consumption motion looks wrong.
Workaround: "holds [product] up to camera, smiles, does not eat or drink." End on hold, not consumption.

**Makeup application:**
Problem: color transfers to wrong body parts, pre-existing makeup marks appear, smudging.
Workaround: "holds [product] up to camera, does not apply. Finished look — [describe the result]." Show the result without showing the application.

**Complex hand-object interaction:**
Problem: extra fingers, object warping, product changing shape mid-shot.
Workaround: keep interactions simple — pick up, hold, rotate, set down. One action per shot.

**Small text / fine print on packaging:**
Problem: text garbles, especially at arms-length or 480p.
Workaround: keep product large in frame (filling 30–40% of the shot), use 720p minimum for product-forward shots, use Agent mode (not standard generation) for any shot where label legibility matters.

---

## Shot-Level Prompt Template (Complete)

```
Vertical UGC video, [creator.png] [environment — specific room/setting], 
[outfit detail], [action — one action only]. 
[product.jpg if in frame — how they're holding/interacting + reinforce color/descriptor]. 
Speaking directly to lens: "[dialogue — within word budget]." 
Handheld feel, slight camera shake, candid, natural skin texture, 
[environment-specific lighting], imperfect framing. 
9:16 vertical, [X] seconds.
```

Fill every bracket. Vague prompts = generic AI output. Specific prompts = UGC output.
