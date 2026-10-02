# Changelog

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
