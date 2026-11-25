# Skull Base Playground · Ethmoid

An interactive 3D teaching model of the adult ethmoid labyrinth and sinonasal anatomy. It's built from an adult CT sinus scan (0.6 mm, bone kernel) segmented by Matt B.

- **Hand-traced (Matt B):** the ethmoid bony parts and the anterior/posterior air-cell regions. These were smoothed and hole-filled, with each structure kept separate.
- **Derived from the CT:**
  - the individual air cells, split within each traced group;
  - the maxillary, frontal and sphenoid sinuses;
  - the vomer;
  - the nasolacrimal ducts.
- **Context:** the surrounding skull was segmented automatically and is shown faint.

## Tours
- **Cells: Anterior vs Posterior:** a two-stage explode on one slider. The anterior and posterior groups first move off the ground lamella, then the cells within each group separate.
- **Paranasal Sinuses:** maxillary, frontal and sphenoid sinuses around the ethmoid cells, including the variant recess of the left posterior ethmoid.
- **Lateral Nasal Wall:** per-structure explode sliders, with optional sinus and nasolacrimal duct overlays.
- **Infundibulum & Frontal Outflow:** the infundibulum, semilunar hiatus and frontal outflow as fixed 3D sheets, with surrounding structures exploding away from them. Sagittal and coronal slices are annotated.
- **Ground Lamella:** on desktop, a split 3D view (lateral view plus an isolated turntable). Below it are fixed axial, coronal and sagittal slices; click an axial or coronal slice to show its plane on the sagittal "7".
- **The Four Lamellae**
- **Anterior Ethmoid / OMU**
- **Midline & Skull Base**
- **Turbinates**
- **Posterior Ethmoid**
- **Lamina Papyracea**

## Display toggles
- Paranasal sinuses (shown as a highlighted box)
- Nasolacrimal ducts
- Dotted contact lines: agger nasi ↔ uncinate, and middle turbinate ↔ ground lamella
- The ground lamella's attachment margin

Every tour has linked axial, coronal and sagittal CT slices, plus CT volume and "patient" cross-section modes. The site works on desktop and phones; the split studio layouts are desktop-only.

The site is fully static: plain HTML and WebGL2, with no build step and no dependencies. The only external request is Google Fonts.

## Publish on GitHub Pages
1. Create a repository (this one is `ethmoid-bone`) and upload **all files in this folder** to its root, including the hidden `.nojekyll` file.
2. In the repository, go to **Settings → Pages**. Under **Build and deployment** choose **Deploy from a branch**, then select branch `main` and folder `/ (root)`.
3. After a minute the site will be live at `https://<your-username>.github.io/ethmoid-bone/`.

The upload is about 60 MB across roughly 70 files, which GitHub's web uploader accepts (each file is under 25 MB). With git:
```
git init && git add . && git commit -m "Ethmoid playground" && git branch -M main
git remote add origin https://github.com/<you>/ethmoid-bone.git && git push -u origin main
```

## Run locally
The page loads its data with `fetch`, so opening `index.html` straight from disk won't work. Serve the folder instead:
```
python3 -m http.server 8000
```
then open http://localhost:8000.

## Files
- `index.html`: the whole viewer, including code, styles and tour text.
- `meshes_lo.txt`: low-detail surfaces for every structure plus the context skull. This file loads first.
- `hi_<id>.txt`: high-detail surfaces, loaded per structure on demand.
- `ct_XX.jpg`: CT slices packed into image atlases.
- `labels.b64.txt`: the label volume for the slice overlays.

Mesh and label data are gzip-compressed and base64-encoded.

## Controls
- **Desktop:**
  - Drag to rotate.
  - Right-drag or shift-drag to pan.
  - Scroll to zoom.
  - Hover to name a structure.
  - Click to send the slice views to that point.
  - In the parts list (grouped by category → structure → side), click to isolate; ⇧/⌘-click to toggle.
  - Scroll the studio slices with the mouse wheel.
- **Phone:**
  - Drag to rotate and pinch to zoom.
  - Tap a part to toggle it.
  - Tour chips sit under the 3D view.

Imaging data contain no patient identifiers. Segmentation © Matt B. Please credit when sharing.
