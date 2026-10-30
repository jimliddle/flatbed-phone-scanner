# Flatbed

A document scanner that runs entirely in the browser. Point your phone at a letter, a receipt or a newspaper page and Flatbed finds the edges, squares up the perspective, cleans up the lighting and saves the page. Everything stays on your device: there is no server, no account and no upload.

The whole app is one HTML file (`index.html`, about 180 KB) with no external libraries. The other files in this repository let it install to a home screen and work offline.

## Features

- **Live edge detection.** The camera view outlines the page as you aim, and with auto capture on it takes the shot once the page has been held steady for a second.
- **Perspective correction.** Corners are refined on the full-resolution photo, and the real shape of the sheet is estimated from the perspective, snapping to A4, US Letter or Legal when it is close.
- **Article selection.** For a story within a newspaper page, Article mode finds the headline, column and photo blocks and lets you tap the ones that belong together.
- **Looks:** Auto, Colour, Greyscale, B&W, Crop only, or the original photo. Auto removes shadows and paper tint, then picks colour when there is colour on the page, greyscale when there are photos and B&W for plain text.
- **Compact storage.** B&W pages are saved as 1-bit PNG (typically 20–40 KB a page) and the rest as JPEG at a quality you choose.
- **Export and share:** PDF, individual images or a ZIP, sent through the phone's share sheet or saved as a download.
- **Password-protected PDFs** using AES-256, readable in any standard PDF viewer.
- **Encrypted backup** of the whole library (AES-256-GCM, PBKDF2 with 600,000 rounds) that can be restored on another device.
- **Editing later:** re-crop, change the look, rotate, reorder by press-and-drag, merge documents.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The complete app |
| `sw.js` | Service worker that keeps the app available offline |
| `manifest.webmanifest` | App name, colours and icons for installing |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | Home-screen icons |

`index.html` works on its own, but browsers require the service worker to be a separate file, so offline use and dependable installation need all of them in the same folder.

## Installing on a phone

Open  directly in your browser.

- **Android (Chrome or other):** ⋮ menu → **Install app** or **Add to Home screen**.
- **iPhone (Safari):** Share → **Add to Home Screen**.

Once installed it opens full screen and works without a connection.

## Scanning tips

- Contrast helps most: a pale page on a darker table is ideal. White paper on a white desk is the hardest case.
- Fill most of the frame and keep the whole page in view. If an edge runs off the frame, the crop stops at the frame edge.
- Use **batch mode** (the stacked-pages button in the camera) to shoot a run of pages without stopping; each is cropped and saved automatically and you can fix any later.
- For a newspaper article, choose **Article**, tap the headline, its columns and any photo, then tap **Use**. The corners can still be adjusted by hand afterwards.

## Camera troubleshooting

If the camera is refused without any prompt, it is likely you downloaded the page and ran it by double clicking on it which usually blocks camera access. The camera screen explains which case applies and how to fix it, and always offers **Use the phone's camera app** as a fallback, which feeds the photo through the same detection and clean-up.

To reset a blocked permission:

- **Chrome:** tap the icon left of the address → Permissions → Camera → Allow.
- **Safari:** tap **aA** in the address bar → Website Settings → Camera → Allow.

## Browser support

Recent Chrome, Edge, Safari (iOS 16.4 or later) and Firefox. A few differences:

- Chrome on Android captures at the camera's full still resolution. Safari and Firefox capture at the live video resolution, which is plenty for letters but softer for a full broadsheet.
- The torch button appears only where the browser exposes the phone's flashlight (mainly Chrome on Android).
- HEIC photos import only in Safari. Other browsers need JPEG or PNG.

## Privacy and storage

Pages, thumbnails and (optionally) original photos are kept in the browser's IndexedDB for this site. Nothing is sent anywhere. Re-encoding strips location and other metadata from imported photos.

Browsers can clear site data when a device runs low on space. Flatbed asks the browser to mark its storage as persistent, and Settings shows how much space is used, but an encrypted backup is the safe way to keep scans long term. Clearing the browser's site data for this address deletes the library.

