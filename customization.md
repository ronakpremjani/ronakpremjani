# RonakOS — Customization Guide
<!-- RonakOS v2.0 · Customization Reference -->

```
┌─────────────────────────────────────────────────────────────────────────────┐
│   RonakOS v2.0 · Customization Reference                                    │
│   Customize every element of your GitHub profile experience                 │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## `$ color-palette`

The entire profile uses a single coherent palette. To change the accent color, find-replace `#60A5FA` across all SVG files.

| Token           | Hex       | Usage                              |
|─────────────────|───────────|────────────────────────────────────|
| `--bg`          | `#0A0A0A` | Window backgrounds                 |
| `--surface`     | `#111111` | Card surfaces                      |
| `--border`      | `#242424` | All borders                        |
| `--text`        | `#F8FAFC` | Primary text / headers             |
| `--muted`       | `#8B949E` | Secondary text / metadata          |
| `--dim`         | `#555555` | Tertiary text / decorations        |
| `--accent-blue` | `#60A5FA` | Primary accent (links, prompts)    |
| `--accent-green`| `#3FB950` | Success / IN PROGRESS indicators   |

---

## `$ section-guide`

### Banner (§01)
**File:** `assets/banner.svg`

Change the animation delays by editing `.a0` → `.a11` delay values.

```css
/* Speed up the boot sequence — halve all delays */
.a0  { animation-delay: .2s;  }
.a1  { animation-delay: .5s;  }
/* ... etc */
```

Change the title bar text:
```svg
<text x="450" y="26" class="tab-label">visitor@ronak — bash — 100×28</text>
```

---

### ASCII Identity (§02)
The RONAK ASCII art uses Unicode box-drawing characters. To regenerate or change the font style, use:
- [patorjk.com/software/taag](https://patorjk.com/software/taag/) — Font: "ANSI Shadow"
- Copy the output directly into the ` ``` ` code block in README.md

---

### Typing Animation (§02)
**Service:** [readme-typing-svg.demolab.com](https://readme-typing-svg.demolab.com)

Customize the rotating lines:
```
lines=Your+first+line.;Your+second+line.;Your+third+line.
```

Parameters you can tune:
| Param      | Current | Description          |
|------------|---------|----------------------|
| `font`     | Fira Code | Monospace font     |
| `size`     | 13      | Font size in px      |
| `duration` | 3500    | Typing speed (ms)    |
| `pause`    | 1200    | Pause between lines  |
| `color`    | 60A5FA  | Text color (no `#`)  |
| `width`    | 560     | SVG width in px      |

---

### Tech Stack (§06)
Edit the JavaScript object in `README.md` directly. It's plain text inside a ` ```javascript ``` ` code fence — no rebuilding needed.

---

### Project Cards (§07)
**Files:** `assets/project-chatvia.svg`, `assets/project-portfolio.svg`

To add a third project card:
1. Duplicate `project-chatvia.svg` → rename to `project-yourproject.svg`
2. Change the accent gradient color (`borderGrad`)
3. Update all text content
4. Add a third `<td>` in the `<table>` in README.md, or create a new row

To change the status pill color/label:
```svg
<!-- Find and edit this block -->
<rect x="290" y="-14" width="120" height="20" rx="10" fill="#0D2818"/>
<text x="302" y="-1" class="ct card-status">● IN PROGRESS</text>

<!-- Options: -->
<!-- fill="#0D2818" + stroke="#1A4A2A" → green pill (IN PROGRESS) -->
<!-- fill="#0A1E2A" + stroke="#1A4A6A" → blue pill (PORTFOLIO)    -->
<!-- fill="#1E1A0A" + stroke="#4A3A1A" → amber pill (PLANNED)     -->
<!-- fill="#1E0A0A" + stroke="#4A1A1A" → red pill (DEPRECATED)    -->
```

---

### Roadmap (§08)
The progress bars are plain Unicode characters inside a code fence. To update:

```
████████████████████░░░░░░   78%
```

| Character | Meaning    |
|-----------|------------|
| `█`       | Filled     |
| `░`       | Empty      |

Each full bar = 26 characters. Calculate: `Math.floor(percent / 100 * 26)` filled blocks.

---

### GitHub Stats (§09)
Replace `ronakpremjani` with your actual GitHub username in all stat URLs.

```
https://github-readme-stats.vercel.app/api?username=YOUR_USERNAME
https://streak-stats.demolab.com?user=YOUR_USERNAME
https://github-readme-activity-graph.vercel.app/graph?username=YOUR_USERNAME
```

---

### Contribution Snake (§09)
The snake animation requires a GitHub Actions workflow. See `setup.md` for instructions.

---

## `$ typography`

The profile uses system monospace fonts in this priority order:
1. `SF Mono` (macOS/iOS)
2. `Fira Code` (cross-platform, most common)
3. `JetBrains Mono` (JetBrains IDEs)
4. `Cascadia Code` (Windows Terminal)
5. `Menlo` (older macOS fallback)
6. `monospace` (system fallback)

This ensures the profile looks great on any OS without loading external fonts (GitHub blocks Google Fonts in SVGs).

---

## `$ adding-sections`

Every new section follows this pattern:

```markdown
### `$ your-section-name`

\`\`\`
┌─────────────────────────────────────────────────────────────────────────────┐
│                                                                             │
│   YOUR SECTION HEADER                                                       │
│   ───────────────────                                                       │
│                                                                             │
│   Content goes here                                                         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
\`\`\`

<br/>

<div align="center">
  <img src="./assets/divider.svg" alt="" width="100%" />
</div>

<br/>
```

The box border uses these Unicode characters:
- `┌` `─` `┐` (top)
- `│` (sides)
- `├` `┤` (horizontal divider inside box)
- `└` `─` `┘` (bottom)

---

_RonakOS v2.0 · Crafted with intention_
