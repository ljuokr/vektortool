# Changelog

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
