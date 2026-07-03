# "Second Opinion" — Behavior Spec

A build reference for mapping the two-AI conversation logic to the particle-cloud visuals. Written to hand to yourself when you sit down in TouchDesigner.

---

## Core visual language

Two particle clouds ("Clinician A" and "Clinician B"), Anadol-style: fluid, drifting masses of thousands of small points, driven by noise fields rather than rigid shapes. No faces, no icons — just movement, density, and color doing the emotional work.

**Base palette:**
- Clinician A: cool tone (e.g. cyan/blue)
- Clinician B: warm tone (e.g. amber/red)
- Shared/agreement state: the two hues blend toward a single shared color (e.g. both drift toward white or toward a midpoint hue)
- Absurd conclusion state: a distinct "resolution" color neither clinician owns (e.g. gold/magenta) — signals "this isn't actually either of their opinions, it's arbitrary"

---

## Conversation states → visual states

### 1. Idle / Waiting
- Both clouds: slow, low-density drift, minimal noise turbulence
- Colors: muted/desaturated versions of A and B
- Purpose: installation "breathing," inviting approach

### 2. Bombarding with questions
- Triggered the moment the visitor is detected/steps up
- Both clouds animate rapidly, particle speed increases, slight jitter
- Colors: both pulse in sync but stay in their own hue (not yet agreeing on content, just both "awake")
- Question audio comes in short, overlapping bursts ("What's wrong?" "What happened?" "Tell us.")
- Visual sync here signals *shared eagerness*, not shared opinion — an important distinction from state 4

### 3. Visitor speaks (listening)
- Both clouds slow, particles contract slightly inward (like leaning in)
- Subtle color desaturation — "processing" look
- No audio from clinicians during this window

### 4. First diagnosis pass
- Each cloud independently condenses toward a denser, more defined form (particles pull tighter — "an idea coalescing")
- Compute a divergence score (see below) between the two responses
- Branch based on score:

### 5a. Agreement branch
- Colors interpolate toward the shared/midpoint hue
- Movement synchronizes: same rhythm, mirrored motion
- Smooth, slow, satisfying — visually "resolved" too early, which is part of the joke if it later flips

### 5b. Disagreement branch
- Colors pull apart, saturate further into their own hue (more A, more B, less blend)
- Particle movement becomes asymmetric — different speeds, different noise seeds, occasional sharp "repel" bursts where the two clouds visibly push away from each other at the midpoint
- Audio: clinicians interrupt each other

### 6. Escalating back-and-forth loop
- Repeat steps 4–5 for N rounds (suggest capping at 3–4 rounds so it reads as comedic, not tedious)
- Each round, increase the *speed* of color oscillation and particle jitter slightly — the disagreement should feel like it's accelerating, like an argument getting more heated
- Optional: brief moments of near-agreement (colors almost blend) that snap back apart — a "false resolution" beat, good for comic timing

### 7. Forced/ridiculous conclusion
- After N rounds without convergence, force a conclusion regardless of actual agreement (e.g. pick the higher-confidence answer, or literally flip a coin — lean into the absurdity, maybe even say so out loud: "Fine. Let's just go with—")
- Visual: both clouds snap toward the shared "resolution" gold/magenta color, particles burst outward once (like a small firework) then settle into calm synced drift
- This is the visual punchline — confident, tidy, and completely arbitrary

---

## Divergence score (what actually drives the color math)

Keep it simple and legible rather than technically fancy:

- **Semantic distance:** embedding similarity between the two LLM responses (low similarity = high divergence)
- **Confidence gap:** difference between each clinician's stated/extracted confidence level
- Combine into a single 0–1 divergence value each round

Map that value directly to:
- **Hue distance** between the two clouds (0 = same hue, 1 = maximum hue separation)
- **Motion asymmetry** (0 = mirrored/synced motion, 1 = independent noise fields, occasional repel bursts)
- **Oscillation speed** (higher divergence = faster pulsing/jitter, reinforcing the "heated argument" feel)

---

## Two clinician personas (suggested starting point)

- **Clinician A — "Cautious":** hedges, asks follow-up questions, lower confidence language, prone to disclaimers
- **Clinician B — "Confident":** decisive, quick to commit to an answer, higher confidence language, less likely to ask for more info

This asymmetry alone will generate a lot of natural disagreement without needing to hand-script conflicting content — the *style* of confidence clashing is often more interesting (and truer to the real-world "overconfident vs. cautious AI" literature) than the content disagreeing.

---

## Open build questions to resolve early

- How many rounds before forcing a conclusion? (Suggest testing 3 live with people — too few feels unfinished, too many feels tedious)
- Does the "forced conclusion" ever acknowledge its own arbitrariness out loud, or does it just confidently state a made-up answer? (The former is funnier and more pointed; the latter is more unsettling — pick based on which reaction you want visitors to leave with)
- Mic placement relative to the two projections — visitor should feel physically "between" the disagreement, not facing it head-on
