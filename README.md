# .antiui — The Direct Property Injection (DPI) Protocol

"Tailwind is a dictionary for a language you already speak. We cut the middleman."

**.antiui** is a high-performance, type-safe CSS protocol designed for the post-utility era. It is a **Direct Property Injection (DPI)** engine that eliminates the abstraction layer between developer intent and browser rendering. No translation, no proprietary class-name mapping, no bloat.

---

## Manifesto — Death to the Middleman

For the last decade, developers have been forced to map their thoughts to proprietary class names.

* **The Problem:** You learned `leading-tight` instead of `line-height: 1.25`. You learned `p-4` instead of `padding: 16px`.
* **The Result:** Mental friction, "class soup," and massive CSS bundles filled with unused code.
* **The Solution:** .antiui treats the HTML attribute as a first-class style instruction. It uses a **Single-String Injection** model where the string *is* the logic.

---

## Core Architecture — The Ghost JIT Engine

The heart of .antiui is a **Non-Blocking Mutation Cycle**. It is "ghostly"—it only generates CSS for the properties currently rendered on your screen.

1. **Detection:** A high-speed `MutationObserver` identifies elements with the `ui` attribute.
2. **Parsing:** The engine splits the string by `;` and `:` tokens.
3. **Atomic Hashing:** It hashes the Property-Value-Modifier triplet (e.g., `bg:#000`) to create a deterministic atomic token.
4. **VirtualSheet Linkage:** Styles are injected into a single Constructable Stylesheet via `CSSStyleSheet.insertRule()`.

---

## The Shorthand Protocol

Frequent CSS properties are collapsed into concise short-codes. To maintain valid attribute strings, **underscores (`_`)** are used to represent spaces.

### Structural Primitives

* `<row>` — Flex row container.
* `<col>` — Flex column container.
* `<box>` — The universal container.
* `<text>` — Typography-optimized block.

### Property Mapping

| Property | Short-Code | String Token Example | Result |
| --- | --- | --- | --- |
| **Flex** | `f:` | `f:center` | `align-items: center; justify-content: center;` |
| **Padding** | `p:` | `p:20px_40px` | `padding: 20px 40px;` |
| **Background** | `bg:` | `bg:#111` | `background: #111;` |
| **Radius** | `r:` | `r:full` | `border-radius: 9999px;` |
| **Gap** | `g:` | `g:12px` | `gap: 12px;` |
| **Color** | `c:` | `c:#eee` | `color: #eee;` |
| **Border** | `b:` | `b:1px_solid_#333` | `border: 1px solid #333;` |

---

## "Never Seen Before" Features

### Fluid Typography (`~`)

Write a range and the engine produces a `clamp()` that scales between breakpoints automatically.
`ui="size:16~32"` -> `font-size: clamp(16px, ..., 32px)`

### Linear Gradient Pipes (`|`)

Quickly define gradients using pipes.
`ui="bg:grad(r|#000|#fff)"` -> `linear-gradient(to right, #000, #fff)`

### State-Chain Modifiers (`.`)

Chain states directly inside the string using dot-notation:

* **Hover:** `bg.h:blue`
* **Active:** `scale.a:0.95`
* **Focus:** `b.f:2px_blue`

---

## Usage

### React / JSX

The `@dotantiui/react` components focus on the `ui` prop for maximum portability.

```tsx
import { Box, Row, Text } from '@dotantiui/react';

const Card = () => (
  <Box ui="bg:#111; p:24px; r:16px; b:1px_solid_#333;">
    <Row ui="g:12px; f:center-y;">
      <Box ui="w:40px; h:40px; bg:blue; r:full;" />
      <Text ui="size:14~18; c:#eee; w:600;">
        User Profile
      </Text>
    </Row>
  </Box>
);

```

### Static Trace CLI

For zero-runtime production builds, statically trace your source to emit a compiled CSS file.

```bash
npx anti-ui build --input ./src --output ./dist/styles.css --minify

```

---

## Performance Benchmarks

| Metric | Tailwind CSS | .antiui (DPI) |
| --- | --- | --- |
| **Initial Bundle** | 15 KB - 80 KB (CSS) | 2.1 KB (JS Engine) |
| **HTML Size** | Large (Class soup) | Minimal (Single string) |
| **Dev-Cycle** | Build re-run (1–2s) | Instant (0s) |
| **Type Safety** | String-based | TS Template Literals |

---

## License

MIT © @dotantiui

---

**Would you like me to generate the TypeScript definition file for these `ui` string literals to ensure you get autocomplete inside the quotes?**
