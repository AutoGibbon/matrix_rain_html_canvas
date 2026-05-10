# matrix rain

A WebGL2 matrix rain shader. Built as a Lively Wallpaper background but it's just a single HTML file, runs anywhere a browser will load it.

## what it does

- Discrete trails: each column has trails that arrive on a schedule, traverse the screen, get evicted by the next one. Not a continuous brightness gradient.
- Head flash: white → cyan → green over half a second, decay continues into the cells immediately behind the head so they inherit the colour fade.
- Body flash: separate ramp, blown-out matrix green driven into bloom for a phosphor-burn look.
- Dark field: same map sample as the flash gate, opposite end of the range. Some cells go dim instead of bright.
- Bloom: single-pass cross kernel, weighted by luminance². No render-to-texture nonsense.
- Resolution-independent: 54 rows at any canvas height, columns scale with aspect ratio.
- CRT touches: scanlines, slow breathing zoom, per-cell brightness variance.

## tunables

All in the fragment shader as `#define`s, grouped and commented. The ones you'll actually want to touch:

- `TRAIL_GAP_MEAN` — seconds between trail arrivals per column
- `TRAIL_GAP_VAR` — burstiness; some columns dense, some quiet
- `FLASH_PROB` / `DARK_PROB` — fraction of body cells flashing/dimming
- `FLASH_BOOST` / `FLASH_BOOST_TAIL` — head/body flash brightness
- `BLOOM_STRENGTH` / `BLOOM_RADIUS` — phosphor halo
- `REF_CELL` — reference glyph size in pixels at 4K, scales to other resolutions

## use as a wallpaper

Drop `rain.html` into Lively Wallpaper as a webpage source. Should work in any other HTML wallpaper tool the same way.

## credits

Built iteratively with Claude (Anthropic). I drove the design — analysed the original film footage, set the visual goals, decided what to keep and what to rip out, tuned values to taste. Claude wrote most of the shader code and helped reason through the maths, especially the stateless trail derivation and the flash gating logic. Several rounds of "this looks wrong, why?" went into getting it where it is.

I'm open about AI-assisted work. The aesthetic decisions and architectural calls are mine; the implementation is collaborative.

## licence

MIT. Do whatever.
