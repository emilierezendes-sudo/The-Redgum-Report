# The Redgum Report — how to update the site

The site is five plain HTML files. No build step, no tools needed — open any
`.html` file in a text editor (Notepad works) to change text, or replace a file
in `uploads/` to change a picture.

## The pages

| File | What it is |
|---|---|
| `index.html` | Home page (hero, About, photo previews, subscribe form) |
| `newsletter-post.html` | The current newsletter dispatch |
| `book-review.html` | This month's Author of the Month |
| `book-review-archive.html` | All 14 past authors, with jump-links |
| `photo-journal.html` | Full photo grid |
| `style.css` | Shared rules that make the pages work on phones/tablets. You normally don't need to touch this. |

## Photos — current state

Mixed formats, for a reason:

- **Archive photos are `.jpg`**, 640px on the long edge. These are your
  replacement photos, downscaled — the thumbnails render at only 244×183, so
  640px is already about 2.6× more detail than any screen shows.
- **Everything else is `.webp`** — those came out of the Claude Design export
  in that format.

**15 archive photos are deliberately absent.** The design-export versions were
too low-resolution and looked soft, so they were removed rather than shown
blurry. Their slots were taken out of the page too, so nothing looks broken —
every author still has 1–3 photos. To fill one back in, drop a photo into
`uploads/` and say so; the markup has to be re-added for it to appear.

Nothing is lost: the low-res originals are in commit `5da8879`, and the
full-size replacements in `99dd5e0`.

## Replacing a photo

Drop a new file into `uploads/` using the **exact filename** below, replacing
the old one. Match the existing extension (`.jpg` for archive photos, `.webp`
for the rest) — or use any extension and tell me, and I'll update the one
`src="uploads/…"` line that points at it. Note that **renaming a `.jpg` to
`.webp` does not convert it** and will break the image.

Three rules that will bite you otherwise:

- **Lowercase filenames and extensions.** Web hosts are case-sensitive even
  though Windows isn't. `Photo-Journal-1.webp` or `photo-1.JPG` will work when
  you double-click locally and then break once published.
- **Around 800px on the long edge is plenty**, and keep files under ~150 KB.
  A full-size phone photo (3–5 MB) makes the page slow on cell data for no
  visible gain — the archive thumbnails are tiny.
- **Put it in `C:\Users\emili\projects\redgum-report\uploads\`.** That is the
  live folder. Anything under OneDrive is not connected to the site.

### Filenames

**Home page**
- `about-portrait.webp` — round portrait in the About section

**Photo Journal** — two wide, seven tall
| Filename | Shape | Caption |
|---|---|---|
| `photo-journal-1.webp` | **wide** | Bouncing down the mountain at sunset |
| `photo-journal-2.webp` | tall | Corduroy in Yosemite |
| `photo-journal-3.webp` | tall | Flowers :) |
| `photo-journal-4.webp` | tall | More flowers :) |
| `photo-journal-5.webp` | **wide** | Grapevine lake, at sunset |
| `photo-journal-6.webp` | tall | Me, on a walk |
| `photo-journal-7.webp` | tall | O beautiful America |
| `photo-journal-8.webp` | tall | Cailie and I, ain't she cute?! |
| `photo-journal-9.webp` | tall | Houston skyline |

Numbers 1–4 also fill the preview row on the home page, so those four appear on
both pages.

**This month's book review**
- `author-photo.webp` — round author portrait
- `book-cover.webp` — book cover (square)

**Book review archive** — three per author, slightly wide (4:3):
`<author>-photo-1.webp`, `-2`, `-3`, where `<author>` is one of:

`jeanne-birdsall`, `jane-austen`, `james-herriot`, `tolkien`,
`darlene-deibler-rose`, `conan-doyle`, `fred-gipson`, `lynn-austin`,
`eric-blehm`, `katie-davis-majors`, `diana-wynne-jones`, `eoin-colfer`,
`chesterton`, `cressida-cowell`

Example: `uploads/jane-austen-photo-2.webp`

## A note on photo framing

17 of the imported photos had a custom crop applied in the design editor (you'd
dragged them to reposition). Those crops were converted to CSS
`object-position` values, so the framing should match what you set up. If you
**replace** one of those photos, the old crop still applies and may frame the new
photo oddly — look for `object-position` on that image's line and delete it to
go back to plain centring.

## Changing captions or text

Open the page in a text editor and find the words you want to change — they sit
between HTML tags like `<figcaption ...>Flowers :)</figcaption>`. Change only
the words, leave the `<...>` parts alone.

## The email signup

The subscribe form on `index.html` posts to Buttondown
(account: `TheRedgumReport`). New subscribers appear in your Buttondown
dashboard automatically. If you ever rename the account, update the username in
two places in `index.html` — the form's `action=` URL and its `onsubmit` URL.

## Publishing the site (Netlify Drop)

Fastest way to get a public link, free, no command line:

1. Go to <https://app.netlify.com/drop>
2. Drag the whole `website` folder onto the page.
3. Wait a few seconds — you get a live URL like `random-name-123.netlify.app`.
4. To keep that URL permanently (and to be able to re-upload updates), create a
   free Netlify account when it prompts you. Without an account the link is
   temporary.
5. In Site configuration → Change site name, pick something nicer, e.g.
   `redgum-report.netlify.app`.

To publish updates later: drag the folder onto the same Drop page again while
signed in, or use "Deploys → Drag and drop" inside your site's dashboard.

If you'd rather have your own domain (`theredgumreport.com`), you buy it from a
registrar and point it at Netlify in Domain settings — worth asking for help
with when you get there.

## Adding a new month's newsletter

Easiest approach: copy `newsletter-post.html` to a new name (e.g.
`newsletter-2026-08.html`), edit the headline, date and body text in the copy,
then update the "Newsletter" links in the nav of each page to point at the
newest one. (If you'd rather have a proper list of past dispatches, that's a
small addition worth asking for.)
