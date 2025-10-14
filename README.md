# 🎓 Final Capstone Report — Emotion Recognition in Large Language Models (LLMs)

Welcome to the official LaTeX source code repository for my final-year capstone project:

> **Emotion Recognition in Large Language Models (LLMs) via Hybrid Retrieval and Few-Shot Classification**

This repository contains the **complete LaTeX environment**, all report chapters, appendices, images, bibliography, and configuration files required to compile the entire research report into a professional PDF using **TeX Live 2025** and **Visual Studio Code (VS Code)**.

---

## 🗂️ Repository Overview

The repository follows a **modular LaTeX structure** for clarity and scalability.

```
📦 Final-Capstone-Report
 ┣ 📂 .vscode/              → VS Code LaTeX Workshop settings
 ┣ 📂 Images/               → All report figures and diagrams
 ┣ 📂 _minted/              → Auto-generated syntax highlighting cache (by minted)
 ┣ 📂 appendices/           → Additional appendices, extended tables, code listings
 ┣ 📂 chapters/             → Core report chapters (Intro, Methodology, Results, etc.)
 ┣ 📂 frontmatter/          → Title page, abstract, acknowledgments, TOC
 ┣ 📜 main.tex              → Root file that compiles the entire report
 ┣ 📜 preamble.tex          → All packages, formatting, fonts, and color themes
 ┣ 📜 references.bib        → Bibliography database (BibTeX format)
 ┣ 📜 titlepage.tex         → Custom title page design
 ┗ 📜 README.md             → This documentation
```

---

## ⚙️ Prerequisites

To compile the report correctly, you need these three core components installed:

1. **TeX Live 2025** — the LaTeX distribution  
2. **Visual Studio Code (VS Code)** — the text editor  
3. **LaTeX Workshop** — the VS Code extension for LaTeX compilation and preview  

---

## 🧰 Step 1 — Install TeX Live 2025

TeX Live is the official and complete LaTeX distribution for Windows, macOS, and Linux.  
It includes all required compilers (`xelatex`, `biber`, `latexmk`), fonts, and thousands of packages.

- 🌍 **Official website:** [https://tug.org/texlive/](https://tug.org/texlive/)
- 💾 **Size:** ~9 GB  
- ⏱️ **Time:** Installation may take up to an hour — **worth it** since it provides everything you’ll ever need for LaTeX.

After installation, TeX Live binaries are located in:

```
C:\texlive\2025\bin\windows\
```

> ⚠️ **Important:** Add this folder to your Windows PATH environment variable.  
Otherwise, VS Code won’t find `xelatex`, `biber`, or `latexmk`.

---

## 💻 Step 2 — Install Visual Studio Code

- Download VS Code here: [https://code.visualstudio.com/](https://code.visualstudio.com/)  
- Once installed, open the Extensions Marketplace (Ctrl + Shift + X) and install:

> 🔹 **LaTeX Workshop** by James Yu

This extension enables building, previewing, and error tracking for LaTeX projects.

---

## 🧩 Step 3 — Configure VS Code (`settings.json`)

Open VS Code and set up your LaTeX environment:

1. Press `Ctrl + Shift + P`
2. Type **“Preferences: Open Settings (JSON)”** and open it
3. Paste the following configuration:

```json
{
    "workbench.colorTheme": "Default High Contrast",
    "files.autoSave": "afterDelay",

    "latex-workshop.latex.tools": [
        {
            "name": "latexmk (xelatex)",
            "command": "C:/texlive/2025/bin/windows/latexmk.exe",
            "args": [
                "-xelatex",
                "-synctex=1",
                "-interaction=nonstopmode",
                "%DOC%"
            ]
        },
        {
            "name": "xelatex",
            "command": "C:/texlive/2025/bin/windows/xelatex.exe",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "%DOC%"
            ]
        },
        {
            "name": "biber",
            "command": "C:/texlive/2025/bin/windows/biber.exe",
            "args": [
                "%DOCFILE%"
            ]
        }
    ],

    "latex-workshop.latex.recipes": [
        {
            "name": "latexmk 🔁 (xelatex)",
            "tools": ["latexmk (xelatex)"]
        },
        {
            "name": "xelatex ➡ PDF",
            "tools": ["xelatex"]
        },
        {
            "name": "xelatex ➡ biber ➡ xelatex*2",
            "tools": ["xelatex", "biber", "xelatex", "xelatex"]
        }
    ],

    "workbench.editor.enablePreview": false,
    "window.zoomLevel": 2
}
```

✅ **This configuration ensures:**
- LaTeX Workshop uses **XeLaTeX** for Unicode and modern fonts
- **Biber** handles bibliography processing
- Auto-save triggers recompile
- The internal PDF viewer refreshes automatically

---

## 🧾 Step 4 — Compile the Report

Once setup is done:

1. Open the project folder in VS Code  
2. Open `main.tex`  
3. Press **Ctrl + Alt + B** (LaTeX Workshop build shortcut)  
4. Wait for the build to complete  
5. The generated file `main.pdf` will appear in the workspace

---
**Explanation:**
1. **XeLaTeX** compiles the main `.tex` file and creates temporary `.aux` and `.bcf` files.  
2. **Biber** reads the citations from `references.bib` and writes a `.bbl` file.  
3. **XeLaTeX** runs again (usually twice) to integrate citations and update cross-references.  
4. The final, clean **PDF** is generated.

---

## 🧩 Why XeLaTeX?

This project uses **XeLaTeX** instead of pdfLaTeX because:
- It supports **UTF-8 characters** and non-Latin scripts
- It can load **system fonts** directly (e.g., Times New Roman, Noto Sans)
- It’s fully compatible with:
  - `minted` (syntax highlighting)
  - `TikZ` (for diagrams)
  - `PlantUML` (for UML visuals)
- It produces higher-quality, modern typography

---

## 📚 Bibliography — `references.bib`

All references are stored in `references.bib` using **BibTeX** format.

Example:
```bibtex
@article{peffers2007design,
  title={Design Science Research Methodology for Information Systems Research},
  author={Peffers, Ken and Tuunanen, Tuure and Rothenberger, Marcus A and Chatterjee, Samir},
  journal={Journal of Management Information Systems},
  volume={24},
  number={3},
  pages={45--77},
  year={2007}
}
```

To compile with references:
- Use the **recipe** `xelatex ➡ biber ➡ xelatex*2` in VS Code
- Or run manually:
  ```bash
  xelatex main.tex
  biber main
  xelatex main.tex
  xelatex main.tex
  ```

---

## 🎨 Recommended Fonts

For best results under XeLaTeX:
| Font Role | Recommended Font |
|------------|------------------|
| Serif (main text) | Times New Roman or TeX Gyre Termes |
| Sans-serif | Noto Sans, Helvetica |
| Monospace | DejaVu Sans Mono |

---

## 🧠 Troubleshooting

| Problem | Cause | Solution |
|----------|--------|----------|
| `minted.sty not found` | Minimal TeX Live installation | Install **full TeX Live 2025** |
| `Pygments not installed` | Missing Python dependency | Run `pip install Pygments` |
| `biber not recognized` | PATH not updated | Add `C:\texlive\2025\bin\windows\` to PATH |
| PDF doesn’t refresh | Viewer cache | Close and reopen the PDF tab |
| Compilation stops halfway | Missing package | Run `tlmgr update --self --all` to update TeX Live |

---

## 💡 Tips for Editing

- Always compile with **XeLaTeX**, not pdfLaTeX.  
- Use relative paths for images:  
  ```latex
  \includegraphics[width=\textwidth]{Images/chart.png}
  ```
- Don’t manually delete `_minted/` — it’s managed automatically.  
- You can add new chapters by simply creating `.tex` files under `/chapters` and importing them in `main.tex`.

---

## 🧩 Example of File Inclusion

Inside `main.tex`, chapters are imported like this:

```latex
\input{frontmatter/titlepage}
\input{chapters/introduction}
\input{chapters/methodology}
\input{chapters/iterations}
\input{chapters/results}
\input{appendices/appendixA}
```

---

## 📘 Compilation Command (Manual)

If you prefer the terminal:

```bash
latexmk -xelatex main.tex
```

or step-by-step:
```bash
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex
```

---

## 🧠 Why TeX Live is Worth It

TeX Live may take time (around **9 GB** download), but it’s a **complete ecosystem**:
- Works offline
- Contains 4000+ packages
- Zero missing dependencies
- Same behavior across Windows, Linux, and macOS

Once installed, your environment will compile *any* academic paper, thesis, or technical report flawlessly.

> 💬 “It takes a while, but one installation to rule them all.”

---

## 📄 Project Metadata

| Field | Information |
|--------|-------------|
| **Author** | Aimen Guedhami *(Gathaa)* |
| **Institution** | South Mediterranean University — MedTech |
| **Degree** | Bachelor of Software Engineering |
| **Year** | 2025 |
| **Supervisor** | Dr. Jihene Ben Naceur |
| **Title** | Emotion Recognition in Large Language Models via Hybrid Retrieval and Few-Shot Classification |
| **Technologies** | LaTeX (XeLaTeX + Biber), TeX Live 2025, VS Code, Minted, TikZ |

---
## 🏁 Final Notes

This repository demonstrates a complete **Design Science Research (DSR)**-based LaTeX environment — modular, extensible, and ready for academic publication.  
It’s suitable for research reports, dissertations, and technical documentation.

---

## ⭐ Credits

Developed by **Aimen Guedhami (Gathaa)**  
B.Eng. Software Engineering — *South Mediterranean University (MedTech)*  
Final Capstone Report, Class of 2025  

If this setup helped you, please ⭐ star the repository — it helps others discover a ready-to-use professional LaTeX environment 💫

---

> 📜 “LaTeX is not just a typesetting system — it’s a mindset for precision, structure, and clarity.”
