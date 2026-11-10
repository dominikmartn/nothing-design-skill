# Nothing Design Skill

A design system skill for [Claude Code](https://claude.ai/code) inspired by Nothing's visual language. Monochrome, typographic, industrial.

I kept describing the same design rules to Claude over and over — Swiss typography, OLED blacks, segmented progress bars, dot-matrix motifs. So I packaged it into a reusable skill.

![Preview](preview.gif)

## What you get

Tell Claude `/nothing-design` or say "Nothing style" and it generates UI following these principles:

- Three-layer visual hierarchy (display, body, metadata — that's it)
- Space Grotesk + Space Mono + Doto font stack
- Full dark and light mode token system
- Segmented progress bars, mechanical toggles, instrument-style widgets
- Output as HTML/CSS, SwiftUI, or React/Tailwind

## Install

Copy the `nothing-design` folder into your Claude Code skills directory:

```sh
git clone https://github.com/dominikmartn/nothing-design-skill.git
cp -r nothing-design-skill/nothing-design ~/.claude/skills/
```

That's it. Next time you start Claude Code, the skill is available.

## What's inside

| File | |
|------|---|
| `SKILL.md` | Design philosophy, craft rules, workflow |
| `references/tokens.md` | Colors, fonts, spacing, motion tokens |
| `references/components.md` | Buttons, cards, lists, tables, overlays |
| `references/platform-mapping.md` | CSS, SwiftUI, React output mappings |

## License

MIT

---

Made by [@dominikmartn](https://x.com/dominikmartn) · [dominikmart.in](https://dominikmart.in/?utm_source=github&utm_medium=readme&utm_campaign=nothing-design-skill). Other projects:

- **[Ocelli](https://ocelli.app/?utm_source=github&utm_medium=readme&utm_campaign=nothing-design-skill)** · Meeting notes and dictation for your Mac
- **[hue](https://hueapp.io/?utm_source=github&utm_medium=readme&utm_campaign=nothing-design-skill)** · Drop a brand link, name or screenshot and it one shots a full design system
- **[Harp](https://github.com/dominikmartn/harp)** · Many Claude Code and Codex agents side by side, one sidebar tells you which one needs you
