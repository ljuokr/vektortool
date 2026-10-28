# Vektortool

**From vector to object.** Draw. Embroider. Laser-cut. 3D-print.
Free. No install, no account, works offline. A vector graphics editor that runs
entirely in your browser - a single HTML file, no server.

➡ **[vektortool.app](https://vektortool.app)**

![Vektortool](preview.png)

## Release status

The 28 October 2026 release uses the tested `VT-20261028-local-r41` build
(the local identifier is retained so the released application stays byte-identical
to the tested file; SHA-256 `e109b7f1d9c09c2e7cd6e7917f01a5028cbc0fe84b2626d6df284cb88573a753`).
r41 adds a laser and cutting-plotter export (xTool Studio, LightBurn, Silhouette
Studio; red hairline = cut, black = engrave) and two-colour outline tracing for it,
a link to the Design und Technik website in the status bar, the classic four-row
tatami stagger, and fill routing that hides travel under rows sewn later. Tatami and
outlined lettering choose per letter between routing variants. Over six outlined
fonts, visible travel across finished rows falls from 218 mm (r37) to 34 mm, close to
Ink/Stitch 2.2.0 (35 mm).
r37 improves embroidery routing and lettering: the final material check reroutes
stitches through the interior instead of cutting them into jumps, the underlay and
travel around holes take shorter interior routes, tatami and satin text are sewn
letter by letter, satin text gets a centre-walk underlay, and crossings in script
letters (such as the looped "t" of Pacifico) become clean columns, and satin stitches
follow the cross-section of the stroke, so thick bowls no longer fan. Over five test
texts satin trims fall from 51 to 32 compared with the state before these changes, and in a comparison of 16 shapes with Ink/Stitch
no Vektortool shape has stitches outside. r31 reworked fill-stitch routing: rows at sharp corners reach the edge again,
travel runs just inside the outline instead of on it, stitches that graze an
inward-curved edge are bent inward instead of being cut into chains of short
jumps, and the underlay leads into the fill without a trim. For a traced gecko
this reduces jumps in the needle points from 260 to 49 and trims from 3 to 1.
The pattern generator starts with "Fill canvas" and keeps a free gap between
scale arcs. r30 made the paint bucket cover the clicked area completely (no fringe of the
old colour, fill placed below the lines and reaching to their middle), adds
a "Smooth edges" switch with its slider to outline tracing, keeps the tracer
preview zoom while adjusting, and shows colour groups in a second column. r29
adjusted the tracer interface
(colour count on its own line, clearer colour family option, fill option visible
in outline tracing). Both build on r28, which
repaired findings of an independent re-verification of r27: SVG
files with gradient or pattern paint are imported again, import notices name
the actual cause, Gecko no longer stitches path-text characters the browser
does not draw, heavy fills are no longer locked by a 5-second time limit in the
background calculation, late camera streams are stopped, and 59 messages are
translated in all languages. See the changelog for scope and limitations.

The releases were tested in isolated Chrome, Firefox and WebKit profiles with
actual saved browser downloads and independent machine-file decoding. Every
embroidery file that r27 produced in these tests is byte-identical, apart from
the corrected Gecko path-text overflow cases; r29 and r30 output is byte-identical
to r28. r31, r37 and r41 change routing on purpose; their files were compared with the
previous release by coverage, stitches outside the shape, jumps, trims and short
stitches, and r37 and r41 also with Ink/Stitch 2.2.0. r37 and r41 were tested in Chrome and WebKit only. These are targeted repair checks,
not exhaustive browser or machine certification.
Direct paste into the tested macOS Inkscape 1.2.1 remains unsuccessful; selected
artwork can instead be saved with Ctrl/Cmd+Shift+C for SVG file import.

Remaining work includes complex-image and large-text calculation limits, SVG
typography, gradients and `use` references outside the supported subset, broader
device/target-application checks including LightBurn, and physical machine/material
trials. Worker execution improves responsiveness, not total calculation time.
Fine lettering can still contain many short stitches and jumps. Very
small subpaths inside otherwise valid compound objects can still disappear on
the machine grid. There is no manufacturing approval. Existing projects are not
silently cleaned, and previously saved hidden objects are not automatically
unhidden. Back up important work and inspect exports in the intended target
application.
Pushing `main` automatically deploys `vektortool.html` to GitHub Pages.

## What it does

- **Draw** - shapes, paths, freehand, text (also on a path), mirror/repeat, layers
- **Fill** - flood a connected visible colour into a separate vector shape,
  with adjustable tolerance; originals stay unchanged
- **Trace images** - turn a pixel image into vector paths (tracer) plus outline mode
- **Embroider** - stitch types, stitch order, export as an embroidery file (DST/PES)
- **3D printing & laser** - pattern generator (origami and more) and SVG templates
  to extrude in a slicer or cut on a laser cutter
- **Box generator** - finger-joint boxes for laser cutting

Save editable work as **SVG (project)**. It embeds all canvases, hidden objects,
fonts and settings. For sharing visible artwork without this extra project data,
choose **SVG graphic** instead. Existing `.linea` projects can still be imported.

## For school and workshop

Made for school, FabLab and hobby use: **no sign-up, no cloud**, works offline.
All data stays on your device. The interface is available in German and more
than 30 other languages.

## Use it locally

The app is a single file. Open the info panel (ℹ), download the file and open
`vektortool.html` in your browser. It works fully offline, and no data leaves
your device.

## License

[PolyForm Noncommercial 1.0.0](https://polyformproject.org/licenses/noncommercial/1.0.0/)
- free for non-commercial use. © Lukas Jordi.
