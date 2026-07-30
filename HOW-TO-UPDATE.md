# The Redgum Report — how to update the site

Mostly plain HTML files you can edit in Notepad. The **newsletter** is different
— it's written in Markdown (plain text), and GitHub turns it into the styled page
for you. That's the one you'll edit most, and it's the easiest.

## The pages

| File | What it is |
|---|---|
| `newsletter-post.md` | **The newsletter — plain text, write freely.** |
| `book-review.md` | **This month's Author of the Month — a form you fill in.** |
| `_authors/*.md` | **One file per past author.** The archive page builds itself from these. |
| `index.html` | Home page (hero, About, photo previews, subscribe form) — still HTML |
| `photo-journal.html` | Full photo grid — still HTML |
| `book-review-archive.html` | Just a title; the content comes from `_authors/` |
| `style.css` | Shared styling. You normally don't need to touch this. |
| `_layouts/`, `_config.yml` | Machinery that wraps your writing in the site design. Leave alone. |

## Writing the newsletter

Open `newsletter-post.md`. The top block between the `---` lines sets the
headline and labels; everything below it is just your writing.

```
---
layout: newsletter
title: The One Where the Fence Finally Falls Down
kicker: Newsletter · July 2026
byline: Written on a Sunday, mostly true
topics: [Family, Garden, Dispatch]
---

Just type paragraphs. Leave a blank line between them.

> Start a line with > to make it a pull-quote.
```

Only `layout:` must stay exactly as it is. Change `title`, `kicker`, `byline`
and `topics` freely — `topics` are the little pills at the bottom, and you can
list as many or as few as you like.

Formatting you can use in the body:

| You type | You get |
|---|---|
| blank line between paragraphs | separate paragraphs |
| `> some text` | a pull-quote (big italic teal, orange bar) |
| `## A heading` | a section heading |
| `*words*` | *italic* |
| `**words**` | **bold** |
| `[text](https://example.com)` | a link |
| `- item` on each line | a bulleted list |

Straight quotes and `--` are converted to proper curly quotes and dashes
automatically, so don't worry about typing them fancy.

**For next month:** copy `newsletter-post.md` somewhere safe if you want to keep
the old one, then just rewrite it. (Ask me if you'd like a proper archive of past
dispatches — that's a small addition.)

**Editing in a browser instead:** on github.com open `newsletter-post.md` and
click the pencil icon. There's a Preview tab, and Commit changes publishes it.
Works from a phone, and nothing to install.

## A new Author of the Month

**You never move anything to the archive.** This Month's Pick shows whichever
file in `_authors/` has the highest `order`. Add next month's file and it becomes
the pick; last month's drops into the archive on its own.

So the whole job is: create one file in `_authors/`. Copy
`_authors/anthony-horowitz.md` and change the values — it has a comment above
each field saying where it lands on the page.

```
---
title: 'Anthony Horowitz'
slug: anthony-horowitz
order: 15
photos:
  - file: anthony-horowitz-photo-1.webp
  - file: anthony-horowitz-photo-2.webp

intro: |
  The cream box at the top. Optional.

author_bio: |
  Shown beside the round photo.

book: Alex Rider
book_meta: Spy Thriller · Book Series
book_summary: |
  One paragraph, or several with a blank line between.

verdict_title: Hard to Put Down
verdict_badge: Recommend
verdict: |
  What you actually thought.

closing: Until next month's stack — happy reading.
---
```

Things that matter:

- **`order` must be higher than every other author** — that's what makes it this
  month's pick. Next one is 16, then 17.
- **`slug` must match the filename** without `.md`. It's the archive link target.
- **`photos`: the first is the author** (shown round), **the second is the book
  cover** (shown square). A third is optional and only shows in the archive.
- **Name photos after the author** — `anthony-horowitz-photo-1.webp`, not
  `author-photo.webp`. Reusing a generic name would make old archive entries
  show the new month's photos.
- The `|` after a field name means "the indented text below is the value". Keep
  the indentation, and leave a blank line between paragraphs.
- `verdict_badge` is the little pill. Any words work ("Would Not Reread"). Add
  `verdict_badge_color: '#8a4526'` for a rust pill instead of teal.

Older author files are written differently — plain prose in the body with
`## headings` instead of labelled fields. Both styles render fine, so there's no
need to convert them. Two marks you'll see in those: `{: .rr-lead}` after a
paragraph makes it an italic lead-in, `{: .rr-sig}` makes it a small italic
signature.

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

## Keeping past newsletters

Right now there's one newsletter page, and writing next month's means rewriting
`newsletter-post.md` — the old dispatch is replaced (though every version stays
in the repo's history, so nothing is truly lost).

If you'd like past dispatches to stay on the site with their own pages and an
index listing them, that's a worthwhile addition and not much work — ask when
you want it.
