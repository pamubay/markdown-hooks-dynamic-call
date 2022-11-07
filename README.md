## Bug

`.Content` doesnt rebuild when dynamically-called partial template inside markdown render hooks modified.

## How-to reproduce

1. start `hugo server`, then open browser.
2. modify `layouts/partials/dynamic-render-link.html`,
3. Add some random character
4. Changes detected, site rebuild but `.Content` doesnt update with new changes

All markdown hooks affected, `link`,`image`, `heading`, `codeblock`. 

Also tested using `--disableFastRender` still __doesnt work__.

---

**layouts/_default/_markup/render-link.html**

```
{{/* partial template dynamic call */}}
{{- partial (print "dynamic-render-link.html") . -}}
```

---

__Structure:__

```
.
├── config.toml
├── content
│   └── _index.md
├── layouts
│   ├── _default
│   │   ├── home.html
│   │   └── _markup
│   │       ├── render-codeblock.html
│   │       ├── render-heading.html
│   │       ├── render-image.html
│   │       └── render-link.html
│   └── partials
│       ├── dynamic-render-codeblock.html
│       ├── dynamic-render-heading.html
│       ├── dynamic-render-image.html
│       └── dynamic-render-link.html
└── README.md

```
