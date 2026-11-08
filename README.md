# Real-Time Location Tracker

A single-page web app that covers both tracking options from the brief:

1. **Laptop by IP address** - looks up your public IP (or any IP you type) and plots the estimated position with an uncertainty circle.
2. **Phone by GPS** - streams live position with the browser Geolocation API, draws the path, and shows accuracy, speed, heading and distance travelled. The path can be exported as CSV.

The **Research notes** tab explains how IP geolocation works and its limits, and compares GPS with cell tower triangulation.

## Run it

Geolocation only works on HTTPS or `localhost`, so serve the folder instead of double-clicking the file:

```bash
cd location-tracker
python3 -m http.server 8000
```

Then open http://localhost:8000.

To test GPS on a phone, either deploy the folder to GitHub Pages / Netlify (both use HTTPS), or run the server on your laptop and use a tunnel such as `ngrok http 8000`.

## Using it on a phone (required for GPS)

Browsers only allow location on HTTPS. A saved file, a WhatsApp download or a `http://192.168...` link will not work. Easiest fix:

1. Create a GitHub repository and upload `index.html` (name it `index.html`).
2. Repository **Settings > Pages**, choose the `main` branch and `/ (root)`, then Save.
3. Open the `https://<your-username>.github.io/<repo>/` link in Chrome or Safari on the phone (not inside WhatsApp or Facebook).
4. Tap the GPS tab, then "Locate me now", and choose **Allow** (precise location) when asked.

Alternative: drag the folder onto https://app.netlify.com/drop for an instant HTTPS link.

## Tech

- Plain HTML, CSS and JavaScript, no build step
- [Leaflet](https://leafletjs.com/) with OpenStreetMap tiles for the map
- [ipwho.is](https://ipwho.is/) for IP lookups (free, no key)
- Browser Geolocation API (`watchPosition`) for GPS

## Notes

- IP results are approximate, usually the ISP's regional hub, not the street.
- Only track devices you own or have permission to track.
