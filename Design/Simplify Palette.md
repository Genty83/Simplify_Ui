# SimplifyPalette

## Overview

SimplifyPalette is the central colour palette system within the SimplifyUI theme package.

It provides a consistent collection of colour ramps that form the foundation for the Desktop and Web theme token systems.

All colour ramps use OKLCH to provide perceptually consistent colour transitions and precise control over lightness, chroma and hue.

## Colour Ramp Structure

Each colour ramp contains exactly 16 shades, progressing from lightest to darkest.

| Shade | Order |
|---:|---|
| 10 | Lightest |
| 20 | |
| 30 | |
| 40 | |
| 50 | |
| 60 | |
| 70 | |
| 80 | |
| 90 | |
| 100 | |
| 110 | |
| 120 | |
| 130 | |
| 140 | |
| 150 | |
| 160 | Darkest |

## Colour Ramps

### Zinc

**Status:** In development

**Category:** Neutral

**Colour space:** OKLCH

Zinc will be the first neutral colour ramp developed for SimplifyPalette.

Tailwind Zinc will serve as a visual reference only. SimplifyUI will have its own independently designed ramp.

The ramp will be developed by carefully tuning:

- Lightness progression
- Chroma distribution
- Hue consistency and transitions

**Shade values:** Not yet defined.

## Design Principles

- All colour ramps use OKLCH.
- Every ramp contains exactly 16 shades.
- Shade numbering follows the 10–160 convention.
- Ramps progress consistently from lightest to darkest.
- Existing palettes may be used as visual references, but SimplifyPalette will have its own colour definitions.
- Colour ramps remain independent of Desktop and Web semantic token structures.

## Future Work

- Complete the Zinc ramp.
- Define additional neutral and chromatic ramps.
- Establish consistent colour generation principles.
- Define how palette colours are consumed by Desktop and Web theme tokens.