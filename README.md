# Hitesh & Shivangi · Wedding Reception Invitation

A single-page digital wedding invitation for the reception on **28 November 2026, 7:00 PM onwards** at Hotel Golden Orchid, Ambala City.

Guests tap the royal doors to open the invitation. Background music (*Moh Moh Ke Dhaage*) then fades in, and they can scroll through the hero, the invitation message, a scratch-to-reveal date, a live countdown, the venue details with a map, directions and an add-to-calendar button, and a closing note.

## Technologies
- Plain HTML, CSS and vanilla JavaScript with no build step (`public/index.html`)
- Netlify Image CDN (`/.netlify/images`) serves resized WebP versions of the artwork in `public/img/`
- A self-hosted MP3 in `public/audio/`, played with the HTML `<audio>` element
- Google Fonts and an embedded Google Map

## Run locally
```bash
netlify dev
```
Then open the URL it prints. You need the Netlify CLI so the `/.netlify/images` URLs resolve.

## Changing the song
Replace `public/audio/moh-moh-ke-dhaage.mp3` with another MP3. If you rename the file, update the `<audio id="bgMusic">` `src` in `public/index.html` and the title in the `mediaSession` block. Keep the file small (about 1–3 MB) so it loads quickly on mobile data.
