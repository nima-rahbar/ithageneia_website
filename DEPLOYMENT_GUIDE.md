# 🌐 Website Deployment & Audio Streaming Guide: ithageneia.nimarahbar.com

This guide provides step-by-step instructions for deploying the **Ithageneia** platform to your subdomain:
`https://ithageneia.nimarahbar.com`

This deployment serves two purposes:
1. **Official Showcase Landing Page**: An introduction and download showcase website built with Bootstrap 5 and the color palette of `nimarahbar.com`.
2. **Audio Streaming Host**: Hosts all 50 Listening Comprehension MP3 files (`Thema_01.mp3` to `Thema_50.mp3`) with **CORS** and **Byte-Range Seeking enabled**, allowing your Android app to stream audio directly without bloating the APK file size!

---

## 📁 What is in `website_bundle/`

The `c:\Projects\ithageneia\website_bundle\` directory contains the showcase web package:

```text
website_bundle/
├── index.html                  # Official introduction & showcase landing page (Bootstrap 5)
├── style.css                   # Theme stylesheet with nimarahbar.com color scheme
├── .htaccess                   # Pre-configured Apache CORS & Byte-Range streaming headers
├── nginx.conf                  # Nginx equivalent config snippet (if using Nginx)
├── robots.txt                  # Search engine crawler permissions
├── assets/
│   └── maps/                   # Visual map assets
├── audio/                      # 50 Listening Comprehension MP3 tracks (~240 MB)
│   ├── Thema_01.mp3
│   ├── Thema_02.mp3
│   └── ... Thema_50.mp3
└── DEPLOYMENT_GUIDE.md         # This deployment guide
```

---

## 🚀 Deployment Options

### Method A: cPanel / Plesk / Web Hosting File Manager (Easiest)

1. **Compress the folder**:
   - In Windows File Explorer, select all files and folders inside `c:\Projects\ithageneia\website_bundle\` (including `.htaccess`).
   - Right click -> **Compress to ZIP file** (e.g. `website_bundle.zip`).
2. **Open your Hosting Control Panel** (cPanel / Plesk / DirectAdmin).
3. Navigate to **File Manager** -> go to the document root directory for `ithageneia.nimarahbar.com` (often `public_html/ithageneia` or `subdomains/ithageneia`).
4. Click **Upload** and upload `website_bundle.zip`.
5. Select the uploaded ZIP file and click **Extract**.
6. Ensure that `index.html` and `.htaccess` are directly inside the root folder of the subdomain.

---

### Method B: FTP / SFTP (FileZilla / WinSCP)

1. Open **FileZilla** or your preferred FTP client.
2. Connect to your server hosting `nimarahbar.com`.
3. Navigate to the web root directory of `ithageneia.nimarahbar.com`.
4. Drag and drop all contents of `c:\Projects\ithageneia\website_bundle\` to the server.
5. Wait for the 50 audio files and web assets to finish uploading.

---

### Method C: SSH / Git / VPS (Ubuntu / Debian / Nginx / Apache)

If you run your own VPS:
```bash
# Copy files to your web root
rsync -avz --progress /path/to/website_bundle/ user@nimarahbar.com:/var/www/ithageneia.nimarahbar.com/

# Ensure correct permissions
chown -R www-data:www-data /var/www/ithageneia.nimarahbar.com/
chmod -R 755 /var/www/ithageneia.nimarahbar.com/
```

If you use **Nginx**, copy the configuration from `website_bundle/nginx.conf` into your `/etc/nginx/sites-available/` block and reload Nginx:
```bash
sudo nginx -t && sudo systemctl reload nginx
```

---

## 🧪 Verification & Health Check

After uploading, verify that both the website and the audio streaming are working:

### 1. Web App Test
Visit `https://ithageneia.nimarahbar.com` in your browser:
- Check that the page loads with all 920 questions.
- Test dark/light mode toggle.
- Test question type filters (Cloze, Sorting, Recall, Maps, Multi-select).
- Test **🗣️ Προφορικά** and **✍️ Γραπτά** tabs.

### 2. Audio Streaming Test
Open this URL directly in your browser:
`https://ithageneia.nimarahbar.com/audio/Thema_01.mp3`
- The audio player should open and play immediately.
- Test clicking at the middle/end of the audio progress bar (seeking/scrubbing). If seeking works instantly without starting over, byte-range streaming is functioning properly!

### 3. CORS Check (Command Line)
In PowerShell or Terminal, verify the CORS header:
```bash
curl -I https://ithageneia.nimarahbar.com/audio/Thema_01.mp3
```
Expected response headers:
```http
HTTP/1.1 200 OK
Access-Control-Allow-Origin: *
Accept-Ranges: bytes
Content-Type: audio/mpeg
```

---

## 📱 How the Android App Connects to Your Host

We have already implemented the automatic streaming resolver in `app.js`:

```javascript
const REMOTE_AUDIO_BASE = 'https://ithageneia.nimarahbar.com/audio/';

function resolveAudioUrl(path) {
  if (!path) return '';
  if (path.startsWith('http://') || path.startsWith('https://')) return path;
  const fileName = path.split('/').pop();
  if (window.ITHAGENEIA_STREAM_AUDIO) {
    return `${REMOTE_AUDIO_BASE}${fileName}`;
  }
  return path;
}
```

### Key Advantages for Your Android App:
1. **Tiny APK Size**: You do NOT need to include the 240 MB `audio/` folder inside the Android APK. The APK will be only **~3 MB**, saving bandwidth and ensuring instant downloads on Google Play.
2. **Zero CORS Issues**: Because your `.htaccess` / `nginx.conf` includes `Access-Control-Allow-Origin: *` and `Accept-Ranges: bytes`, the Android WebView will stream and scrub audio with zero restrictions.
3. **Automatic Fallback**: If an audio file is missing locally, the player automatically falls back to `https://ithageneia.nimarahbar.com/audio/Thema_XX.mp3`.
