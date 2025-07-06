
## 📚 CST8305 Slides — Local Backup & PDF Export

This guide documents how to:

✅ Pull all slides from your professor’s site
✅ Host them locally on your machine
✅ Verify they work
✅ Compile them into a single PDF using `decktape`
✅ Automate sending the PDF to a friend (optional)

---

## 📂 1️⃣ Download the Slides

The slides for week 5 are served from a **single HTML file** with slide anchors (`#1` → `#57`).
We use `wget` to mirror the main file and its dependencies:

```bash
# Make a working folder
mkdir -p ~/hakclub.com
cd ~/hakclub.com

# Pull the main slide page and its assets
wget --mirror --convert-links --adjust-extension --page-requisites --no-parent http://hakclub.com/utk/24W-CST8305/week5-LITE2.html
```

---

## 📂 2️⃣ Pull Missing Module Files

The slides load `.utk` module files dynamically.
They won’t show correctly without them.
Manually download any `.utk` modules the page needs:

```bash
# Create the modules folder if needed
mkdir -p utk/modules

# Download the specific modules you see 404s for in the browser DevTools
wget http://hakclub.com/utk/modules/cst8305-23f-networking-LITE-3.utk -P utk/modules/
wget http://hakclub.com/utk/modules/cst8305-23f-package-management-LITE-4.utk -P utk/modules/
```

---

## 🗂 3️⃣ Verify Folder Structure

Your final structure should look like:

```
hakclub.com/
 └── utk/
      ├── 24W-CST8305/
      │   └── week5-LITE2.html
      ├── remark-latest.min.js
      ├── styles/
      │   └── remark.css
      └── modules/
          ├── cst8305-23f-networking-LITE-3.utk
          └── cst8305-23f-package-management-LITE-4.utk
```

---

## ⚙️ 4️⃣ Host Locally Using Python

Serve the slides with a local HTTP server so all JS runs properly:

```bash
cd ~/hakclub.com
python3 -m http.server 8080
```

---

## ✅ 5️⃣ Verify It Works

Open your slides in the browser:

```
http://localhost:8080/utk/24W-CST8305/week5-LITE2.html#1
```

Use the arrow keys or navigation to flip through all slides (1–57).
Check the browser **Console** for missing file errors — download any missing modules.

---

## 🖨️ 6️⃣ Compile All Slides to PDF with Decktape

Decktape is a CLI tool that automates stepping through all slides and saving a PDF.

### 📌 Install Dependencies

Make sure `node` and `npm` are installed:

```bash
sudo apt update
sudo apt install nodejs npm -y
```

Install `decktape` globally:

```bash
sudo npm install -g decktape
```

Install Chrome if not already:

```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo apt install ./google-chrome-stable_current_amd64.deb
```

---

### 📌 Run Decktape

Run Decktape with the Chrome path to render all slides to PDF:

```bash
decktape --chrome-path=$(which google-chrome) remark http://localhost:8080/utk/24W-CST8305/week5-LITE2.html slides.pdf
```

---

## ✅ 7️⃣ Check the PDF

Verify:

```bash
xdg-open slides.pdf
```

---

## ✉️ 8️⃣ (Optional) Send to a Friend with Curl + Discord Webhook

If you want to share via Discord from the CLI:

1️⃣ Create a webhook in your channel:
*Channel Settings → Integrations → Webhooks → New Webhook → Copy URL*

2️⃣ Send the file:

```bash
WEBHOOK_URL="https://discord.com/api/webhooks/XXXX/YYYY"

curl -H "Content-Type: multipart/form-data" \
  -F "file=@slides.pdf" \
  $WEBHOOK_URL
```

---

## 🎉 Done!

You now have:

* A complete offline backup of the slides
* A single PDF for easy sharing
* A reproducible workflow for other weeks

---

**Happy studying! 🐧📚**
