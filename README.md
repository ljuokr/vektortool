# Vektortool

**From vector to object.** Draw. Embroider. Laser-cut. 3D-print.
Free. No install, no account, works offline. A vector graphics editor that runs
entirely in your browser - a single HTML file, no server.

➡ **[vektortool.app](https://vektortool.app)**

![Vektortool](preview.png)

## Release status

The 2 October 2026 release uses the tested `VT-20261002-local-r16` build
(the local build identifier is retained to keep the tested application bytes unchanged).
Archived conflict backups no longer keep the storage notice open automatically;
backups remain accessible from the status bar. The loaded-backup timestamp is
removed from the notice. Actual save failures and active conflicts still warn.
The embroidery preview now shows actual calculation errors instead of a misleading
missing-DST-file message, offers a direct retry, and clearly labels a retained older
preview. Preview and export consistently respect hidden, disabled and ignored objects;
a separately active outline remains available when only its fill is hidden.
No numerical stitch algorithms or strict export error guards changed in r15.
It includes SVG component splitting, a combined selection frame, laser SVG text
outlines, and fixes for background remnants and empty embroidery fill results.
Actual project-SVG, laser-SVG, DST and PES downloads have been independently
inspected. The Gecko tracing-to-embroidery flow was checked in Chromium-based
browsers. Remaining validation includes full project reopen round trips, final
Safari/Firefox and cold-offline checks, LightBurn, and physical machine/material
trials. Back up important work and verify exports in the intended target application.
Existing traces keep their stored background fragments: retrace the original
image to use the improved background removal. Very light foreground edges may
also be removed; small embroidery details still require care.
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
