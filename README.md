# 🕷️ GetBackToCinemas (GBC)

A Netflix-style, single-file movie/show trailer browser. Browse a curated catalog of upcoming films and shows, then click a card to watch its trailer in an embedded YouTube player — all in one `index.html` with no backend.

## Features

- **Netflix-inspired UI** — glassy fixed nav, full-bleed hero banner, and horizontally-scrolling content rows
- **Dynamic hero banner** — automatically pulls the catalog item flagged `hero: true` and renders its backdrop, logo, and description
- **Clickable poster/logo** — clicking the hero logo or "Watch Trailer" button launches the trailer
- **Trailer modal player** — a fullscreen modal with a themed "DECRYPTING..." preloader animation before swapping in a live YouTube iframe embed
- **Categorized rows** — catalog items are grouped into sections (e.g. "Upcoming Superhero Cinematic," "Sci-Fi & Multi-Language Discovery") with horizontally-scrolling carousels
- **Responsive layout** — card sizes, hero height, and nav collapse gracefully down to mobile breakpoints (768px and 480px)
- **Multi-language tagging** — each catalog entry carries a language chip (e.g. `EN`, `MAL`)

## Tech Stack

- Plain HTML/CSS/JS — no framework, no build tooling, no bundler
- **Vanilla JavaScript** — renders the hero and card rows from a JS array (`discoveryCatalog`) via template-string HTML generation
- **[Lucide Icons](https://lucide.dev/)** (via `unpkg.com` CDN) for nav/UI icons
- **Google Fonts (Inter)** for typography
- **YouTube IFrame embeds** for trailer playback (no YouTube API SDK — just a raw `<iframe>` src)
- Poster/thumbnail images pulled from external sources (YouTube `i.ytimg.com` thumbnails, TMDB, and other public image URLs)

## Usage

Just open `index.html` in a browser — no server, install, or API key required.

1. The page loads with a hero banner for the featured title and two scrollable rows of other titles
2. Click any poster card, the hero logo, or the "Watch Trailer" button
3. A themed preloader ("INITIALIZING THEATER... / DECRYPTING: [TITLE]...") plays for ~3 seconds
4. The YouTube trailer loads in an embedded, autoplaying iframe
5. Click the ✕ button to close the player

## How It Works

- `discoveryCatalog` is a static array of objects (`id`, `title`, `lang`, `img`, optional `hero`/`desc`), each `id` being a YouTube video ID
- `initUI()` runs on `DOMContentLoaded`, finds the hero item, injects the hero markup, then loops over defined `sections` (index ranges into the catalog) to build each row via `createCard()`
- `playVideo(id, title)` shows the modal, displays a fake-loading preloader for 3 seconds (`setTimeout`), then injects a YouTube `<iframe>` embed pointed at that video ID with `autoplay=1`
- `closeVideo()` hides the modal and clears the iframe so playback stops
- Card and hero images are hot-linked directly from external hosts (no local asset storage)

## Notes

- All video IDs currently point to public YouTube trailers/content — nothing is self-hosted
- The "DECRYPTING" preloader delay is purely cosmetic (styling flourish) and not tied to any real loading state

## Credits

Built by **ajil21** as a UI/frontend exploration project — not affiliated with any studio, network, or the films/shows referenced.

## License

For fun / educational purposes only.
<img width="540" height="360" alt="image" src="https://github.com/user-attachments/assets/56888d0b-ffe6-42e2-bbe7-3fca5032969a" />
