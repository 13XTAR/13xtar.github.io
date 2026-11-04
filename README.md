# 13XTAR — Cinematic Portfolio (working build)

A mobile-first, dark cinematic portfolio for GitHub Pages, with a phone-friendly Pages CMS editing setup and an optional AI-generated original movie-art workflow.

## What is included
- Cinematic YouTube hero using the supplied video, with muted autoplay/loop requested (browser playback rules still apply).
- Photography journal with filters, a full-size lightbox, and a subtle 13XTAR signature overlay.
- Cinematography film gallery driven by `content/videos.json`, vertical Shorts embeds, five supplied YouTube Music playlists, mood links, and social profile links.
- Editable JSON content files for the homepage, photos, videos, playlists, and movies.
- `.pages.yml` configuration for Pages CMS.
- Optional GitHub Actions workflow that generates original, vertical movie-shelf artwork for entries whose `poster` field is blank.
- Cinematic motion system: animated hero orbit, scrolling marquee, scroll progress, reveal transitions, desktop pointer response, active section navigation, and back-to-top control.
- Separate photography portfolio with a keyboard-accessible full-size lightbox, branded favicon, custom 404 page, responsive mobile layout, Blur Mode OFF by default, and reduced-motion support.

## Content editing (Pages CMS)
The CMS reads `.pages.yml` from the repository root. The website reads the JSON files inside `content/`; the CMS config alone does not render site content.

- `content/site.json`: homepage headline, description, hero video, and social links.
- `content/photos.json`: photos and their categories.
- `content/videos.json`: YouTube video IDs and descriptions, rendered in the Films & Cinematography section.
- `content/site.json`: the `heroVideoUrl` field controls the homepage showreel; the hero remains muted and loops when browser autoplay rules allow.
- `content/playlists.json`: playlist names, moods, and playlist IDs.
- `content/movies.json`: your Movie Shelf. Add a title, year, genre, and optional poster mood description. Leave `poster` blank to request AI artwork.

Photos can use a full `https://` image URL or a file uploaded into `assets/uploads/`. The `13XTAR` signature is a site overlay, not a claim that an uploaded photo was AI-generated.

## AI movie artwork: one-time setup required
The AI workflow is intentionally optional and does not expose an API key in the public site.

1. Create an API key with an image-generation provider that supports the OpenAI Images API.
2. In the GitHub repository, open **Settings → Secrets and variables → Actions → New repository secret**.
3. Name the secret exactly `OPENAI_API_KEY` and paste the key as its value. Never put this key in `index.html`, JSON files, or Pages CMS content.
4. Ensure GitHub Actions are enabled for the repository.
5. Add a movie in Pages CMS with `poster` left blank. When `content/movies.json` is committed, the workflow generates up to three missing posters per run and commits the artwork into `assets/uploads/posters/`. If more than three need generating, run **Actions → Generate original movie-shelf artwork → Run workflow** again.

**Cost and output:** Image generation through the API is not guaranteed to be free and can incur usage charges. Check the provider's current pricing before enabling it. The workflow generates original editorial artwork, not an official studio poster; it asks for no actor likenesses, copied poster layouts, logos, or text. The site overlays the movie title separately. Review each generated image before using it publicly.

If no API key is configured, the website still works and the CMS still edits content; only automatic poster generation is skipped.

## Local/preview notes
The editable content loader uses `fetch()` to read JSON files, so preview it through a web server or after deployment; opening `index.html` directly as a `file://` URL may show the built-in starter content instead.

## Deployment
The project is configured for GitHub Pages from the `main` branch and repository root. New commits trigger the Pages build-and-deployment workflow. If Pages is not enabled, open **Repository Settings → Pages**, choose **Deploy from a branch**, select `main` and `/(root)`, then save.

## Editing the site
Open Pages CMS, sign in with the GitHub account that has write access to this repository, and select `13XTAR/13xtar.github.io`. Edit the Homepage, Photography, Cinematography videos, Music playlists, or Movie Shelf collections and save the changes. The site reads those JSON files automatically after deployment.

## Safety and service notes
- Never commit passwords, personal documents, access tokens, or API keys.
- Keep GitHub two-factor authentication enabled.
- YouTube controls video playback, ads, availability, and quality; 4K depends on the source video.
- The animated music bars are decorative, not audio-reactive.
- Instagram cards are profile links, not fake auto-updating feeds.
- Blur Mode is off by default to keep the page lighter on mobile.
