# The Google Flow UGC Ad Playbook for DTC Brands & Creative Agencies
How to generate multi-shot UGC video ads using Google Flow's Agent mode, Gemini Omni Flash, and a Claude Cowork skill that writes every prompt for you — so you go into Flow with a complete production package instead of a blank prompt box.

---

## What Google Flow Actually Is (And Why It's Different)

Google Flow is a video generation workspace powered by Gemini Omni Flash — Google's latest video model. It's not a prompt box that outputs a single clip. It's a media library where your assets live — product images, creator references, scenes — and a generation environment where those assets become video.

The part most people miss: there's an Agent mode built directly into the prompt box. You're not just generating one clip at a time. You're briefing an agentic creative director that can write, generate, organize, and iterate across your entire project.

Three things make this the most accessible AI video tool for DTC right now:

**1. No API required.** Google Flow is a UI tool. No fal.ai account, no Python scripts, no ffmpeg setup. You generate inside the browser. The barrier to entry is a Google AI Pro subscription ($19.99/month).

**2. Asset tagging via filename.** You reference your uploaded assets directly in prompts using their filename — `product.jpg`, `creator.png`, `reference-ad.mp4`. Flow knows which asset you mean. This is the mechanic that makes consistent, multi-shot production possible without code.

**3. Agent mode handles the production loop.** Instead of manually writing a new prompt for every shot, you brief the Agent once with the full picture — product, creator, angle, scenes — and it runs the session.

---

## The Product Fidelity Problem (And How Agent Mode Solves It)

Standard Flow generation has a product fidelity issue. When you generate from a product image, the model sometimes gets the color wrong, garbles the label text, or drifts from the reference.

We tested this directly with a Goli supplement bottle:

**Standard mode:** Generated a green bottle. The reference was red. Label text garbled — "WORLD'S FIRST ASHWAGANDHA FRNE," nonsense copy throughout.

**Agent mode with the product image attached:** Correct red bottle. Label text readable — "WORLD'S FIRST APPLE CIDER VINEGAR GUMMIES," dietary info, icons all visible. The model even added a detail we didn't prompt — it shook the bottle so you can hear the gummies rattling.

The lesson: always use Agent mode for product-forward shots. Standard generation is for environment and lifestyle shots where product accuracy isn't critical.

---

## How to Build a UGC Creator That Looks Real

The difference between a UGC creator that looks real and one that looks like an AI demo is almost entirely in the character image prompt. Plasticky outputs come from prompts that describe a perfect person in perfect lighting. Real-looking outputs come from prompts that deliberately introduce imperfection.

**The character image prompt formula (for ChatGPT Images 2.0 / Nano Banana Pro):**

```
Candid iPhone photo of a [age]-year-old [gender], [specific physical detail — hair color/texture, freckles, etc.], [minimal/natural] makeup, wearing [specific casual outfit — not "stylish," something real], [environment — sitting in car / standing in kitchen / etc.]. Shot from [slight angle — low angle, slightly off-center]. [Specific lighting — soft overcast daylight / warm window light]. Slightly imperfect exposure. Real, unretouched skin texture. Natural flyaways. No studio lighting. Editorial-style realism.
```

**What to avoid:**
- "Beautiful woman" — produces model-face
- "Professional lighting" — produces studio look
- "Stylish outfit" — produces fashion-shoot energy
- Neutral backgrounds — removes environmental realism

**What to add:**
- Specific imperfections: flyaways, freckles, slightly uneven lighting
- A real environment even in the character image: car seat, kitchen counter in background, bathroom mirror
- "Candid iPhone photo" — one of the most reliable realism signals

Once you have the character image, upload it to Flow. It becomes your creator reference for every shot.

---

## The Asset Tagging System

This is the mechanic that makes multi-shot production work in Flow.

When you upload an asset to your Flow project, you reference it in prompts by its exact filename. Flow identifies which asset you mean and uses it as a reference for generation.

**Example:**

You upload:
- `creator.png` — your AI UGC creator image
- `goli-bottle.jpg` — your product photo

Your prompt becomes:

> Vertical UGC video, `creator.png` sitting in car driver's seat, auburn hair, olive green top, holding `goli-bottle.jpg` up toward camera, speaking directly to lens: "Okay I used to mix pre-workout in my car and it was absolute chaos." Handheld feel, soft window light, slightly shaky, candid.

Flow reads `creator.png` and `goli-bottle.jpg` as visual references — not descriptions, actual images. The output reflects the real product and the real creator, not a hallucinated version of either.

**Rules for the asset tagging system:**
- Use descriptive filenames: `red-goli-bottle.jpg` is better than `image1.jpg`
- Always tag both creator AND product in every shot prompt — even if the product isn't the focus of that shot
- For environment shots, you can tag just the creator and describe the environment in text

---

## The 5-Shot DR Script Structure

A full UGC ad for Meta or TikTok runs 30–45 seconds. Five shots, each 6–9 seconds, each with a clear job in the direct response structure.

**Shot 1 — Hook (0–7s)**
Creator holds product, speaks directly to camera. One claim, no setup.
Goal: stop the scroll. Make them want to know more.
Example dialogue: *"I've been taking these every morning for 30 days and my energy is actually different."*

**Shot 2 — Problem agitation (7–16s)**
Different environment. Creator without product. Describe the before state.
Goal: make the viewer feel the pain. Make it specific.
Example dialogue: *"I used to wake up already dreading the day. Before I even got out of bed I was already running on empty."*

**Shot 3 — Discovery (16–24s)**
Back to a product-forward environment. Creator opens or interacts with product.
Goal: introduce the solution naturally, not as a pitch.
Example dialogue: *"A friend told me about ashwagandha for cortisol and I was skeptical. But I figured $30 was worth a shot."*

**Shot 4 — Transformation (24–34s)**
Active environment — gym, outdoors, at work. No product in hand. Creator looks and feels different.
Goal: show the result. Make it specific and believable.
Example dialogue: *"By week two I wasn't hitting that 3pm wall anymore. Week four — I'm waking up before my alarm."*

**Shot 5 — CTA (34–45s)**
Back to a clean environment. Creator holds product toward camera.
Goal: remove friction. Give them one action.
Example dialogue: *"If you're running on caffeine and stress, try it for 30 days. Link is below. Money back guarantee, so you literally have nothing to lose."*

---

## Voice Consistency — The Real Limitation and the Workaround

Google Flow does not support custom voice upload. You can't drop an MP3 and clone a voice the way Seedance 2.0 handles audio references. Each generated clip produces a new AI voice, and right now there's no way to lock voice identity across shots inside Flow.

The Avatar feature (available on paid plans) captures your own face and voice through a registration process — it's not an uploadable file. If you're building founder-led content and register your own avatar, you get voice consistency because it's your actual voice. For AI creator ads, you don't have that option yet.

**The workaround:**

Generate every clip with `generate_audio: false` — or generate with audio and strip it in post. Then dub the entire ad with a consistent voice in ElevenLabs or CapCut's AI voice feature.

This adds one step but gives you full control: consistent voice, consistent pacing, ability to iterate the script without regenerating video.

**The two-step workflow:**
1. Generate all video clips in Flow with placeholder dialogue or silent
2. Write the final dialogue script, record or generate a voiceover in ElevenLabs, stitch in CapCut

The visual performance of each clip is independent of the audio — you're not losing anything by separating them.

---

## Running This With The Claude Skill

Everything in this playbook — the character image prompt, the asset-tagged shot prompts, the dialogue for each scene, the Agent instruction — can be generated in 60 seconds using the `flow-ugc-ads` Claude Cowork skill included with this playbook.

Here's how it works:

You drop a product image into your Cowork project folder. You tell Claude what kind of ad you want. Claude reads the skill and produces a complete production package:

1. A character image prompt optimized for realism (paste into ChatGPT Images or Nano Banana Pro)
2. A 5-shot script with dialogue for each scene
3. Five asset-tagged Flow prompts — ready to paste directly into Flow's Agent mode
4. A single Agent instruction you can use to brief Flow all at once
5. A voice-over script to hand to ElevenLabs

No blank-page problem. No guessing what to write in Flow. You go in with everything.

**Example prompt to run the skill:**

```
Use the flow-ugc-ads skill.

Product: Goli Ashwagandha Gummies — a supplement gummy for stress and energy
Product image: goli-bottle.jpg
Angle: testimonial
Creator: 27-year-old woman, fitness-oriented, relatable, not model-perfect
```

Claude produces the full production package. You generate the creator image, upload both assets to Flow, paste the Agent instruction, and run.

---

## Prompt Structure That Actually Works in Agent Mode

Agent mode in Flow responds to production instructions, not just descriptions. The more it reads like a director's brief, the better the output.

**Structure every Agent session like this:**

```
I'm creating a [N]-shot vertical UGC ad for [product]. 

My assets:
- [creator.png] — the UGC creator
- [product.jpg] — the product

Generate these shots in order:

Shot 1: [environment]. [creator.png] holding [product.jpg], speaking to camera: "[dialogue]." Handheld feel, [lighting], candid.

Shot 2: [different environment]. [creator.png] without product, [action], speaking to camera: "[dialogue]." [lighting].

[Continue for each shot]

Keep the creator's appearance consistent across all shots. Generate each shot at 9:16 vertical, 8 seconds.
```

**Style modifiers that push toward UGC (not commercial):**
- `handheld feel, slight camera shake` — removes tripod perfection
- `candid` — one of the most reliable realism signals
- `natural skin texture` — avoids plastic AI skin
- `soft window light` / `overcast natural light` — avoids studio lighting
- `imperfect framing` — Gemini tends to perfectly center everything without this

Without these modifiers, you get an ad that looks like a rendered commercial. With them, you get something that passes for a real creator on first scroll.

---

## What's Still Hard

**Eating and drinking shots.** Any shot where the creator consumes the product tends to hallucinate — wrong mouth position, product appearing and disappearing, liquid physics going wrong. Use a "hold and smile" ending instead of a consumption shot.

**Small text on packaging.** Label text at 480p or when the product is small in frame often garbles. Keep the product close and large in frame, and always use Agent mode when product fidelity matters.

**Multi-environment character consistency.** Flow doesn't have Seedance's explicit `@Video1` reference syntax. Character consistency in Flow relies on the creator image reference being tagged in every single prompt. If you forget to tag `creator.png` in one shot, the creator drifts. Don't skip it even if the shot isn't creator-forward.

**Voice.** No custom voice upload yet. Plan for ElevenLabs in post.

---

## Cost Reality

Google Flow runs on a credit system under Google AI Pro ($19.99/month). Gemini Omni Flash is significantly cheaper per second than Seedance 2.0 on fal.ai.

Approximate comparison for a 5-shot, 40-second ad:

| Tool | Approx. cost | Setup required |
|------|-------------|----------------|
| Google Flow (Gemini Omni Flash) | ~$2–4 | Browser only, AI Pro subscription |
| Seedance 2.0 via fal.ai | ~$6–10 | fal.ai account, API key, Python, ffmpeg |
| Human UGC creator | $150–300 per clip | 3–7 day turnaround |

Flow's cost advantage is real, but the bigger advantage is friction. No API, no terminal, no setup. You're generating inside a browser 90 seconds after you have your assets ready.

---

## Quick-Start Checklist

- [ ] Subscribe to Google AI Pro ($19.99/month) at labs.google.com/flow
- [ ] Generate your AI UGC creator image using the character prompt formula above (ChatGPT Images 2.0 or Nano Banana Pro)
- [ ] Name your files descriptively before uploading: `creator.png`, `product-name.jpg`
- [ ] Upload both assets to your Flow project
- [ ] Use the `flow-ugc-ads` Claude Cowork skill to generate your full production package
- [ ] Always use Agent mode for product-forward shots — never standard generation
- [ ] Tag both `creator.png` AND `product.jpg` in every shot prompt
- [ ] Plan for ElevenLabs voiceover in post — don't rely on per-shot audio for voice consistency
- [ ] Test a single shot first before running all five
- [ ] Stitch final clips in CapCut — add captions, music, and the ElevenLabs voiceover

---

## What's Inside The Skill File

Included with this playbook: `flow-ugc-ads.skill` — install in Claude Cowork and you're ready.

The skill contains:

**SKILL.md** — the main workflow. Handles intake, angle selection, character prompt generation, shot list writing, asset-tagged Flow prompts, Agent instruction, and ElevenLabs voiceover script.

**references/prompting.md** — how to write prompts that produce UGC output in Flow instead of commercial output. Style modifiers, dialogue pacing, asset tagging syntax, Agent mode briefing structure.

**references/angles.md** — shot-by-shot breakdowns for all five preset angles: testimonial, unboxing, lifestyle demo, problem-solution, car/on-the-go. Each includes visual direction, dialogue patterns, and which shots need product tagging vs creator-only.

**references/characters.md** — character image prompt templates for 8 creator archetypes: fitness woman, fitness man, busy mom, college student, professional woman, outdoors guy, beauty creator, everyday guy. Each is tuned for realism, not model-face.

The skill is read-only on first install but everything is editable — add creator archetypes, customize angles, or adjust the default DR script structure for your category.

---

## Next Steps

This playbook covers the core workflow end-to-end. The real value shows up when you run it 10 times and build a creator library — 5–6 saved character images across different demographics, each ready to drop into any ad.

If you want more — advanced angle patterns, brand-specific voice calibration, the full creative production system that layers this with competitor research and creative briefs — that's what we build inside SCALE AI.

New skills every month. Production-grade systems for DTC brands and agencies who need to ship more winning creative than they did last year.

Ready to go deeper: join 541+ brands and agencies inside SCALE AI at mikefutia.com/scale-ai.

Get to work.

— Mike
