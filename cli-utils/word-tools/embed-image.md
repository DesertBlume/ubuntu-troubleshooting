##  **Create a Word File with an Embedded Image Using the CLI**

This guide explains how to generate a **Word (`.docx`)** or **OpenDocument (`.odt`)** file containing text and an image **entirely from the terminal**, using **Pandoc** and Markdown.

---

###  **Why use Pandoc?**

[Pandoc](https://pandoc.org) is a powerful universal document converter.
It allows you to write your content once — in a simple, readable **Markdown** file — and then convert it to many formats like `.docx`, `.odt`, `.pdf`, and more.

Using Pandoc from the terminal makes it easy to:

* Automate reports
* Batch-generate documents
* Include images, headings, lists, tables, and code

---

###  **Step 1 — Install Pandoc**

On Ubuntu:

```bash
sudo apt update
sudo apt install pandoc
```

---

###  **Step 2 — Create a Markdown file**

Pandoc uses **Markdown** (`.md`) as input.
A Markdown file is just plain text with simple formatting syntax.

>  **Important:** The source file must use the `.md` extension so Pandoc knows how to parse it.

Example command to create a Markdown file with an embedded image:

```bash
echo '# Lab Screenshot' > MyLabFile.md
echo 'This document shows how to embed an image from the CLI.' >> MyLabFile.md
echo '' >> MyLabFile.md
echo '![Figure Description](full-image-name.png)' >> MyLabFile.md
```

* Replace **`Figure Description`** with a caption or alt text for the image.
* Replace **`full-image-name.png`** with the actual name of your image file, including the extension.
  This file must be in the **same directory** when you convert.

---

###  **Step 3 — Convert to Word (`.docx`)**

Run Pandoc to generate your Word document:

```bash
pandoc MyLabFile.md -o MyLabReport.docx
```

* `MyLabFile.md` is your input Markdown file.
* `-o MyLabReport.docx` sets the output file name and format.
* You can change the extension to `.odt` if you prefer OpenDocument.

---

###  **Step 4 — Verify the Output**

To quickly verify the Word file opened correctly, use:

```bash
xdg-open MyLabReport.docx
```

This will open the file in your system’s default Word processor (LibreOffice Writer or MS Word if installed).

---

##  **Summary**

**Install Pandoc** — the universal converter
**Write content in Markdown** — simple syntax, includes images
**Run Pandoc** — convert `.md` to `.docx`
**Verify** — open the generated Word file to confirm the image is embedded

---

**This method is ideal for scripts, batch reports, or lightweight documentation workflows on Linux.**

**No GUI required.**

---

**Maintained by: Hmoad Hajali**

---
