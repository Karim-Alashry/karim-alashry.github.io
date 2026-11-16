# Karim Alashry: The Story Behind the Character (Issue #01)

An interactive comic-book portfolio. Static HTML, CSS and vanilla JavaScript (CSS 3D transforms, IntersectionObserver, requestAnimationFrame). No backend, no build step, no JS libraries. Google Fonts (Syne, DM Sans, Bangers, Cairo) load online and fall back to system fonts offline.

## How it reads
18 "pages": cover (opens in 3D as you scroll), Chapter 01 Journey (opener + 5 job scenes), Chapter 02 Skills, Chapter 03 Missions (2 pages), Chapter 04 Creative Universe (opener, videos, photography, universe + Instagram), Chapter 05 Education & Certifications (2 pages), Final chapter Contact, and "TO BE CONTINUED...". A fixed reading indicator shows `CHAPTER / PAGE n / 18`. Reduced-motion users get the same content with no 3D or scroll animation; tablets and phones get lighter motion.

## Folder structure
```
karim-portfolio/
  index.html
  README.md
  assets/
    images/
      karim-character-panels.png      official multi-panel image (source)
      karim-comic-portrait.png/.webp  central portrait (png = full-res source, webp = used on page)
      crop-voice / photo / cx / team / creative / rap / face .webp   panel crops
      photo-01 ... photo-05.webp      photographs, in the order you supplied them
    documents/Karim-Alashry-CV.pdf
    audio/karim-universe-soundtrack.mp3
  previews/
    open-cage-preview.mp4/.jpg   لعنة القفص المفتوح
    replay-curse-preview.mp4/.jpg   لعنة الإعادة
    version-tani-preview.mp4/.jpg   VERSION تاني
```

## Run locally
```
python3 -m http.server 8000
```
then open http://localhost:8000

## Editing
- **Text/data**: experience, skills, missions, videos, photos and certificates are arrays at the top of the `<script>` in `index.html` (`XP`, `CATS`, `MIS`, `VIDEOS`, `PHOTOS`, `CERTS`).
- **Music**: replace `assets/audio/karim-universe-soundtrack.mp3` (same name). If missing, the player shows UNAVAILABLE and nothing else breaks. Music never autoplays and pauses while a video preview plays.
- **Video previews**: replace the `.mp4` and `.jpg` in `previews/` (same names). Clip: `ffmpeg -ss 4 -t 14 -i full.mp4 -vf scale=540:-2 -c:v libx264 -crf 29 -c:a aac -b:a 96k -movflags +faststart previews/name.mp4`; thumbnail: `ffmpeg -ss 7 -i full.mp4 -frames:v 1 -vf scale=540:-2 previews/name.jpg`.
- **Photos**: replace `photo-0X.webp`; captions are archival (SHOT 01-05) only.
- **CV**: replace `assets/documents/Karim-Alashry-CV.pdf`.
- **Social preview**: after deploying, change the `og:image` URL in `<head>` to the full address of `assets/images/karim-comic-portrait.png`.

## Deploy to GitHub Pages
1. New **public** repository (e.g. `karim-portfolio`), no README/.gitignore/license.
2. Upload the *contents* of this folder (so `index.html` sits at the repo root, plus `assets/` and `previews/`).
3. Settings > Pages > Deploy from a branch > `main` / `(root)` > Save.
4. Open `https://<username>.github.io/karim-portfolio/`. All paths are relative.
