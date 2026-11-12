# MotionStock All in One

Single-page bundle of 5 stock tools for microstock work. Blue theme by default.
**Live link / repo: NOT deployed yet — parent deploys after review.**

## Files

- `index.html` — obfuscated publish file (318,669 bytes). The ONLY file that goes public.
- `_source/index.html` — clean app shell (top bar, left icon rail, 8 lava themes, license gate, tool switching).
- `parts/tool-1-poster.js` — Poster Set (457 presets)
- `parts/tool-2-jpg.js` — JPG Studio (76 styles)
- `parts/tool-3-png.js` — PNG Studio (40 modes)
- `parts/tool-4-pattern.js` — Seamless Pattern (157 presets)
- `parts/tool-5-calendar.js` — Event Calendar (130 events)
- `license-generator.html` — **PRIVATE seller file. NEVER upload to GitHub.** Generates AIO license keys.

## Rebuild

```bash
node ~/workspace/tools/obfuscator/build-allinone-publish.js
```

Concatenates shell + 5 parts, obfuscates, writes `index.html`, and fails loudly
if the AIO license secret appears in plain text.

## License gate

`GATE_ON = false` in `_source/index.html` (open by default). Set it to `true`,
rebuild, redeploy to lock the app behind an activation key. Keys are
`AIO-<1M|2M|12M>-<expiry base36>-<rand4>-<check6>` (cyrb53, secret `AIO_SECRET`
lives only in `_source` + `license-generator.html`). Generate keys with
`license-generator.html` — never share that file.

## Verification done (2026-11-12, node only)

- `node --check` passes on all 5 parts, the combined clean JS, and the built
  obfuscated script.
- Counts verified: Poster 457 (all 12 category counts + New 73), JPG 76 styles,
  PNG 40 modes, Pattern 157 presets, Calendar 130 events.
- Poster preview SVG == export SVG for presets #1, #56, #199, #383, #456
  (normalized compare, grain on).
- JFIF 300 DPI patch verified for JPG + Pattern (units=1, 300x300).
- License round-trip verified: generated 1M/2M/12M keys verify; bad and
  PSP-style keys rejected.
- **NOT yet verified: live browser smoke test.** `mount()` for Poster, PNG,
  Pattern and Calendar was verified only with DOM stubs / statically (JPG
  mount was stub-tested). Before/after deploy, open the site in a real
  browser, switch through all 5 tools, click a preset/style/mode, and
  download one JPG/SVG/PNG from each export tool.

## Deploy (for the parent)

Create repo `motionstock-all-in-one`, push ONLY `index.html` (+ a README).
Enable GitHub Pages. Optional: Cloudflare Pages for a username-free link.
Never push `_source/`, `parts/` or `license-generator.html`.
