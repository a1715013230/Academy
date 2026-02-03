# Prompt Library (Mechanics x ML)

This folder contains original prompts tuned for mechanics / computational physics + machine learning writing.

Design goals
- Domain-aware structure (PDE/BC/IC, discretization, data regime, physical consistency)
- Paper-quality tone (ICLR/ICML-style), minimal fluff
- Word-friendly Chinese variants when relevant

Source inspiration (not copied)
- https://github.com/Leey21/awesome-ai-research-writing

Prompts
- `zh2en-academic-latex.md`: Chinese draft -> English academic LaTeX (mechanics+ML)
- `en2zh-readable.md`: English LaTeX -> readable Chinese (mechanics+ML)
- `zh2zh-word-rewrite.md`: Chinese draft -> Chinese academic paragraph (Word), mechanics+ML
- `shorten-english-latex.md`: Tighten English LaTeX by 5-15 words (keep meaning)
- `expand-english-latex.md`: Expand an English paragraph with missing details placeholders
- `polish-english-mechanics-ml.md`: Style polish for mechanics+ML paper English
- `logic-check-reviewer.md`: Reviewer-style logic + assumption + leakage checks
- `experiment-analysis.md`: Turn raw results into a solid mechanics+ML experiment paragraph
- `captions-figure.md`: Figure caption generator for mechanics+ML
- `captions-table.md`: Table caption generator for mechanics+ML
- `model-selection.md`: Model choice helper (PINN/FNO/DeepONet/surrogate)
