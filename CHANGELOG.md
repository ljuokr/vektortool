# Changelog

## 14 October 2026 — r30

Release build `VT-20261014-local-r30`, byte-identical to the tested local file
(SHA-256 `dc861e0c54623fa6ca8b3c92185380ce15805cfbc3babb2af2b9793b2a70e0ff`).
Paint bucket coverage, smoothing for outline tracing and tracer layout fixes on
top of r29; no tracing or embroidery calculation changed.

- Paint bucket: cover the clicked area completely. The fill ended at the last fully coloured raster pixel, so a fringe of the old colour up to half a pixel wide stayed visible around every fill, and a white gap stayed between a fill and the line around it. Antialiased edge pixels now belong to the area, along thin parts such as spikes and notches up to three pixels deep (not inside bitmaps, whose soft edges would be painted over). In addition, the outline of the fill reaches an eighth of a pixel beyond the raster pixel edges, because the browser's own rasteriser is only that precise: Chrome, Edge and Firefox round horizontal path edges to quarter raster pixels and approximate curves, which hid slivers of the old colour from the bucket.
- Paint bucket: place the fill directly above the area it colours instead of on top of the drawing. Lines drawn above the area stay above the fill. Under a line the fill reaches to the middle of the line, because lines keep their width on screen and become thinner in the drawing when zooming in; under a filled shape it reaches one raster pixel. Seams between two areas that meet under the edge of a shape above are covered. A fill between two members of a group joins the group.
- Paint bucket: recolouring an earlier fill reproduces its outline instead of growing by its own overlap with every click.
- Outline (black-and-white) tracing: new checkbox "Smooth edges" below "Filled instead of outline", with the "Path smoothing" slider moved from "More options" directly below it. The checkbox switches smoothing on (1.5 px, or the strength chosen last) and off. The default stays off, with the pixel outline as before. Without smoothing the outline is byte-identical to r29.
- Tracer preview: keep the zoom and position set with pinch or Ctrl+wheel when a slider or checkbox changes the result. Each new preview image started at the base size and visibly zoomed back within a tenth of a second.
- Colour tracing: show "Group and hide colours" as a second column next to the controls once colours are detected (from a window width of 900 px; narrower windows keep one column). "More options" then open below it in the same column instead of as a third column. The empty box below the source image is hidden; it only appears when it holds the note about reduced processing resolution.
- Add the two new texts in all 31 non-German languages.

Verification on the final file in isolated Chrome, Firefox and WebKit profiles:
the paint bucket in 19 situations per engine with actual mouse clicks and saved
SVG downloads (56 checks per engine). Coverage was measured on the exact
geometry, independent of any rasterisation: at about 45 000 points per engine
along the edges of the covered shapes the old colour is exposed nowhere (apart
from one point in a slit narrower than a pixel), and the fill reaches on average
0.13 to 0.58 px, at thin parts at most 1.6 px, beyond the covered edge. 4 000 random
rasters exercised the flood and outline code without a browser. The smoothing
switch and slider passed 15 checks per engine including actual imports, the
tracer layout and preview zoom 9 checks per engine. The ten public
motifs produced the same 18 of 20 DST/PES pairs per engine, all byte-identical
to r28; the tracer interface, Gecko, satin-text, catalogue, camera, paint-server
and import checks were repeated without deviation.

Limits: the fill remains a raster result. Its outline is a staircase of half
pixels and lies up to about 0.6 px outside the covered edge, at thin parts up to
1.6 px; slits narrower than about one raster pixel are left open, so some of the
old colour can remain inside them. At corners
of thin outlines the fill can show one raster pixel (0.5 px) beyond the line at
very high zoom; its position relative to the middle of a line is accurate to
half a raster pixel. Under lines thinner than about 0.6 px the fill can show on
the other side. A click takes 80 to 170 ms on an A4 page instead of 45 to
130 ms, and up to about 0.3 s for the whole page background. The new
translations were not reviewed by native speakers. Otherwise unchanged from r29.

## 13 October 2026 — r29

Release build `VT-20261012-local-r29`, byte-identical to the tested local file
(SHA-256 `75ccbd71a877bd2fae4f4e9f3d253247d06a7a58d525660142c927c671f76ee5`).
Tracer interface adjustments on top of r28; no tracing or embroidery calculation changed.

- Show the colour count below the heading "Group and hide colours" on its own line instead of inside the wrapped heading.
- Replace the collapsible "presort colours" entry by a single checkbox, "Arrange colour circles by colour family", with a note saying that it only changes the display and helps when merging by hand. The function itself is unchanged.
- Show "Filled instead of outline" directly below the threshold in outline (black-and-white) tracing. It was only reachable under "More options"; a retained setting is now visible when the tracer is reopened. "With inner shapes" stays under "More options".
- Add the two new texts in all 31 non-German languages.

Verification on the final file in isolated Chrome, Firefox and WebKit profiles:
11 interface checks per engine including an actual filled import; the ten
public motifs produced the same 18 of 20 DST/PES pairs per engine, all
byte-identical to r28; the Gecko, satin-text, catalogue, camera and import
checks were repeated without deviation.

Limits: unchanged from r28. The new translations were not reviewed by native
speakers.

## 12 October 2026 — r28

Release build `VT-20261011-local-r28`, byte-identical to the tested local file
(SHA-256 `82b267ce32212d2ed1f14fef8a74926dd16d693379c10b2bbaa0c1522f5b8829`).
Repairs from an independent re-verification of r27.

- Import SVG files that use gradient or pattern paint again. r27 rejected the whole file as invalid; as before r27, an object painted only by a gradient or pattern is skipped and counted, and everything else is imported.
- Name the actual cause in import notices: separate notices for skipped gradient, pattern and image objects, for `use` references, and for objects imported without their gradient or pattern paint. Unpainted objects such as an artboard frame no longer raise a loss notice. The notices also appear when nothing could be imported.
- Do not stitch characters of imported SVG path text that Gecko does not draw. Characters beyond the end of the path were piled up at the path end and characters before its start were continued in a straight line; text that lies completely off its path is now rejected in Gecko as in Chromium. Chromium output is unchanged. Stitch cache version 253.
- Keep the fixed limit of five million calculation steps per object, but allow 30 s instead of 5 s of active computing time in the pausing background calculation. The 5-s limit made the same design export or lock depending on device speed and load. The synchronous calculation keeps its 5-s limit.
- Let the fill underlay pause between its passes like the main fill and remove a quadratic scan from the short-stitch merge. Stitch output is unchanged.
- Stop a camera stream that arrives after Cancel or after switching cameras, and remove the Escape handler when the camera view closes.
- Complete 59 messages in all 31 non-German languages: SVG import diagnostics and notices, the empty laser export, the custom format label and the caption in the tracer help illustration. The fill style and satin underlay option "Kontur" is no longer shown as "Stroke".

Integrated verification on the final file in isolated Chrome, Firefox and WebKit
profiles with actual saved downloads: the ten public motifs in colour and
black-and-white mode produced 18 of 20 DST/PES pairs in each engine (r27:
17 or 16, 14 and 16). All pairs that r27 produced are byte-identical (17 in
two Chrome runs, 14 in Firefox, 16 in WebKit); the newly exported sunflower
equals the output of r27 with only the time limit changed. The files of the
material, satin-text, Gecko and font tests are byte-identical to r27 in every
engine; the only changed files are the corrected Gecko path-text overflow
cases. Further checks: eight gradient/pattern imports and 18 notice cases per
engine, 13 path-text visibility cases per engine compared against the
browser's own rendering, 14 camera checks with a simulated device, and the new
messages in 32 languages through the application's own translation function.

Limits: gradient and pattern paint itself is still not imported, and `use`
references are reported, not resolved. WebKit still locks imported path text
that overflows its path. The main fill pass of one object remains a single
block (longest observed main-thread task 2.4 s in the landscape motif,
unchanged; butterfly 3.4 s to 1.2 s, sunflower 3.9 s to 2.1 s). The
synchronous 5-s limit, the 2.5-s outline check and all fixed safety limits are
unchanged; the fern motif still exceeds the 100,000 contour-point limit. Runs
of very short jump records in satin-text DST files were observed and left
unchanged because their effect on a machine is untested. The new translations
were not reviewed by native speakers. No complete SVG/browser/device
certification and no physical machine/material approval is implied.

## 5 October 2026 — r27

Release build `VT-20261005-local-r27`, byte-identical to the tested local file
(SHA-256 `28c15f5bd5ee6c87777d5437355439bdd6e18ba49adb6983a051611095cae73c`).

- Canonicalise supported static CSS paints before project persistence, including escaped colours, modern RGB/HSL and inherited SVG currentColor. Migrate known paint fields in detached legacy project/undo data while retaining strict validation and original recovery downloads.
- Exclude alpha-zero and zero-width unpainted geometry from embroidery and DXF, including gear/wheel exceptions and conversion paths. Preserve visible controls and correctly convert named/RGB/HSL red to the PES thread palette.
- Preserve supported SVG path-text geometry, anchors, baseline offsets and positioned text spans. Wait for registered fonts before measuring; cancellation cannot commit stale text. Correct exact-path rotation and reject fully overflowed text instead of generating phantom stitches.
- Preserve imported SVG line caps, joins and miter limits. Scale non-scaling strokes correctly for PNG/PDF raster export; project/graphic SVG semantics remain unchanged.
- Run Satin/lengthwise text skeletonisation and routing in a local Worker with revision, cancellation and export guards. Missing fonts and Worker failures do not silently substitute text or release incomplete files. Keep the existing large-raster limit, checked before expensive calculation. Stitch cache version 252.
- Protect strong light/dark contrast during automatic colour merging, including the tested WebKit Gecko. Automatic merging, exact target group count and original source pixels are retained.

Integrated verification: three browser engines; actual project-SVG, DXF, DST,
PES, PNG and PDF downloads; project reimports and historical IDB recovery.
The dedicated stitch suite saved 30 files, independently decoded all 15 DST/PES
pairs and retained byte parity in 30 comparisons. SVG tests covered 14 import/
roundtrip cases plus four rotation/overflow cases. Gecko passed in all three
engines, with six independently decoded embroidery files. A fresh network-offline
Chrome launch of the final local file also passed through actual export.

Limits: unsupported SVG typography and partial alpha are explicitly rejected;
new SVG diagnostics are not yet fully translated. Worker execution reduces the
long UI block, not total compute cost (10 large M glyphs: 16.194 s total,
167 ms maximum observed main-thread LongTask in the integrated test). Very large
text still reaches the existing raster limit. Stronger contrast protection can
increase complexity in photographs: the tested fern produced 69.3% more paths;
nine other public motif groupings remained unchanged. PDF remains JPEG-based.
No complete SVG/browser/device certification, LightBurn validation or physical
machine/material approval is implied. Already lost source detail or incorrect
historical imports may require reimporting/retracing the original.

## 4 October 2026 — r26

Release build `VT-20261004-local-r26`, byte-identical to the tested local file
(SHA-256 `fedad10331bf614c0cd02cae95700543de1725d43d08e8d63fd3f9c4027f879b`).
Includes the preceding local r23-r25 interface and contour-preview changes.

- Keep test-card embroidery and parameter locks scoped to the active canvas. Do not change other canvases' persistent stitch visibility; do not blindly unhide previously saved objects.
- Reject an active export object if all its sewn movement disappears after actual 0.1-mm machine-grid quantisation. Report the object ID and an explanation; applies to DST/PES/PEC/EXP.
- Improve lengthwise lettering against the shaped whole-word contour while preserving existing main rows. Connect compact repair runs only through checked material, preserve holes, and decline reordering that increases remaining jump distance. Add bounded reference-word caching and computation limits. Stitch cache version 251.
- Add an optional blue finishing-contour display guide for internal previews. It does not add stitches and is hidden for stale/error previews, external files and partial playback.
- Restore consistent round, contrasting help buttons and organise area settings.
- Refresh canvas dimensions without stitch data and suppress frame warnings based on a previous drawing's stale bounding box.
- Complete 31 targeted UI/message keys in all 31 non-German languages, including dynamic text controls, export warnings and help. Fix the desktop RTL preview/header column placement.
- Update version notes and stop presenting unresolved historical symbolic identifiers as GitHub commit links.

Verified: real-browser Gecko/test-card/return/reload, imported micro-object error
handling, Pacifico in three sizes, DE/EN/AR views and a mobile layout. Targeted
source tests include 28 test-card checks, 56 export-guard cases, 40 text cases,
eight text safety checks and translation/syntax regressions. Twenty regular
exports remain byte-identical; 160 additional saved text files were independently
decoded with matching ordered stitch geometry across all four formats. Twenty
Satin text cases retain their previous point arrays. These counts are bounded
tests, not complete end-to-end coverage.

Remaining limitations: fine lettering still has short detail stitches and jumps;
large lengthwise words can take longer. Whole-word coverage improved in 17/20
measured lengthwise cases, not every possible font or design. Tiny subpaths inside
otherwise valid compound objects can still collapse. Machine-grid rounding can
slightly exceed a nominal stitch-length setting (observed Satin maximum 7.052 mm
for a nominal 7 mm). Actual browser-download round trips, cold-offline and final
cross-browser/target-application checks, and physical sew-outs remain incomplete.
No general error-free or manufacturing approval is implied.

## 3 October 2026 — r22

Release build `VT-20261003-local-r22`, byte-identical to the tested local file.
Includes the preceding local r20/r21 tracer and palette-interface work.

- Keep the final assigned tracer pixels in an owned buffer instead of re-reading the display canvas. Controlled one-unit RGB readback differences no longer create extra islands; automatic colour merging and intentional one-pixel features remain supported.
- Preserve the geometry of tiny closed running-stitch contours with size-dependent simplification. Ordinary contours and open paths keep their previous rules. This can create more micro-stitches, not necessarily better sew-outs.
- Do not exempt an entire micro-stitch-only run from the quality warning as if it consisted solely of tie stitches.
- Use the existing 0.001-pixel source-frame minimum consistently in SVG rendering, node editing, separation and stitch mapping. Valid source frames below 0.5 pixels no longer shrink again or shift incorrectly.
- Include texture pattern definitions and rotated bounds in copied/selection SVG. Keep existing clipboard MIME fallbacks; replace universal compatibility claims with a short translated file-export shortcut hint.
- Stitch cache version 249.

Verified on the integrated build: 1,522 stitch/geometry regressions, 11 tracer
readback/worker checks, 41 automatic-merge checks, 55 crop/scale/alpha checks,
28 selection-SVG checks and 32 clipboard API checks. The broader tracer quality
suite remains 318/322, with the same four existing quantisation deviations.
Additional project/export checks and 19 independently decoded saved DST files
passed. Machine files from isolated encoder checks are not browser downloads.

The real-browser fresh Gecko workflow (automatic merge, background removal,
apply, embroidery preview) completed without hiding micro-objects. DST export
was triggered, but its saved browser file was not independently confirmed.
Direct paste into the tested macOS Inkscape 1.2.1 remains unresolved. Complex
motifs still meet calculation limits; complete browser round trips, cold-offline,
final cross-browser, target-program and machine/material checks remain open.
Other geometries collapsing below the machine format's 0.1-mm grid still need
a general post-quantisation export guard. Existing projects are not silently
rewritten. No general error-free or manufacturing approval is implied.

## 2 October 2026 — r16

- Keep the routine storage notice closed even when archived conflict backups exist. Backup details remain available through the status bar.
- Remove the loaded-backup timestamp from the notice; the recovery list retains its entry dates.
- Preserve warnings for real save/restore failures, active conflicts, degraded storage, reset operations and a resumed tab whose own prior state differs from the displayed main document.
- Storage writes, recovery data and loading logic are unchanged. Verified with 19 regression assertions and a real two-tab conflict, reload, and recovery-list workflow.

## 2 October 2026 — r15

Release build `VT-20261002-local-r15`, byte-identical to the tested local file.

- Replace the misleading missing-DST placeholder for editor drawings with actual preparation, empty, inactive-object and calculation-error states. A direct **Recalculate** button is available in the empty preview.
- Preserve the last valid preview on calculation failure and explicitly mark it as not updated. Reset playback controls when the current drawing has no active embroidery; restore them after a successful calculation.
- Use one eligibility check for preview and export. Hidden, disabled or ignored whole objects are excluded; a separately active differently coloured outline remains available when only the fill is hidden.
- Add contextual hints in all 32 supported languages. Numerical stitch algorithms, stitch cache 245 and strict export error guards remain unchanged.

Verified with real browser failure/retry/recovery, hidden-fill/active-outline,
manual recalculation and language-switch flows; 382 source-function, pipeline,
translation and syntax assertions passed. Additional eligibility and production
DST/PES/PEC/EXP encoder tests passed. The exact cause in the unavailable reported
user drawing remains undetermined; no new machine/material approval.

## 2 October 2026 — r14

Release build `VT-20261002-local-r14`, byte-identical to the tested local file.
Includes the previously unpublished r13 fixes.

- Split compound SVG colour shapes into separate components while retaining holes; one combined selection frame for multi-selection.
- Dedicated **SVG for laser (text as outlines)** export: raster-derived text/path-text contours with an expanded export page where needed. Editable project SVG retains its text. DXF text export remains unsupported.
- Tracer colour/black-and-white demo switching, visible background selection and interface translations improved.
- Background removal now follows the existing colour-distance threshold without stranding darker JPEG background pixels at a second brightness cutoff. Automatic colour merging and contour tracing are unchanged. Similar light foreground edges can still be removed.
- Short embroidery rows can no longer mutually eliminate each other; negative pull compensation cannot collapse a usable short row. Stitch cache updated to 245. Empty active objects still block export.
- Reproduced the Gecko-without-background workflow: after component splitting, 8 objects instead of 127 and no empty-stitch errors in the tested configuration. Existing vector documents are not silently cleaned; retrace the source image.

Actual Gecko DST/PES downloads were independently decoded: identical ordered
nonzero sewn segments and colour blocks after origin alignment. Format-specific
trim commands are not a guarantee of identical machine behaviour. Actual project
SVG metadata and laser SVG output were also inspected. Cross-browser, cold-offline,
LightBurn and physical material validation remain incomplete; no manufacturing approval.

## 2 October 2026

Release build `VT-20261002-local-r12`. Application bytes are unchanged from the tested local candidate.

- Distinct freehand, line and curve preview cards with interaction hints in all 32 languages; Bezier handles retained in previews.
- Consistent micro-stitch quality warnings across legal zero-length stitch records; exported stitch geometry unchanged by this warning fix.
- Visible-colour paint bucket with tolerance, independent vector output, undo and cancellation safeguards.
- Editable SVG projects replace the `.linea` save option; legacy project import remains available.
- Triangle/Brackets living-hinge cutouts, quieter snap confirmation and independent colour/black-and-white tracer previews.
- Includes the preceding local tracing, text, embroidery, project-storage and translation repairs.

Known validation gaps: real browser downloads and reimports, final cross-browser and cold-offline checks. Fine embroidery details and laser/material behaviour require physical samples; this is not a manufacturing approval.

## 2026-06-17
- Text on a path: distance slider (outside / on the line / inside), arc side, letter spacing and text colour; glyphs now sit straight on rectangles, polygons and stars
- Image tracer: camera capture and a test-image button
- English README and repository metadata

## 2026-06-16
- Image tracer: full coverage, no dropped shapes; enclosed same-colour areas are kept and raw trace colours are preserved
- Same-colour fragments are combined into one shape per colour

## 2026-06-15
- Embroidery fill: cleaner dense rows without diagonal or staircase artefacts
- Tie stitches are recognised correctly by external analyzers

## 2026-06-14
- Embroidery settings: value input boxes, translated density warnings

## 2026-06-13
- File import: SVG and DXF as real vectors, embroidery files (DST/PES/EXP/PEC)
- Contour fill as a real spiral
- In-app changelog, manual value entry in the embroidery settings

## 2026-06-12
- Reworked embroidery panel: help cards, stitch types and stitch order
- Pattern generator fixes (3D / origami)
- Additional export formats (EXP/PEC), tracer mode-switch fixes
- Many interface strings translated across 31 languages

## 2026-06-11
- First public release: browser-based vector editor (draw, trace images, embroider, 3D/laser templates, box generator)
- All editor fonts embedded, 31-language interface, text-on-path embroidery
