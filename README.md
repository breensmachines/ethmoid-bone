# Skull Base Playground · Ethmoid & Turbinates

An interactive 3D teaching model of adult sinonasal anatomy: an adult CT sinus scan (0.6 mm, bone kernel), segmented by Matt B. The ethmoid parts are hand-traced. The surrounding skull was segmented automatically from the same scan and is shown faint for context.

The tours are:
- Lateral nasal wall, with one explode slider per structure and a septum toggle
- Ground (basal) lamella
- Anterior vs posterior ethmoid
- The four lamellae
- Anterior ethmoid and the ostiomeatal unit (OMU)
- Midline and skull base
- Turbinates
- Posterior ethmoid
- Lamina papyracea

Each tour has linked axial, coronal and sagittal CT slices, plus CT volume and "patient" cross-section modes. It works on desktop and phones.

Fully static: plain HTML and WebGL2, no build step and no dependencies. The only external request is Google Fonts.

## Publish on GitHub Pages
1. Create a new repository (e.g. `ethmoid-playground`) and upload **all files in this folder** to its root, including the hidden `.nojekyll` file.
2. In the repository, go to **Settings → Pages**. Under **Build and deployment** choose **Deploy from a branch**, then select branch `main` and folder `/ (root)`.
3. After a minute the site will be live at `https://<your-username>.github.io/ethmoid-playground/`.

## Run locally
The page loads its data with `fetch`, so opening `index.html` straight from disk won't work. Serve the folder instead:
```
python3 -m http.server 8000
```
then open http://localhost:8000.

## Files
- `index.html`: the whole viewer (code, styles and tour text)
- `meshes_lo.txt`: low-detail surfaces for every structure, plus the context skull, loaded first
- `hi_<id>.txt`: high-detail surfaces, loaded per structure on demand
- `ct_XX.jpg`: CT slices packed into image atlases for the slice views and volume rendering
- `labels.b64.txt`: the label volume for the slice overlays

Mesh and label data are gzip-compressed and base64-encoded.

## Controls
- **Desktop:** drag to rotate, right-drag or shift-drag to pan, scroll to zoom, hover to name a structure, click to send the slice views to that point. Click a part in the list to isolate it; ⇧/⌘-click toggles it.
- **Phone:** drag to rotate, pinch to zoom, and tap a part in the list to toggle it. Tour chips sit under the 3D view, with the explode sliders right below.
- The septal soft tissue is hidden by default. Show it with **Show septal soft tissue** or **Colorize septum & inferior turbinates**. In the lateral wall and ground lamella tours, the gold button shows the septum at 75%.
- **Other bones** sets how transparent the context skull is.

Imaging data contain no patient identifiers. Segmentation © Matt B. Please credit when sharing.
