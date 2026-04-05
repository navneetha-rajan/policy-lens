# Design System Specification: Clinical Precision & Tonal Depth

## 1. Overview & Creative North Star
**The Creative North Star: "The Clinical Curator"**
This design system moves away from the sterile, "template-heavy" feel of traditional healthcare software. Instead, it adopts the persona of a high-end editorial journal—authoritative, airy, and hyper-legible. We achieve "Clinical Integrity" not through rigid grids and heavy borders, but through **intentional asymmetry, breathability, and tonal layering.** 

By utilizing a "Warm Off-White" foundation against "Pure White" surfaces, we create a soft-contrast environment that reduces cognitive load for clinicians while maintaining a premium, bespoke feel. The system rejects "standard" UI tropes in favor of a sophisticated, layered experience where data is the hero.

---

## 2. Colors & Surface Logic
The palette is rooted in a clinical teal and a sophisticated warm neutral base. The goal is to use color as a functional tool, never as decoration.

### The "No-Line" Rule
To achieve a high-end feel, **prohibit 1px solid borders for sectioning.** Boundaries must be defined solely through background color shifts. For example, a `surface-container-low` section sitting on a `surface` background provides all the separation a user needs without the visual noise of a line.

### Surface Hierarchy & Nesting
Treat the UI as a series of physical layers. Use the `surface-container` tiers to create "nested" depth:
- **Background (`surface`):** `#F7F8FA` — The warm, foundational canvas.
- **Section Base (`surface-container-low`):** `#F2F4F6` — Used for secondary grouping.
- **Active Cards (`surface-container-lowest`):** `#FFFFFF` — Use this for primary interactive cards to create a "pop" against the off-white background.

### Signature Accents
- **Primary Teal (`#0EA5A0`):** Reserved strictly for "The Moment of Action" (Primary Buttons, Active Toggles) and "The Moment of Truth" (Key Data Highlights).
- **Functional Tones:** Use `error` (`#BA1A1A`) and `tertiary` (Warm Orange/Brown) sparingly for critical alerts and secondary data trends.

---

## 3. Typography: The Editorial Edge
We pair modern sans-serifs with a precise monospace to create a "Technical-Humanist" contrast.

- **UI Text (Inter/Geist Sans):** Used for navigation, labels, and body copy. It is clean, approachable, and highly readable at small scales.
- **Data Strings (IBM Plex Mono):** Used for Drug Codes, Policy IDs, and Tier Labels. The monospace font adds a layer of "Technical Authority," signaling to the user that this specific string is a piece of precise, clinical data.

**Hierarchy Strategy:**
- **Display/Headline (Manrope):** Use large, low-tracking headlines for dashboard titles to establish an editorial feel.
- **Metric Values:** Large numeric values (32–40px, Weight 600) should be the visual anchor of any page, paired with a `label-md` (13px) muted gray unit label for context.

---

## 4. Elevation & Depth
We convey hierarchy through **Tonal Layering** rather than traditional structural lines.

### The Layering Principle
Depth is achieved by "stacking" surface-container tiers. Place a `surface-container-lowest` (#FFFFFF) card on a `surface-container-low` (#F2F4F6) section to create a soft, natural lift.

### Ambient Shadows & Glassmorphism
- **Whisper Shadows:** When a card must float, use a "Whisper Shadow": `0 1px 4px rgba(0,0,0,0.06)`. The shadow should feel like a suggestion of light, not a heavy drop-shadow.
- **The Ghost Border:** If a border is required for accessibility, use the `outline-variant` token at **10%–20% opacity**. Never use 100% opaque, high-contrast borders.
- **Glass Effects:** For floating overlays (like tooltips or dropdowns), use a semi-transparent `surface` color with a `backdrop-blur` (12px–20px). This makes the UI feel integrated and premium.

---

## 5. Components

### Cards & Metrics
- **The Metric Block:** A high-contrast pairing of a 32px Weight 600 value and a 13px muted label. 
- **Trend Indicators:** Use a "Pill" style for trends. Teal text on a subtle teal background for positive; Muted Red for negative. No borders.
- **Card Containers:** 8px rounded corners (`DEFAULT`). Forbid divider lines within cards; use 24px–32px of vertical white space to separate content blocks.

### Buttons & Inputs
- **Primary Button:** Solid Teal (#0EA5A0) with White text. 8px radius. Use a subtle scale-down (0.98) on click for tactile feedback.
- **Secondary Action:** Transparent background with a "Ghost Border" (10% opacity outline).
- **Input Fields:** Pure white background (#FFFFFF) with a subtle 1px border (#E4E7EC). On focus, the border transitions to Teal, and the shadow deepens slightly.

### Lists & Tables
- **The "No-Divider" List:** Rows should be separated by a subtle background toggle (Zebra striping using `surface` and `surface-container-low`) or simply by generous white space. 
- **Monospace Data:** Policy IDs and Drug Codes in tables must use `IBM Plex Mono` to distinguish them from descriptive text.

---

## 6. Do's and Don'ts

### Do
- **Do** use white space as a structural element. If a layout feels cluttered, increase the padding rather than adding a border.
- **Do** use the 150ms ease-out animation for all hover and transition states to ensure the UI feels responsive but "calm."
- **Do** lean into the 8px corner radius for a "confident yet approachable" look.

### Don't
- **Don't** use gradients. The visual "soul" comes from the interplay of flat, high-quality tonal shifts.
- **Don't** use purely decorative icons. If an icon doesn't aid in navigation or data interpretation, remove it.
- **Don't** use high-contrast dividers. Lines should be the last resort for separating information.