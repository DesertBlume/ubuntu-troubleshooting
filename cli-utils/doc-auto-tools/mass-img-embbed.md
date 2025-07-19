# Lab PDF Generator

This is a Bash + Pandoc utility script that automates the generation of professional lab report PDFs from a collection of `.png` images. It includes a customizable cover page, auto-generated captions based on image filenames, and proper formatting for submission-ready documents.

---

## Requirements

This tool requires the following software to be installed on your system:

```bash
sudo apt update
sudo apt install pandoc texlive-latex-base texlive-fonts-recommended texlive-latex-extra
````

Tested on Ubuntu 24.04 LTS.

---

## Usage

1. Place the `make_lab_pdf.sh` script and all desired `.png` images into the same directory.

Example:

```
Lab05/
├── make_lab_pdf.sh
├── Screenshot 1.png
├── Screenshot 2.png
├── Screenshot 3.png
```

2. Run the script:

```bash
chmod +x make_lab_pdf.sh
./make_lab_pdf.sh
```

The script will prompt for:

* The desired name of the final PDF (e.g., `haja0013_lab_5`)
* The lab number or title (e.g., `Lab 05`)
* Your full name (default: Hmoad Hajali)
* Your email address (default: [Haja0013@algonquinlive.com](mailto:Haja0013@algonquinlive.com))
* The instructor's name (default: Dan Chase)

The script will then:

* Create a temporary Markdown file with a cover page and one image per page
* Automatically caption each image using the filename (without the extension)
* Generate a PDF using Pandoc with LaTeX formatting
* Save the result to the current directory as `<filename>.pdf`

---

## Output

The resulting PDF will contain:

* A clean, professional cover page with name, email, instructor, and the current date
* One image per page, with a bold caption below each image
* Proper page breaks using LaTeX `\newpage`

Images are sorted alphabetically by filename. Filenames with spaces or special characters are supported.

---

## Features

* Cover page generation with dynamic metadata
* Filename-based captions
* Alphabetical sorting of images
* Safe handling of spaces and special characters in filenames
* Compatible with standard LaTeX rendering engines

---

## Potential Improvements

* Support for additional image formats (`.jpg`, `.jpeg`, `.webp`)
* Centering and scaling of images via LaTeX customization
* Optional templates for customized document styling
* GitHub Actions workflow for automated PDF generation on push

---

## License

This script is open for personal, academic, or internal institutional use. Contributions and adaptations are welcome. No warranties provided.

---

## Author

Developed by Hmoad Hajali
Email: [haja0013@algonquinlive.com](mailto:haja0013@algonquinlive.com)
Institution: Algonquin College


