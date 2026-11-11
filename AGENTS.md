# AGENTS.md

## Architecture
A static site with no build step. Netlify publishes `public/` (see `netlify.toml`).

- `public/index.html` holds all markup, CSS (in one `<style>` block) and JS (in one IIFE `<script>`). The page is split into sections: opening cover (`#intro`), `#hero`, `#invitation`, `#save-date` (heart-shaped scratch canvas), `#countdown`, `#reception`, `#closing`.
- `public/img/` holds the original artwork. Always reference it through the Image CDN: `/.netlify/images?url=/img/<file>&w=<w>&fm=webp`.
- `public/audio/moh-moh-ke-dhaage.mp3` is the background song, self-hosted. Google Drive links are not reliable for streaming audio.
- `public/reception.ics` is the calendar event (CRLF line endings, times in UTC; 7 PM IST = 13:30Z).

## Conventions and non-obvious decisions
- Music **must** start inside the "Tap to open" click handler (`Music.play()` at the top of `openInvitation`), because mobile browsers block autoplay that doesn't come from a user gesture. The floating `#musicBtn` appears once the cover has faded. Music pauses when the tab is hidden and resumes when it's visible again. iOS ignores `audio.volume`, so the fade-in only works on other platforms. That's expected.
- Tailwind CDN was removed on purpose. It was a heavy render-blocking script used by only one element. Use plain CSS with the existing `--wine/--maroon/--gold` variables.
- Add to Calendar uses the `.ics` file on Apple devices and swaps to a Google Calendar URL everywhere else (small IIFE in the script).
- Layout units use `svh`, `clamp()` and `env(safe-area-inset-*)` for phones. Keep tap targets at 44px or larger.
- z-index layers: intro 100, petals canvas 120, music button 130.
- Opening animation performance on phones: never animate `filter` (blur/brightness) or `mix-blend-mode` layers; stick to `transform`/`opacity`. The hero name shimmer is a duplicate `.names-sheen` layer (aria-hidden) with a clipped gradient. Don't put `filter: drop-shadow` on the names to fake the glow.
