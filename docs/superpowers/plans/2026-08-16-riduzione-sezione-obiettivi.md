# Riduzione della sezione 1.2 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Ridurre di circa il 50% la sezione 1.2 «Obiettivi dell'elaborato» senza perdere contenuti, citazioni o registro accademico.

**Architecture:** La sezione sarà riscritta come una sequenza di sette paragrafi: contesto e riferimento architetturale; limite del metodo originario e obiettivo YOLO; dataset; fine-tuning e real-time; motivazione e compromessi; integrazione; norma e criteri finali. I dettagli tecnici già destinati ai capitoli successivi saranno condensati.

**Tech Stack:** LaTeX, BibLaTeX/Biber, latexmk con pdfLaTeX.

## Global Constraints

- Mantenere invariati il contenuto sostanziale, il registro accademico e le fonti.
- Conservare tutti i nove nuclei informativi elencati nella specifica approvata.
- Non introdurre nuovi obiettivi né dichiarare la conformità alla norma UNI EN ISO 20380:2019.
- Portare il testo dalle attuali 1218 parole a un intervallo indicativo di 550–670 parole.

---

### Task 1: Condensare e verificare la sezione 1.2

**Files:**
- Modify: `chapters/01-introduzione.tex:62-96`

**Interfaces:**
- Consumes: contenuti e citazioni della sezione 1.2 attuale; specifica `docs/superpowers/specs/2026-08-16-riduzione-sezione-obiettivi-design.md`.
- Produces: una sezione 1.2 più breve, collegata senza modifiche alle sezioni 1.1 e 1.3.

- [ ] **Step 1: Registrare la lunghezza iniziale**

Run:

```bash
awk '/\\section\{Obiettivi dell.elaborato\}/{capture=1; next} /\\section\{Struttura dell.elaborato\}/{capture=0} capture' chapters/01-introduzione.tex | sed '/^%/d' | wc -w
```

Expected: `1218` parole.

- [ ] **Step 2: Riscrivere la sezione**

Sostituire i tredici paragrafi correnti con sette paragrafi che preservino, nell'ordine: Nauta e DEWS; complessità dell'ambiente e sostituzione del rilevatore con YOLO; dataset; fine-tuning e real-time; vantaggi e compromessi; integrazione nella pipeline; norma UNI e criteri di valutazione. Conservare le chiavi di citazione `Eng2008DEWS`, `Eng2004Region`, `Eng2006Robust`, `Redmon2016YOLO` e `UNI20380` vicino alle rispettive affermazioni.

- [ ] **Step 3: Misurare la riduzione**

Run:

```bash
awk '/\\section\{Obiettivi dell.elaborato\}/{capture=1; next} /\\section\{Struttura dell.elaborato\}/{capture=0} capture' chapters/01-introduzione.tex | sed '/^%/d' | wc -w
```

Expected: da `550` a `670` parole.

- [ ] **Step 4: Controllare contenuti e citazioni**

Run:

```bash
sed -n '/\\section{Obiettivi dell.elaborato}/,/\\section{Struttura dell.elaborato}/p' chapters/01-introduzione.tex
```

Expected: tutti i nuclei informativi della specifica sono presenti; la dichiarazione normativa resta esplicitamente non certificativa; non compaiono nuove citazioni.

- [ ] **Step 5: Compilare il documento**

Run dalla directory del plugin LaTeX:

```bash
python3 scripts/compile_latex.py /Users/mottyppo/Desktop/Tesi/main.tex --compiler texlive --json
```

Expected: exit code `0`, `main.pdf` generato e nessun riferimento bibliografico non risolto introdotto dalla modifica.

- [ ] **Step 6: Registrare la modifica**

```bash
git add chapters/01-introduzione.tex main.pdf
git commit -m "docs: condense thesis objectives section"
```
