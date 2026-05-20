# Google Flow UGC Ad Skill for Claude Cowork

A Claude Cowork skill that generates complete production packages for multi-shot UGC video ads in Google Flow.

Drop in a product image and an ad angle. Get back everything you need to run a full Agent mode session in Flow: a realistic AI creator image prompt, asset-tagged shot prompts, a 5-shot direct response script, a single Agent briefing instruction, and an ElevenLabs voiceover script.

No API required. No code. Generates inside Google Flow's browser UI.

---

## What's Inside

```
flow-ugc-ads/
├── SKILL.md                      # Main skill file for Claude Cowork
└── references/
    ├── prompting.md              # Style modifiers, asset tagging, dialogue pacing
    ├── angles.md                 # Shot-by-shot breakdowns for 5 ad angles
    └── characters.md             # 8 ready-to-paste creator archetype prompts
```

## Setup

1. Install in Claude Cowork: Settings → Skills → Install from file → select `SKILL.md`
2. Toggle the skill on for any project
3. Drop a product image into your project folder
4. Run: `Use the flow-ugc-ads skill. Product: [name]. Product image: [filename]. Angle: testimonial.`

## Requirements

- Claude Cowork (Claude Desktop)
- Google AI Pro subscription ($19.99/month) at [labs.google.com/flow](https://labs.google.com/flow)
- ChatGPT Images 2.0 or Nano Banana Pro (for creator image generation)
- ElevenLabs (optional — for voice consistency in post)

---

Part of the SCALE AI skills library. New skills monthly at [skool.com/scale-ai](https://www.skool.com/scale-ai/about).
