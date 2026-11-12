# Zeldin Prelight

Browser-based cinematography lighting previsualization (Three.js). No build step.

## Files
- `app.html`  - the editor (keep this PRIVATE if you want the password to mean anything)
- `protect.html` - tool that encrypts `app.html` with your password and gives you `index.html`
- `vendor/` - Three.js r128 and helpers (MIT, see vendor/THREE-LICENSE.txt)

## Publish on GitHub Pages with a password
1. Open `protect.html` in your browser (double-click). If it says encryption is blocked, run
   `python3 -m http.server 8000` in this folder and open http://localhost:8000/protect.html
2. Choose `app.html`, type a password (16+ characters or 4+ random words), click the button.
   Your browser downloads a protected `index.html`.
3. Create a GitHub repository. Upload ONLY `index.html` and the `vendor` folder.
   Do NOT upload `app.html` or `protect.html`.
4. Settings > Pages > Deploy from a branch > `main` / root > Save.
5. Visit `https://<username>.github.io/<repo>/` and enter the password.

To change the app later, edit `app.html`, then repeat steps 1-3 (re-upload `index.html`).

## How strong is this?
`index.html` contains the editor encrypted with AES-256-GCM, with the key derived from your password (PBKDF2, 600,000 rounds). Without the password nobody can read or run the editor, even with the address or the files.
It is still a single shared password, not accounts: anyone you give it to can enter, you cannot revoke one person, and a weak password can be guessed offline. Use a long passphrase.
For real per-user logins, put the site behind Cloudflare Access (free for small teams) or similar.

## Using the editor
Run locally by opening `app.html`. Features: lights (spot with barn doors/grid, RGB LED panel, tube, softbox, octabox, lantern, bulb, sun), flags, bounce board, mannequin, box / sphere / triangle props, cinema camera with camera view, manual photo fit (vanishing points), props from GLB import or a Hugging Face Space (experimental), New / Clear.

## Hugging Face prop generation (experimental)
Upload a photo of ONE object, check the Space id and API name (the Space page, "Use via API"), optionally paste a free HF token, and click Generate. Free Spaces are shared, can be slow or asleep, and may change their interface. The token is stored only in your browser. You can instead generate a GLB on the Space's website and use the GLB import.

## Known limits
Area lights give soft illumination but not true soft shadows (shadow helper is approximate). Intensity is relative. Diffusion lowers output only. Nothing is saved between visits yet. Check each AI model's licence before commercial use.
