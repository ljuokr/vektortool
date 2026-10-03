# Vektortool

**From vector to object.** Draw. Embroider. Laser-cut. 3D-print.
Free. No install, no account, works offline. A vector graphics editor that runs
entirely in your browser - a single HTML file, no server.

➡ **[vektortool.app](https://vektortool.app)**

![Vektortool](preview.png)

## Release status

The 3 October 2026 release uses the tested `VT-20261003-local-r22` build
(the local identifier is retained so the released application stays byte-identical
to the tested file; SHA-256 `c67e33f8cdfe99791d47f86fe17735e28a880a72d1babcb86a7b17419782f57a`).
The tracer retains its assigned pixel colours instead of reading them back from
the display canvas; automatic colour merging remains available. Tiny closed
running-stitch contours and valid small SVG source frames retain their geometry.
Micro-stitch warnings, texture definitions and rotated bounds in selection SVG
exports have also been corrected. See the changelog for scope and limitations.

A fresh Gecko trace with automatic colour merging and background removal reached
the embroidery preview in a real browser without excluding micro-objects.
Source-level regressions and separately saved machine files were independently
checked. These checks are not a complete browser-download round trip or a sew-out.
Direct paste into the tested macOS Inkscape 1.2.1 remains unsuccessful; selected
artwork can instead be saved with Ctrl/Cmd+Shift+C for SVG file import.

Remaining work includes complex-image calculation limits, full browser download
and reopen checks, final Safari/Firefox and cold-offline checks, LightBurn, and
physical machine/material trials. Very small details may require unsafe or
impractical stitches; there is no manufacturing approval. Existing projects are
not silently cleaned: retrace the original image or explicitly exclude unwanted
micro-objects from embroidery. Back up important work and inspect exports in the
intended target application.
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
