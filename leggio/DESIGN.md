# Leggio. Design rules

Read this before drawing anything. Calm, dark interface around a page that reads like a book.

## Type

- **Reading and titles:** a serif. Newsreader (Google Fonts, open license), Georgia as fallback. Titles in a light or regular weight, never bold.
- **Interface:** a sans. Inter (open license), the system font as fallback. Small, 11 to 13 px, regular weight.
- Never a third family, never monospace in the interface. Keep the files of the fonts in `lib/` so Leggio works offline.

## Colors

The interface is dark and quiet, the page is the only bright thing.

| Role | Color |
| --- | --- |
| Background | `#16181F` |
| Bars (top bar, reader bar, window bars) | `#16181F` at 94% opacity, all the same |
| Panels and menus | `#21242D` |
| Text | `#EAEBF1` |
| Secondary text | `#A4ABBA` |
| Lines | `#888FA4` at 8% opacity |
| Accent (progress, read pages, selected ring) | `#9FD2FF` |

No borders around boxes, no boxes behind labels, no text shadows.

## Highlighters

Six colors. On light pages they blend with **multiply**, on dark pages with **screen**, and the highlighted text stays white.

| Name | Color |
| --- | --- |
| Yellow | `#FFD60A` |
| Orange | `#FFA15E` |
| Green | `#30D158` |
| Pink | `#FF375F` |
| Blue | `#0A84FF` |
| Light blue | `#9FD2FF` |

The toolbar circles are 17 px, with room between them. The chosen one gets a 1.5 px ring in its own color, 2.5 px away.

## Page tones

| Tone | Page | Text |
| --- | --- | --- |
| Light | `#F7F3EA` | `#1C2230` |
| Sepia | `#EFE7D7` | `#3F3627` |
| Slate | `#1E2029` | `#C1C7D6` |
| Almost black | `#0A0B0D` | `#C9CDD6` |

For PDFs on dark tones, invert the rendered page: `invert(1) hue-rotate(180deg) brightness(.8)`.

## Motion

Slow and small: 200 to 400 ms, ease-out. Numbers count up instead of jumping. Nothing bounces.
