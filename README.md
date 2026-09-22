# Old-school static homepage

The homepage uses only HTML and CSS. The Notes reader uses a small amount of JavaScript plus Marked to fetch and render `.md` files.

Run locally:

```bash
python3 -m http.server 5173 --bind 127.0.0.1
```

Open <http://localhost:5173/>.

## Add a note

1. Add `notes/my-note.md`.
2. Add a link in `notes/index.html`:

```html
<a href="read.html?file=my-note">My note</a>
```

The reader only accepts simple file names containing letters, numbers, and hyphens.
