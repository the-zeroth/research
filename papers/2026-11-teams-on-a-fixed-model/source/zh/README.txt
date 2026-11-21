固定模型之上的智能体团队：The One 两个月框架实验（中文版，预印本，2026 年 11 月）

编译（XeLaTeX，通过 Tectonic；BibTeX 自动运行）：
  tectonic -X compile main.tex
用 TeX Live：xelatex main && bibtex main && xelatex main && xelatex main

中文字体：main.tex 里的 fontset=mac 使用 macOS 自带字体；在 Linux 或 Windows 上改为 fontset=fandol（TeX Live 自带）。
西文字体：TeX Gyre Termes、TeX Gyre Termes Math、TeX Gyre Heros、Inconsolata（均在 TeX Live 中）。
