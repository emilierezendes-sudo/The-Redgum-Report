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

**All 54 photo slots are filled.** They were imported from the Claude Design
project export, so the site is complete as it stands.

The files are **WebP** (`.webp`), not JPEG — that's the format the design editor
stored them in. Every current browser handles WebP fine. They're capped at
1200px on the long edge because the design editor re-compressed them on upload.

## Replacing a photo

Drop a new file into `uploads/` using the **exact filename** below, replacing
the old one. If your new photo is a `.jpg`, you have two options:

1. Rename it to `.webp` — **this does not work**, renaming doesn't convert the
   format. Don't do this.
2. Either convert it to WebP first, **or** keep it as `.jpg` and edit the one
   `src="uploads/….webp"` line in the HTML to say `.jpg` instead. The second is
   easier if you're only changing one or two.

Two rules that will bite you otherwise:

- **Lowercase filenames and extensions.** Web hosts are case-sensitive even
  though Windows isn't. `Photo-Journal-1.webp` or `photo-1.JPG` will work when
  you double-click locally and then break once published.
- **Keep photos under ~500 KB.** If you swap in a full-size phone photo (3–5 MB),
  the page gets slow on cell data. Resize the long edge to about 1600px.

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
