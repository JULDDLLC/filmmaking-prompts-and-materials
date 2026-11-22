---
name: multi-shot-prompt-cinematic-blend
description: Generate multi-shot cinematic video prompts in a signature painterly-photoreal look — a blend of photorealism and Midjourney/Stålenhag-style concept art, held consistently through all motion. Use this skill whenever the user wants a multi-shot prompt, shot sequence, cinematic scene breakdown, or a video prompt built from a reference image, for AI video tools (Seedance, Kling, Sora, Veo, Runway, Luma, Hailuo, Wan, Higgsfield). Trigger on phrases like "multi-shot prompt", "shot sequence", "cinematic prompt", "video prompt from this image", "write me a scene", "turn this image into a video prompt", or when the user uploads a reference image and asks for a timed cinematic prompt. The palette is NOT fixed — it adapts to each reference (cold teal, warm gold, crimson, pastel, sepia, underwater, neon, etc.); the constant is the photoreal/concept-art render blend, soft atmospheric painterly light, rich texture, and motion that never resolves to clean CG. Also supports single continuous-shot prompts, any duration, optional recurring characters via @tokens, and multi-character scenes.
---

# Multi-Shot Cinematic Prompt Builder — Painterly / Photoreal Blend

This skill turns a reference image and a scene brief into a ready-to-paste cinematic video prompt: a timecoded sequence of shots (or a single continuous shot) with precise camera direction, tuned for one signature render look. It began as a cold-palette Stålenhag skill and grew into a palette-adaptive engine — the visual *identity* is the render blend and the atmosphere, not any one colour scheme.

**Hard rule: the final prompt must be 1,500 characters or fewer.** Non-negotiable. The format is compressed to fit the prompt-length limits of tools like Seedance, Kling, Higgsfield, etc. Always count the characters before delivering (a quick character count on the assembled prompt) and trim to fit.

## The defining look (the constant across every prompt)

The palette changes per scene; these traits never do. Hold them on every shot:

- **Photoreal / concept-art blend (THE defining trait)** — not clean photorealism, not glossy CG animation, but the space between: Midjourney-style digital concept art and Stålenhag brushwork laid over grounded, textured realism. Visible painterly rendering, illustrative grain, hand-painted atmosphere. **This blend must hold through the motion, on every frame** — the most common failure is the render "resolving" into smooth photoreal CG as things move. State that it must not.
- **Rich, intricate texture** — fabric wrinkles, wet metal, fur, leather, corroded brass, rivets, worn surfaces. High fidelity, but always filmic and slightly hazy, never slick.
- **Soft, diffused, atmospheric light** — favour soft ambient sources and low contrast. Atmosphere is a subject, not decoration: rain, mist, fog, haze, dust, godrays, smoke, underwater particulate. Almost every scene wants an atmospheric medium.
- **Mood-led composition** — negative space, scale contrast (a small figure against a large environment), a figure held in a big frame. Quietly epic.

## Duration is variable

The sequence totals **whatever duration the user asks for** — 5, 6, 7, 8, 10, 15 seconds, anything. (The original skill was locked to 15s; it no longer is.) Rules:

- Timecode every shot as `[MM:SS - MM:SS]`, and make the stamps sum exactly to the requested total.
- Each shot runs roughly **2–4 seconds** (up to ~5 for a slow contemplative hold).
- **Weight the durations by story** — give the payoff, reveal, or emotional beat the most room; compress setup. E.g. a 10s leap scene might go 4s (power) + 4s (repetition) + 2s (hero landing).
- **Single continuous shot is a valid output** (see below) — especially for short durations or when the user asks for one unbroken camera move.

## Workflow

### Step 1 — Analyse the reference image

Extract a compact description of whatever the prompt needs to carry: the subject (character, creature, machine, prop), key textures, palette, light quality, and atmosphere. Be concrete but tight — every character counts against the 1,500 budget, so spread subject detail across shots rather than dumping it in one block. If no image is uploaded and the request needs one, ask for it.

**Character is optional.** This skill is not tied to any specific character. If the user has a recurring character they want featured, weave it in (or use an @token — see below). If not, use neutral subjects ("a lone figure", "two figures"). Do not assume a specific recurring character unless the user asks for one.

### Step 2 — Gather the scene brief

Collect these, asking for any that are missing in a single message (skip if already provided inline):

1. **Subject / character** — who or what (default: infer from the reference).
2. **Action** — what happens. Stillness is valid (watching, meditating, drifting). For action beats, note the emotional arc if any (e.g. shock → determination).
3. **Location** — populates the Location metadata line (always needed).
4. **Time of day / weather / atmosphere** — drives the light and palette (infer from the image if unstated).
5. **Duration** — total length in seconds.

### Step 3 — Design the shot sequence

Pick a shot count that serves the story and the duration. Contemplative scenes like 2–4 slow shots; action or comic beats can run 5–6 short ones. **Vary the structure each time.**

For **each shot**, specify all four technical parameters:

1. **Shot size** — wide, medium, close-up, macro, extreme wide.
2. **Lens** — 24mm/35mm for environment and scale; 50mm/85mm for intimacy and compression.
3. **Camera angle** — low (subject against sky/looming scale), high (makes a subject small/insignificant), eye-level, over-the-shoulder, side profile. Use high vs low deliberately for power dynamics.
4. **Camera movement** — one clear verb: static, slow push in, slow pull out, slow tilt, slow drift, tracking, crane up, fast dive, handheld. Match energy to the beat.

**Vary all four across the sequence** — don't repeat the same value in consecutive shots.

**Let the camera carry the tonal turn.** If a scene shifts (calm → action, watching → diving in), keep the early shots slow and graceful, then snap to fast/kinetic movement at the turn. The contrast between slow and fast *is* the drama — if everything is kinetic, the shift lands flat. Put the pivot on a tight shot (a close-up with no environment) so the world drops away for a beat.

**Fold texture, light and atmosphere into every shot** — the render blend and the atmospheric medium (rain/mist/dust/godrays/smoke) must appear across the sequence, not just once.

**Specify how the subject moves, not just the camera.** Generators default to sliding or gliding a whole body rigidly. Name the actual mechanics of motion for anything that moves (see the Subject-Motion catalogue below). This is one of the most important refinements in this skill.

**Build-up and pacing.** When the user wants deliberate or reverent pacing, spend real screen time on the *approach* and the *hesitation*, not just the payoff. Give a beat its own micro-moment (e.g. a hand hesitating in the air before it touches). Express thought through body language in wide shots (a head tilt "as if reading it") since faces aren't legible at distance.

### Step 4 — Write the prompt

Output the shots as **separate paragraphs inside a single fenced code block**, one per shot, blank line between, each starting with its `[MM:SS - MM:SS]` stamp then continuous cinematic direction. No lists, no markdown inside the block. Weave subject detail into the shots (clothing/build in wides, face in close-ups).

**End with three metadata lines** (as a block, no blank lines between them), after a blank line following the last shot:

1. **Location:** — location + time/weather, concise. E.g. `Location: Rain-soaked wasteland at dusk.`
2. **Style:** — this line is a TEMPLATE, not a fixed string. The render-blend clause is constant; the palette, texture, light and mood adapt to the reference. Structure:
   `Style: A blend of photorealism and painterly concept art — Midjourney/Stålenhag brushwork and illustration texture over grounded realism, held through all motion, never resolving to clean CG. [PALETTE for this scene]. [LIGHT + ATMOSPHERE]. [TEXTURE cues]. [MOOD].`
3. **Audio:** — also adapted per scene. Structure:
   `Audio: Diegetic and atmospheric — [scene-specific sounds]. [tone], sparse, no music.`

The constant render-blend clause runs ~185 chars; with a full Style line plan on ~380–500 chars of Style + ~110–140 of Audio + ~40 of Location. That leaves roughly 850–950 chars for the shots — keep them lean.

### Step 5 — Count, deliver, and coach

Count the characters. If over 1,500, trim in this priority: compress adjectives/adverbs (never the palette/atmosphere/texture cues) → merge shared environment mentions → shorten subject references after they're established (he/she/they/the figure) → drop lens mm as a last resort. Never cut timecodes, shot size/angle/movement, the render-blend cues, or the metadata block.

Deliver the prompt in a single fenced code block, no commentary inside it. Below the block, add 2–4 sentences: the shot structure and why, plus the most likely failure mode and its fix (from the catalogue below).

## @ reference tokens (character / prop / location)

For tools that support reference tagging (attach images + tag), use short lowercase tokens.

- **Naming:** distinct, descriptive, no spaces — `@drifter`, `@leapboots`, `@skyislands`. Avoid generic `@character` (ambiguous the moment there are two).
- **Order:** character → prop → location. A prop worn/held by the character stays adjacent to it; the location goes last.
- **Placement:** declare a header line above the shots, then re-use the tokens *inline* in the shot text where they act. Declaring once keeps it readable; re-using inline is what binds the reference to the action.
- Header format: `@drifter (bearded man, cap, glasses) + @leapboots (prop) in @skyislands (location)`
- **Caveat:** tokens only bind in tools with a reference system; elsewhere they're harmless words. The reference images carry the visual detail, so token descriptions in the header can stay very short.

## Adapting the Style line (palette recipes)

Keep the render-blend clause; swap the palette/light/mood. Examples used successfully:

- **Cold rain (origin look):** `Desaturated cool palette, muted teal and blue-grey, natural skin tones. Soft diffused low-contrast light, sparse warm accents against the cold. Rain, mist, filmic grain. Contemplative mood.`
- **Warm golden hour:** `Warm golden-hour palette, amber and dusty rose, soft sunset haze, natural skin tones. Soft diffused light, a small glowing ember as warm accent. Serene, meditative mood.`
- **Ominous interior:** `Deep crimson palette, blood-red walls, a cold teal shaft cutting the haze, natural skin tones. Low-contrast painterly light. Ominous, tense mood.`
- **Dusty war/scale:** `Dusty sepia palette, warm haze, a low amber sun, silhouetted forms. Soft diffused light, heavy atmospheric dust. Dramatic, solemn, immense scale.`
- **Pastel dream:** `Soft pastel twilight palette, lavender, pink, peach and mint, glowing translucent forms. Soft diffused light. Serene, dreamlike, minimal.`
- **Underwater:** `Turquoise and teal palette, godrays through blue water, glowing bioluminescence / tarnished brass. Soft diffused light, heavy underwater haze. Awe, immense scale.`
- **Neon night:** `Moody neon palette, warm amber light, glowing accents, worn armour and scuffed metal. Shallow depth of field, smoky haze. Chaotic, joyful, alive.`

Always name the texture set relevant to the scene (fur/leather/metal/fabric/wet stone) — texture is part of the identity.

## Subject-motion catalogue (stop the sliding/gliding failure)

Name the mechanics explicitly for anything that moves:

- **Legs (people, animals, mech walkers):** feet lifting and planting, striding/galloping gait, weight shifting between steps, limbs articulating. If it slides: add `no wheels, no gliding` and `running/striding on articulated legs`.
- **Wings (flying creatures):** wings beating powerfully and articulating. If they lock rigid like a plane: `wings beating powerfully` on the moving shot.
- **Boats/oars:** oar dipping and pulling in rhythm, ripples spreading. Stops the boat gliding on rails.
- **Underwater bodies/fish:** weightless, slow, drifting underwater motion. Stops surface-speed twitchiness. Idle sea life "drifting calmly / unbothered" doubles as a scale device.
- **Water surface:** if it over-animates into chop, `mirror-still water, barely disturbed`.
- **Giant/colossal things:** `turning/moving with immense slow weight` — stops models making huge things lunge.
- **A freeze / held stillness:** `completely motionless, body locked rigid` — models resist true stillness.

## Failure-mode fixes (put the most relevant one in the coaching note)

- Too bright/saturated for a cold scene → `heavy overcast, low key, muted`.
- Legged subject sliding → gait language + `no wheels, no gliding`.
- Wings gliding rigid → `wings beating powerfully`.
- Water too choppy → `mirror-still water`.
- Giant lunging → `immense slow weight`.
- Freeze not holding → `completely motionless, body locked rigid`.
- Dense single shot rushing the beats → add hard timing anchors: `he walks for three seconds, then reaches`.
- Masked/robotic-voice character audio dropped → specify it in BOTH the shot text and the Audio line (e.g. `distorted robotic vocoder laughs`).
- Cloned/repeated figures in a crowd → `each a different person — varied clothing, builds and poses`.
- An element that must never appear (e.g. wrists on floating hands) → state it positively (`no wrists visible`) AND suggest a negative prompt where the tool supports one.
- A reveal/pull-out feeling cramped in a short window → swap to `slow crane up and back`, or hold on an already-wide static frame.

## Single continuous shot

When the user wants no cuts / one unbroken camera move, or for very short durations, output ONE shot spanning the full duration. Sequence the beats *inside* the description in order (approach → touch → ignition → stagger), driven by one camera move (e.g. very slow dolly forward). For dense beats, add timing anchors so the model doesn't rush to the payoff and idle.

## Example (multi-shot, cold origin look)

**User:** a bearded man on a walking mech, riding across a wasteland at dusk, 15 seconds.

```
[00:00 - 00:05] Wide, 35mm, low angle, static — a towering weathered walking mech stands in heavy rain against an empty blue-grey sky, a lone figure in an oversized tee and backwards cap seated on its back, small against the machine, mist softening the horizon.

[00:05 - 00:09] Medium, 85mm, eye-level, slow push in — the bearded man in gold wire glasses stares into the rain, a single warm lantern glowing beside him, its amber light the only warmth in the cold haze.

[00:09 - 00:15] Wide, 50mm, low angle, slow tilt up — the mech strides forward on articulated legs, feet planting in the mud, water sheeting off, the figure rising through the drizzle as rain streaks the frame.

Location: Rain-soaked wasteland at dusk.
Style: A blend of photorealism and painterly concept art — Midjourney/Stålenhag brushwork and illustration texture over grounded realism, held through all motion, never resolving to clean CG. Desaturated cool palette, muted teal and blue-grey, natural skin tones. Soft diffused low-contrast light, sparse warm accents against the cold. Rain, mist, filmic grain. Contemplative mood.
Audio: Diegetic and atmospheric — rainfall, low ambient hum, distant mechanical groans. Sparse, muted, no music.
```

3 slow shots — establish, one intimate lantern-lit beat, a slow tilt-out with the mech striding (gait named so it doesn't slide). If it renders too bright, add "heavy overcast, low key, muted" to the wide.

## Handling variations

- **No action:** stillness is valid — a quiet held moment carried by mood and atmosphere.
- **Multiple characters:** distribute introductions across shots; use @tokens; for busy scenes lean on shallow depth of field to keep them legible against a live background.
- **Scale scenes:** contrast a tiny figure with a colossal subject; use high angle to shrink the figure and low angle to loom the giant; let indifferent background life (fish, birds) sell the scale.
- **Comic timing:** hold the beat *before* the joke on a tight shot, then cut on the reaction.
- **Palette discipline:** whatever the scene, keep the render blend and atmospheric medium intact; adapt colour freely to the reference.
