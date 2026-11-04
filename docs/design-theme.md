# Alumni invitation: reusable theme

Use the **Theme · Alumni invitation / Taste v2** and **Components · Controls, consent and states** boards in `design.pen`. The forest concept is retained as an archive, not the reference for new pages. These are proposed brand decisions pending SIES approval.

## Tokens

| Pen variable | Value | Role |
| --- | --- | --- |
| v2-bg | #F7F9FA | Main page and invitation surface |
| v2-surface | #ECF0F2 | Alternate sections and fields |
| v2-ink | #1F3038 | Running text, headings, dark footer |
| v2-muted | #5D6B72 | Secondary captions and help |
| v2-accent | #0D7480 | Primary actions and keyboard focus |
| v2-white | #FFFFFF | Text on primary action |
| v2-error | #A22D38 | Error text with an explanation |
| v2-success | #276044 | Verified/confirmed status with a label |
| v2-warning | #785719 | Pending/review status with a label |
| v2-display | Barlow Condensed, 700 | Short editorial headings |
| v2-body | Barlow, 400/500 | UI, body, labels, forms |

Normal-text contrast calculations: slate/frost **12.93:1**, muted/frost **5.22:1**, white/teal **5.49:1**, error/frost **6.70:1**, success/paper **6.44:1**, warning/paper **5.77:1**. These are token-pair calculations, not a complete WCAG audit.

## Typography and spacing

- Desktop public pages: display 112 px, section headings 72 px, lead 26 px, body/UI 18 px, captions 14 px. Wordmark sizes are identity exceptions.
- Tablet: display 100 px, headings 72 px; preserve readable body text rather than scaling the desktop uniformly.
- Mobile: display 72 px, section headings 52 px, body/UI 18 px, captions 14 px. Headlines remain at most two lines. Shorten copy before shrinking type.
- Display leading 0.98, tracking about -0.015 em. Body leading 1.5.
- 8 px spacing base. Desktop outer gutters 32 px; mobile 20 px. The invitation itself uses a 12 px mobile surround.
- Desktop sections use about 120 px vertical separation; mobile sections use 56 px. Related content uses 16–32 px gaps.
- Square corners and flat fills. No ornamental eyebrows, numbered feature rows, decorative rules, gradients or resting shadows.
- Use one principal action per section. Text links are underlined; do not add an arrow to every action.

## Components and behavior

The canvas contains reusable primary/secondary buttons, text-field specimens, consent and status components. Instances on the landing pages share their source component.

| Element | Design rule |
| --- | --- |
| Primary button | Teal, 52 px high; slate hover; visible 2 px focus outline with an offset in implementation |
| Secondary button | Paper fill and slate label; no competition with the primary action |
| Link | Visible underline; 44 px minimum interactive target, including padding |
| Text field | Persistent label, 52 px surface, helper below; focus and errors shown separately |
| Error | Explain the issue beside the field, preserve values, associate the message programmatically |
| Consent | Unchecked by default; directory visibility separate from verification and contact sharing |
| Status | Icon plus words, not colour alone; only use “Verified” after the verification workflow succeeds |
| Empty results | Explain that no match was found and suggest changing a filter |
| Loading | Text status; avoid showing fabricated profile skeleton data as actual people |
| Failure | Retry action and preserved search/filter state |
| Mobile menu | Full readable list; close target 44 px; keyboard focus management and Escape handling |

The inquiry selector has a verification state and a reunion variant on the interaction board. Implement as a labelled radio group. On selection, change the help text and carry the topic into the inquiry form. Do not submit by changing a topic.

## Future page patterns

| Page | Carry forward |
| --- | --- |
| Directory | Barlow UI, filters with visible labels, consent-aware result rows, explicit introduction requests |
| Memory Chest | Large condensed title, actual archival media, captions, provenance and institution/category filters |
| Events | Readable date/time/venue, agenda and registration state; show only published records |
| Communities | Interest-based index, membership state and guidelines; no unconsented member list |
| Careers | Role/employer/eligibility/closing date first; moderated listings and clear external application behavior |
| Institutions | Approved master-data profiles, historical status labels and campus visit requests |
| Give Back | Approved purposes and inquiry-first actions; payment UI only after finance/provider approval |
| Account/admin | Same tokens, Barlow headings at 24–32 px; compact working layouts, explicit errors and status |

The large invitation geometry belongs to public pages. Forms, directories and admin tools should prioritize task density and clarity.

## Responsive and media rules

Desktop navigation groups the public destinations into Alumni, Memory Chest, Participate and Institutions. In implementation, Participate exposes Community, Careers, Events/Reunions and Give Back; the mobile menu lists them directly. Sign in remains visible.

On narrow screens, recomposed sections stack photographs and copy in reading order. No hover-only information or horizontal scrolling is required. Keep the primary action in the initial screen. Body text stays readable at 200% zoom; that still requires browser testing after implementation.

Use actual SIES media with approval, captions and rights records. Found location photographs describe their actual subjects. Do not present Matunga street scenes as an institutional archive, or historical campus photographs as current facilities.

Proposed motion for implementation: a modest footer reveal and short, once-only content entrances. Reduced motion presents the same content statically. No autoplay sound. Video/audio must have a poster, captions/transcript and accessible controls. Motion is not implemented in the canvas.

## Source photographs used

All four files are local in `docs/assets`; metadata is in `docs/assets/credits.json`.

- [SIES Main Entrance](https://commons.wikimedia.org/wiki/File:SIES_Main_Entrance.jpg), credited to SIES, CC0. Hero invitation. Source image is 800 × 600; obtain higher-resolution approved imagery before production.
- [Matunga Station](https://commons.wikimedia.org/wiki/File:Matunga_Station.jpg), Rakesh Krishna Kumar, CC BY-SA 2.0. Memory Chest atmosphere, captioned as Matunga Road station.
- [Flowers at Matunga](https://commons.wikimedia.org/wiki/File:Flowers_at_Matunga.jpg), Rakesh Krishna Kumar, CC BY-SA 2.0. Location photograph beside the Memory Chest feature.
- [SIES GST 11](https://commons.wikimedia.org/wiki/File:SIES_GST_11.jpg), Wiki amn, CC BY-SA 3.0. Institution chapter, captioned as a 2011 quadrangle photograph.

The page footer includes a compact credit line. Production must link each photograph to its source and licence; preserve attribution and applicable share-alike terms for adaptations. The downloaded `sies-gst-nerul.jpg` portrait was reviewed and rejected for this design; it is not displayed. No bundled stock photographs, generated portraits, invented testimonials or named alumni appear in the revised design.

## Acceptance and limits

Check all three canvas widths (1440, 768, 390), the theme and component boards, and the menu/topic variants for clipping. Browser keyboard behavior, live submission, zoom, screen-reader output, responsive breakpoints and motion remain implementation checks. This canvas does not claim production readiness.
