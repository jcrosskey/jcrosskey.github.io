---
layout: post
title:  "Use pandoc for file conversion"
categories: pandoc, markdown, html, pdf, ipynb, conversion, brew
---

The intallation (macOS) procedure can be found [here](https://pandoc.org/installing.html#macos). I personally like to write in markdown format and then convert the files into html or pdf. Following are some examples:


```bash
# -s to create a "standalone" file, with a header and footer, not just a fragment.
pandoc notes.md -f markdown -t html -s -o notes.html
pandoc notes.md -f markdown -t html -s -o notes.html --highlight-style kate

# with table of contents
pandoc notes.md -f markdown -t html -s --toc -c pandoc.css -o notes.html --highlight-style kate

# render math
pandoc notes.md -f markdown -t html -s --mathml --toc -c pandoc.css -o notes.html --highlight-style kate

# other formats
pandoc notes.md -f markdown -t latex -s -o notes.pdf
pandoc notes.md -f markdown -t latex -s -o notes.tex
pandoc notes.md -f markdown -o notes.ipynb

# LaTeX to docx
pandoc -s math.tex -o example.docx
```

## References
* [pandoc Demos](https://pandoc.org/demos.html)
* [pandoc User Guide](https://pandoc.org/MANUAL.html)
