# Wedding Invitation

A single-page wedding invitation site: static HTML, CSS and vanilla JS, no build step.

Built as a rebuild of the *design and motion system* of richardandanita.com. All content,
copy and artwork here is original placeholder material for a fictional couple. None of the
original couple's photographs, names, event details or written passages were copied.

## Run

```bash
python3 -m http.server 4321
```

Then open http://localhost:4321

## Structure

- `index.html` — markup and the inline SVG artwork (envelope texture, wax seal, hero scene, venue plate)
- `styles.css` — design tokens, layout, and every animation
- `main.js` — gate choreography, text splitting, scroll reveals, countdown, parallax, RSVP

## The animations

| Effect | Where |
|---|---|
| Wax seal float, pulse glow, sweeping shine | `.seal*` in CSS |
| Envelope open: flap rotates back, seal lifts away, paper parts and blurs out | `.gate.is-opening` |
| Theatre reveal: valance drops, curtains sweep apart, columns slide in | `body.is-open .stage*` |
| Hero Ken Burns slow zoom | `@keyframes kenBurns` |
| Per-character name reveal out of blur, letter-spacing track-in on the eyebrow | `.ch` + `splitText()` |
| Scroll reveals, fade-up and clip-path wipe variants | `[data-reveal]` + IntersectionObserver |
| Live countdown with a digit roll on every change | `@keyframes digitRoll` + `wireCountdown()` |
| Timeline that draws itself down as you scroll | `#timelineFill` + `wireScrollMotion()` |
| Depth parallax on hero and venue plate | `[data-parallax]` |
| Drifting rose petals | `seedPetals()` |
| RSVP: conditional section, guest stepper, animated check on success | `wireForm()` |

Parallax and the timeline draw share one rAF-throttled scroll listener.

## Making it yours

- Names, dates, venue and schedule are plain text in `index.html`.
- The countdown target is the `WEDDING` constant at the top of `main.js`.
- Colours and type are custom properties in the `:root` block of `styles.css`.
- The RSVP form is local only. It validates and shows the success state but posts nowhere.
  There is a commented `fetch` in `wireForm()` where a backend call belongs.

`prefers-reduced-motion: reduce` is honoured throughout: petals are removed and every
transition collapses, while all content stays visible.
