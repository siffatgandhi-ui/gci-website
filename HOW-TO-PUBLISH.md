# Publishing the GCI site

`index.html` is the whole website — one self-contained file. All images, CSS and
JavaScript are embedded. No build step, no server, no dependencies. Any static
host will serve it.

Keep `preview.jpg` next to it — that's the image shown when the link is pasted
into WhatsApp, LinkedIn or email.

---

## Fastest — Netlify Drop (about 30 seconds, no terminal)

1. Go to **https://app.netlify.com/drop**
2. Drag this whole `GCI_site_deploy` folder onto the page.
3. You get a public link immediately, e.g. `https://cheerful-otter-1a2b3c.netlify.app`

Without an account the link expires in about an hour. Sign up (free) and it
becomes permanent, and you can rename it to something like
`golden-choice-impex.netlify.app` under **Site settings → Change site name**.

## Cloudflare Pages — free, fast in India

1. **https://pages.cloudflare.com** → Create a project → *Upload assets*
2. Upload the folder. You get `your-project.pages.dev`.

## GitHub Pages

1. Create a repository, upload `index.html` and `preview.jpg`.
2. **Settings → Pages → Source: main branch / root**.
3. Live at `https://<username>.github.io/<repo>/` in a minute or two.

---

## Putting it on goldenchoiceimpex.com

Any of the hosts above can serve the real domain:

- **Netlify / Cloudflare Pages** → add a custom domain in the dashboard, then
  point the DNS record they give you at it.
- **Existing hosting** → whoever manages the current site can drop `index.html`
  and `preview.jpg` into the web root. That's the entire deployment.

Once the real domain is live, change this line in `index.html` to the full URL so
link previews resolve correctly:

    <meta property="og:image" content="preview.jpg">
    →
    <meta property="og:image" content="https://goldenchoiceimpex.com/preview.jpg">

---

## Before it goes live on the real domain

- **The enquiry form** opens the visitor's mail client (a `mailto:` link). It does
  not submit anywhere. For real form submissions, a service like Formspree or
  Netlify Forms takes about ten minutes to wire up.
- **Headcount** — the brochure says 386, the brand Q&A says 200+. The page
  currently says "380+ across the group". Confirm which is right.
- **The logo** on this page is a redrawn proposal, not the approved vector
  master. Get sign-off before it represents the company publicly.

---

## Editing later

Don't hand-edit `index.html` — the images are inlined as base64 and it's a
1 MB file. Edit the source instead:

    ~/Desktop/GCI_Website_v3_source-no-images.html   (~60 KB, images are @@tokens@@)

then re-run the build script, which regenerates both this folder and the
shareable Claude artifact from that one source:

    python3 ~/Desktop/GCI_build.py

---

## Adding your stitching / leather footage

The site has a video slot ready in **The Seam** section. Right now it plays a
cross-dissolve of your macro photography; drop in real footage and the video
takes over automatically.

1. Put the file next to `index.html`, e.g. `stitching.mp4`.
2. In `index.html`, find `id="seamVideo"` and add one line inside the tag:

       <video class="seam__v" id="seamVideo" muted loop playsinline preload="none">
         <source src="stitching.mp4" type="video/mp4">
       </video>

That's it. If the file is missing or won't play, it silently falls back to the
stills — so it can never leave a blank section.

**What to shoot** (phone is fine, shoot horizontal):
- Needle going through leather, close and slow — 10s
- Hands guiding a panel through the machine — 10s
- A finished seat cover being pulled taut over foam — 8s
- Cutting table, blade following the pattern — 8s

**Encoding:** H.264 MP4, 1920x1080 or 1280x720, no audio track, 8-15 seconds,
under ~3 MB each. Keep it muted and looping — it is background texture, not a
film. If you have HEVC/.MOV from an iPhone, it needs converting to H.264 or
Chrome and Firefox will not play it.

Do not use stock footage of someone else's factory. An OEM buyer who recognises
it is a problem you do not want.

---

## Media credits & licensing

`media/` contains three atmosphere clips sourced from **Pexels**, whose licence
permits commercial use without attribution:

| File | Subject | Source |
|---|---|---|
| `stitch-machine.mp4` | Sewing machine, needle and presser foot | pexels.com/video/8170061 |
| `leather-hand.mp4` | Hand-stitching leather pieces | pexels.com/video/4456103 |
| `cabin.mp4` | Car interior, leather seat detail | pexels.com/video/6157907 |

These are **atmosphere, not documentation** — they are never captioned as GCI's
own floor or product. Every product card, every factory tile and every figure on
the site is GCI's own material from the brochure.

Replace any of these with real GCI footage whenever you have it: keep the same
filename in `media/` and nothing else needs to change. Doing so is a straight
upgrade — your own line is always more persuasive to a buyer than stock.

Keep the attribution table above accurate if you swap files in or out.

---

## Typefaces

Three tiers, deliberately distinct so a heading always reads as a heading:

| Role | Face | Notes |
|---|---|---|
| Headings, display figures | **Archivo** (variable) | Embedded in the page as a base64 woff2. Width axis 104–118 and weight 700–800 do the work. |
| Body copy | Helvetica Neue | Brand guideline face, unchanged. |
| Labels, specs, item codes | System monospace | Unchanged. |

Archivo is licensed under the **SIL Open Font License 1.1** — free for commercial
use and embedding. Source: fonts.google.com/specimen/Archivo.

**Note for Curly Concept:** the 2026 brand guideline specifies Helvetica Bold for
headlines. Archivo is a deliberate deviation, requested to give headings more
presence. The logo wordmark still uses Helvetica exactly as specified. Worth a
sign-off before this becomes the standard.
