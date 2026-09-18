# Ιθαγένεια Π.Ε.Γ.Π. — Επίσημη Ιστοσελίδα & Audio Streaming Host

[![Website](https://img.shields.io/badge/Website-ithageneia.nimarahbar.com-009bdf?style=for-the-badge&logo=googlechrome&logoColor=white)](https://ithageneia.nimarahbar.com)
[![Google Play](https://img.shields.io/badge/Google_Play-10.00_€-34d399?style=for-the-badge&logo=googleplay&logoColor=white)](https://play.google.com/store/apps/details?id=com.nimarahbar.ithageneia)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)](LICENSE)
[![Bootstrap 5](https://img.shields.io/badge/Bootstrap-5.3.3-7952b3?style=for-the-badge&logo=bootstrap&logoColor=white)](https://getbootstrap.com)

Η επίσημη ιστοσελίδα παρουσίασης, τεκμηρίωσης και φιλοξενίας ηχητικών θεμάτων (Audio Streaming Host) για την εφαρμογή **Ιθαγένεια Π.Ε.Γ.Π.** (Πιστοποιητικό Επάρκειας Γνώσεων για Πολιτογράφηση) για Android.

---

## 🌟 Κύρια Χαρακτηριστικά Ιστοσελίδας

- **Παρουσίαση Εφαρμογής & Ύλης**:
  - Πλήρης επισκόπηση των 920+ ερωτήσεων της επίσημης τράπεζας θεμάτων (Ιστορία, Γεωγραφία, Πολιτικοί Θεσμοί, Πολιτισμός, Γλώσσα).
  - Ενημέρωση για τις προδιαγραφές και τη δομή των εξετάσεων Π.Ε.Γ.Π. του Υπουργείου Εσωτερικών.
- **Υποστήριξη Μεταφράσεων σε 4 Γλώσσες & Interactive Simulator**:
  - Πλήρης παρουσίαση της νέας δυνατότητας μετάφρασης σε **English**, **فارسی (Persian)**, **العربية (Arabic)** και **Türkçe**.
  - Διαδραστικός προσομοιωτής ερωτήσεων (Interactive Question Simulator) με άμεση εναλλαγή γλώσσας, δίγλωσση προβολή (side-by-side) και υποστήριξη RTL διάταξης για τα Περσικά και Αραβικά.
- **Interactive Light & Dark Mode Preview**:
  - Διαδραστικός split-screen slider (σύγκριση πριν/μετά) για προεπισκόπηση του Φωτεινού και Σκούρου θέματος (OLED-friendly) της εφαρμογής απευθείας μέσα στο smartphone mockup.
- **Foldable & Tablet Devices Showcase**:
  - Ειδική ενότητα ανάδειξης της υποστήριξης αναδιπλούμενων συσκευών (Foldables) και Tablets (Dual-Pane adaptive layout, Continuity, Side Rail Navigation).
- **Audio Streaming Host**:
  - Φιλοξενεί και τα 50 ηχητικά αρχεία MP3 (`Thema_01.mp3` έως `Thema_50.mp3`) της ενότητας Κατανόησης Προφορικού Λόγου.
  - Ενεργοποιημένο **Byte-Range Seeking** (`Accept-Ranges: bytes`) και **CORS** (`Access-Control-Allow-Origin: *`), επιτρέποντας στην Android εφαρμογή να κάνει streaming χωρίς να επιβαρύνει το μέγεθος του APK (το APK διατηρείται στα ~3 MB).
- **Google Play Store Link**:
  - Άμεση κατεύθυνση στο Google Play Store (εφάπαξ αγορά 10,00 € χωρίς διαφημίσεις ή συνδρομές).
- **Responsive & Modern UI**:
  - Σχεδιασμένο με Bootstrap 5.3, Bootstrap Icons και το επίσημο χρωματικό σύστημα της [nimarahbar.com](https://nimarahbar.com).

---

## 📁 Δομή Αρχείων (Project Structure)

```text
website_bundle/
├── index.html              # Η κύρια responsive σελίδα υποδοχής & παρουσίασης
├── privacy_policy.html     # Επίσημη Πολιτική Απορρήτου (Google Play & GDPR compliant)
├── style.css               # Προσαρμοσμένο CSS, χρωματική παλέτα & animations
├── .htaccess               # Apache διαμόρφωση για CORS, Byte-Ranges & Caching
├── nginx.conf              # Nginx διαμόρφωση (εναλλακτική για VPS / LEMP)
├── robots.txt              # Ρυθμίσεις ευρετηρίασης μηχανών αναζήτησης
├── LICENSE                 # Άδεια χρήσης MIT
├── assets/                 # Εικόνες, λογότυπα και γραφικά mockups
│   ├── favicon.png         # Επίσημο favicon
│   ├── icon.png            # Εικονίδιο εφαρμογής υψηλής ανάλυσης
│   ├── nimarahbar.png      # Επίσημο λογότυπο δημιουργού
│   ├── main-light.png      # Screenshot εφαρμογής (Φωτεινή λειτουργία)
│   ├── main-dark.png       # Screenshot εφαρμογής (Σκοτεινή λειτουργία)
│   ├── Fold.jpg            # Mockup αναδιπλούμενης συσκευής (ξεδιπλωμένη προβολή)
│   ├── Un-Fold.jpg         # Mockup smartphone προβολής
│   └── maps/               # Διαδραστικοί/βοηθητικοί χάρτες
├── audio/                  # 50 ηχητικά θέματα MP3 (~240 MB)
│   ├── Thema_01.mp3
│   ├── Thema_02.mp3
│   └── ... Thema_50.mp3
└── DEPLOYMENT_GUIDE.md     # Αναλυτικός οδηγός ανάπτυξης & ρυθμίσεων server
```

---

## 🚀 Ανάπτυξη & Φιλοξενία (Deployment)

### 1. Apache / cPanel / Plesk (Συνιστώμενο)
1. Ανεβάστε όλα τα αρχεία του φακέλου στο web root του subdomain (π.χ. `public_html/ithageneia/`).
2. Βεβαιωθείτε ότι το αρχείο `.htaccess` περιλαμβάνεται κανονικά (τα κρυφά αρχεία με τελεία πρέπει να εμφανίζονται στον File Manager / FTP client).
3. Το `.htaccess` εξασφαλίζει:
   ```apache
   # Επιτρέπει streaming σε Android WebViews και mobile players
   Header set Access-Control-Allow-Origin "*"
   Header set Accept-Ranges "bytes"
   ```

### 2. Nginx / VPS
Αν χρησιμοποιείτε διακομιστή Nginx, ενσωματώστε τις ρυθμίσεις από το `nginx.conf`:
```nginx
location /audio/ {
    add_header Access-Control-Allow-Origin "*";
    add_header Accept-Ranges bytes;
    types {
        audio/mpeg mp3;
    }
}
```

---

## 🛠️ Τεχνολογίες

- **HTML5 & Vanilla JavaScript**: Ελαφρύς κώδικας, μηδενικές εξωτερικές εξαρτήσεις frameworks, άμεση φόρτωση.
- **Bootstrap 5.3.3**: Grid system, responsive utility classes και components.
- **Bootstrap Icons**: Ενσωμάτωση SVG εικονιδίων διεπαφής.
- **Modern CSS3**: CSS custom properties, glassmorphism, flexbox/grid και interactive clip-path sliders.

---

## 👨‍💻 Δημιουργός

Αναπτύχθηκε από τον **Nima Rahbar** (Senior Web Designer & Developer).

- **Website**: [nimarahbar.com](https://nimarahbar.com)
- **LinkedIn**: [linkedin.com/in/nimarahbar](https://www.linkedin.com/in/nimarahbar/)
- **GitHub**: [@nima-rahbar](https://github.com/nima-rahbar)

---

## 📄 Άδεια Χρήσης

Το παρόν έργο διατίθεται υπό τους όρους της άδειας [MIT License](LICENSE).
