# Ripple Type

Type anything and watch it ripple outward in ink and dust. A WebGL text effect inspired by
the title-card treatment in AppleTV+'s *Pluribus* — fine hatched lines inside the letterforms
that bend with a radial displacement wave, and a background dot field whose density rises and
falls with that same wave, which is what produces the concentric rings.

Live: https://spankersbro.github.io/ripple-type/

## How it works

- Text is rendered to an offscreen canvas once, then uploaded as a texture — its alpha
  channel is the only thing the shader reads.
- A single GLSL fragment shader computes a radial displacement field: a constant low-amplitude
  ambient wave keeps the piece alive at rest, and up to six click-triggered ripples layer on
  top of it, each decaying by age and distance.
- Inside the text mask, the shader samples a procedural horizontal line pattern at the
  displaced UV, so the hatching bends exactly where the wave passes through.
- Outside the mask, a per-cell hashed dot field renders at a density driven by the same scalar
  wave value used for the displacement — no separate ring-drawing pass, the rings are the wave.

No build step, no dependencies. It's a single `index.html`.

## Run it locally

Open `index.html` in a browser, or serve the directory with anything static:

```bash
python3 -m http.server 8000
```

## Credit

The dot-ripple treatment is a homage to *Pluribus*'s title card, not a reproduction of any
production asset — this is an original shader built by looking at the effect and asking "how
would that work."
