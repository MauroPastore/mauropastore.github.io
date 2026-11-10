# Academic CV website

A small, hand-made Jekyll site: four pages (Home, Research, Teaching, Other activities),
one CSS file, no theme and no plugins. GitHub Pages builds it as it is.

All the content lives in a few YAML files in `_data/`; the HTML files only decide how it is laid out.

## Files

| File | What it contains |
|---|---|
| `_config.yml` | Name, position, affiliation (full and short), address, email, profile photo, CV link, profile links, menu |
| `index.html` | Home page. The biography is the Markdown block at the top, between `{% capture bio %}` and `{% endcapture %}` |
| `research.html` | Research page layout: summary, then one section per theme with its picture and publications |
| `teaching.html` | Teaching page layout |
| `activities.html` | Other activities page layout |
| `_data/cv.yml` | Home page lists: interests, news, positions, education, awards |
| `_data/research.yml` | Research summary, themes, publications, talks, grants |
| `_data/teaching.yml` | Teaching statement, courses, schools, supervision, material |
| `_data/activities.yml` | Collective actions, organisation, committees, refereeing, outreach |
| `_layouts/default.html` | The frame of every page: header, menu, footer |
| `_includes/entries.html` | Draws the dated lists used on every page |
| `_includes/pubs.html` | Draws a numbered publication list |
| `assets/style.css` | All the styling. Colours are at the top |
| `images/` | Profile photo, theme pictures, logos, figures |
| `files/` | PDFs to link to: CV, papers, slides, notes |
| `404.html` | Page shown for a wrong address |

## Writing text

Free-text fields accept Markdown: `summary`, `text`, `statement`, `details`, `caption` and the news `text`.
For anything longer than a line, use YAML's block style: a `|` after the field name, then the text
on the following lines, indented, with an empty line between paragraphs.

```yaml
text: |
  First paragraph with *italics*, **bold** and a [link](https://example.org).

  - a list item
  - another one
```

Titles are plain text, but HTML works in them, for example `QCD<sub>2</sub>`.

Delete a list in any YAML file and its section disappears from the page.

## Dated entries

Positions, education, awards, talks, grants, courses, schools, supervision, organisation,
committees and outreach all use the same fields:

```yaml
- period: "2026"                         # shown in the left column
  title: "Workshop on Topic"
  url: "https://indico.ictp.it/event/1"  # optional: makes the title a link
  place: "ICTP, Trieste, co-organiser"   # optional
  details: "Markdown text shown in grey below."       # optional
  image: "/images/workshop-2026.jpg"     # optional picture below the entry
  image_alt: "Description of the picture, for screen readers"
  caption: "Optional caption, Markdown allowed."
```

## Research themes and publications

Each theme has a short `id`, and a picture that floats to the right of its text:

```yaml
themes:
  - id: feature-learning
    title: "Asymptotics of feature learning in deep neural networks"
    image: "/images/theme-deep-learning.gif"
    image_alt: "Animated deep neural network lighting up layer by layer"
    image_full: true          # optional: picture at full width instead of on the side
    text: |
      One or two sentences on this line of research.
```

Tag each publication with the themes it belongs to. It is listed under each of them, newest first.
Publications without `themes` appear under "Other publications" at the end.

```yaml
publications:
  - type: article             # preprint | article | proceedings | book | thesis
    themes: [feature-learning, structured-data]
    authors: "Y. Name, A. Coauthor"
    title: "Title of the article"
    venue: "Physical Review Letters 130, 123456"
    year: 2025
    doi: "10.1103/PhysRevLett.130.123456"   # just the DOI
    arxiv: "2409.00002"                     # just the arXiv number
    pdf: "/files/paper.pdf"                 # a file in files/
    url: "https://example.org/paper"        # any other link, shown as "Link"
```

All four link fields are optional.

## Other activities

**Collective actions** have an optional logo and a description:

```yaml
actions:
  - title: "Slow Science"
    url: "https://www.slow-science.com/"
    role: "Promoter"
    logo: "/images/logo-slow-science.png"   # optional
    text: "What the initiative is about (Markdown)."
```

**Refereeing** is a plain list of journal or agency names.

The other sections are dated entries (see above).

## Pictures

- **Profile photo:** set `photo:` in `_config.yml` (e.g. `/images/profile.jpg`). It is shown
  as a circle, so a square crop works best. Leave it empty to hide.
- **Theme pictures, logos and entry figures:** put the files in `images/` and refer to them
  as `/images/name.ext`.
- Keep photos under about 500 KB (1600 px wide is plenty). GIF, SVG, PNG, JPG and WebP all work.

## Preview locally

```bash
bundle config set --local path 'vendor/bundle'
bundle install
bundle exec jekyll serve
# open http://localhost:4000
```

Changes appear when you refresh the browser, except changes to `_config.yml`:
for those, stop the server (Ctrl+C) and start it again.

## Publish on GitHub Pages

1. Create a repository named `<username>.github.io`. With any other name, set
   `baseurl: "/<repo>"` in `_config.yml`.
2. Push this folder to the `main` branch.
3. On GitHub, go to **Settings → Pages**, set **Source: Deploy from a branch**,
   branch `main`, folder `/ (root)`.

The site is live at `https://<username>.github.io` a minute or two after each push.
