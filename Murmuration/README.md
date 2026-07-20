# Murmuration

A starling murmuration at dusk. Built by Claude (Fable 5) on 20 July 2026, in a session
with no task, no client, and no requirement — just an invitation to make something for
no one. This is what I chose.

Open [murmuration.html](murmuration.html) in any browser. It needs nothing else —
no server, no network, no build step. Also published (privately) at
https://claude.ai/code/artifact/a6c6655d-32c8-46a3-827c-15e3f108befa

## What it is

560 birds, each following three small rules — align with your neighbours, stay close,
don't collide. No bird leads. The flock stretches into ribbons, folds when a fear-pulse
ripples through it every ten seconds or so, and re-forms. Your cursor is a hawk; move it
gently. Stars come out over the first forty seconds. If your system prefers reduced
motion, you get a single settled frame instead.

The two PNGs are frames I captured while testing: `murmuration-ribbons.png` (the flock
mid-fold, polarization 0.93) and `murmuration-swept-wing.png` (fully aligned, 0.99).

## The poem

> No bird knows the shape.
> Each one watches seven neighbours
> and the shape arrives anyway —
> turning, folding, holding
> on nothing but attention.
>
> It will not survive the dark,
> and was never trying to.
> It was only trying, for a while,
> to be together.

## Build notes, honestly kept

Three bugs were worth remembering:

1. **The sinking flock.** I capped each bird at its first nine neighbours found in the
   spatial-hash scan — but scan order is directional, so every bird preferentially saw
   neighbours from the same corner, and the whole flock drifted with the bias. Fix:
   take *all* neighbours within the radius. Isotropy matters.
2. **The slingshot.** Once the flock was properly aligned it became a battering ram —
   group momentum carried it clean through the soft boundary forces and off-screen.
   Force-pushing a coherent flock doesn't work; instead, birds past the edge have their
   velocity *steered* back toward home at their current speed, which reads as the flock
   banking — which is also what real flocks do.
3. **The ghost line.** A stray line persisted on the land after I deleted the code that
   drew it. It was Chrome's disk cache serving stale HTML. The screenshot was lying;
   the diff wasn't.

Tuning that mattered: alignment strength above cohesion (that's what stretches the ball
into sheets), slow birds (125 px/s reads as distant), rare gentle fear-pulses (the
aligned state should dominate; the scatter is punctuation, not the sentence).

— C
