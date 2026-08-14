# Revisione dell'introduzione e della bibliografia Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Completare `bibliography/bibliography.bib` con una voce accurata per ciascuna delle 21 fonti locali e correggere nel Capitolo 1 soltanto errori fattuali, citazioni e formulazioni problematiche.

**Architecture:** L'intervento separa l'identificazione documentale dalla revisione editoriale. Prima si costruisce un inventario uno-a-uno tra file e record BibLaTeX; poi si correggono citazioni e testo; infine si verifica l'intero documento con LaTeX/Biber e controllo visivo del PDF.

**Tech Stack:** LaTeX, BibLaTeX con backend Biber e stile numerico, Poppler (`pdfinfo`, `pdftotext`, `pdftoppm`), strumenti LaTeX disponibili nel workspace.

## Global Constraints

- Conservare struttura, tono e impostazione generale del Capitolo 1.
- Non riscrivere paragrafi corretti per preferenze stilistiche.
- Non modificare indice, altri capitoli o impostazione grafica generale.
- Inserire una voce bibliografica per ciascuno dei 21 file in `docs/`.
- Citare una fonte soltanto quando sostiene effettivamente l'affermazione associata.
- Mantenere `\nocite{*}` e quindi includere in bibliografia anche le fonti non richiamate nel Capitolo 1.
- Non dichiarare conformità o certificazione rispetto alle norme tecniche.

---

### Task 1: Inventario documentale e metadati

**Files:**
- Read: `docs/Medica/*`
- Read: `docs/Tecnica/Utile/*`
- Read: `docs/Tecnica/Standard/*`

**Interfaces:**
- Consumes: i 21 file locali elencati da `rg --files docs -g '*.pdf' -g '*.mp4'`.
- Produces: una mappatura verificata `percorso locale -> chiave BibLaTeX -> tipo di voce -> metadati` usata nei task successivi.

- [ ] **Step 1: Confermare l'inventario**

Run:

```bash
rg --files docs -g '*.pdf' -g '*.mp4' | sort
rg --files docs -g '*.pdf' -g '*.mp4' | wc -l
```

Expected: 21 percorsi distinti e conteggio `21`.

- [ ] **Step 2: Estrarre i metadati incorporati e le prime pagine**

Run:

```bash
for file in docs/**/*.pdf(.N); do pdfinfo "$file" | rg '^(Title|Author|Subject|CreationDate|Pages):'; done
for file in docs/**/*.pdf(.N); do pdftotext -f 1 -l 2 -layout "$file" -; done
ffprobe -v error -show_entries format_tags -of default=noprint_wrappers=1 "docs/Medica/THE REASONS PEOPLE DROWN.mp4"
```

Expected: metadati sufficienti per i PDF nativi; i quattro file `126685395.pdf`--`126685398.pdf` risultano scansioni e vengono identificati dalle pagine renderizzate.

- [ ] **Step 3: Verificare i dati bibliografici incerti**

Controllare DOI e pagine editoriali autorevoli per articoli e atti di conferenza; controllare le pagine ufficiali di OMS, Unione europea e organismi di normazione per le fonti istituzionali. Per il video registrare titolo, autore/canale, data e URL visibili nel contenuto o nei metadati, senza inventare campi mancanti.

Expected: ogni file ha titolo, autore o ente responsabile, anno e tipo documentale; i campi non dimostrabili vengono omessi.

### Task 2: Ricostruzione della bibliografia

**Files:**
- Modify: `bibliography/bibliography.bib`

**Interfaces:**
- Consumes: la mappatura documentale prodotta dal Task 1.
- Produces: 21 record BibLaTeX univoci, inclusi i record richiamati dal Capitolo 1.

- [ ] **Step 1: Dimostrare che la bibliografia corrente è incompleta**

Run:

```bash
rg -c '^@' bibliography/bibliography.bib
```

Expected before modification: conteggio `1`, relativo alla voce dimostrativa fittizia.

- [ ] **Step 2: Sostituire la voce fittizia con i record reali**

Usare tipi BibLaTeX standard coerenti (`@article`, `@inproceedings`, `@report`, `@manual`, `@online` o `@misc`) e chiavi leggibili. Includere DOI, volume, numero, pagine, editore e URL soltanto quando verificati. Conservare le chiavi già semanticamente corrette usate nel testo, tra cui `WHO2026Drowning`, `Federalberghi2026`, `Eng2008DEWS`, `Kam2002Drowning`, `Eng2004Region`, `Eng2006Robust`, `Eng2003Automatic`, `Redmon2016YOLO` e `UNI20380`.

- [ ] **Step 3: Verificare quantità, unicità e sintassi dei record**

Run:

```bash
rg -c '^@' bibliography/bibliography.bib
rg '^@[A-Za-z]+\{[^,]+' bibliography/bibliography.bib | sort
biber --tool --validate-datamodel bibliography/bibliography.bib
```

Expected: 21 record, 21 chiavi distinte e nessun errore di sintassi o del modello dati.

- [ ] **Step 4: Salvare il risultato bibliografico**

```bash
git add bibliography/bibliography.bib
git commit -m "docs: populate thesis bibliography"
```

### Task 3: Correzione conservativa del Capitolo 1

**Files:**
- Modify: `chapters/01-introduzione.tex`

**Interfaces:**
- Consumes: chiavi e metadati definiti in `bibliography/bibliography.bib`.
- Produces: testo con citazioni risolte e affermazioni coerenti con le fonti.

- [ ] **Step 1: Inventariare le citazioni attuali**

Run:

```bash
rg -o '\\cite\{[^}]+\}' chapters/01-introduzione.tex | sort -u
```

Expected: l'elenco evidenzia le chiavi originariamente non definite, comprese quelle relative a OMS, Federalberghi, Pia, DEWS e UNI EN ISO 20380.

- [ ] **Step 2: Correggere identificazione e citazione della fonte OMS**

Sostituire il riferimento al *Global Status Report on Drowning Prevention 2024* con la scheda informativa *Drowning* dell'OMS, datata 1° maggio 2026, e usare `\cite{WHO2026Drowning}` per le statistiche sui circa 300.000 decessi annui e sulle fasce d'età.

- [ ] **Step 3: Correggere le citazioni e le formulazioni documentali**

Allineare le chiavi del testo ai record reali; distinguere chiaramente dati epidemiologici, descrizioni comportamentali e scelte architetturali. Mantenere le limitazioni già espresse per il rapporto Federalberghi e per la norma UNI EN ISO 20380. Rimuovere o attenuare soltanto le affermazioni che la fonte citata non dimostra.

- [ ] **Step 4: Eliminare il blocco storico commentato superato**

Rimuovere esclusivamente il precedente abbozzo commentato e la nota che ne prescrive l'eliminazione, poiché duplicano il capitolo corrente e contengono riferimenti ormai superati. Conservare i commenti relativi alle future figure o tabelle.

- [ ] **Step 5: Controllare tutte le chiavi citate contro la bibliografia**

Run:

```bash
rg -o '\\cite\{[^}]+\}' chapters/01-introduzione.tex | sort -u
rg '^@[A-Za-z]+\{[^,]+' bibliography/bibliography.bib | sort
```

Expected: ogni chiave del primo elenco è definita nel secondo; nessuna chiave fittizia rimane.

- [ ] **Step 6: Salvare la revisione del capitolo**

```bash
git add chapters/01-introduzione.tex
git commit -m "docs: correct introduction sources"
```

### Task 4: Compilazione e controllo finale

**Files:**
- Verify: `main.tex`
- Verify: `main.pdf`
- Verify: `main.log`
- Verify: `main.blg`

**Interfaces:**
- Consumes: bibliografia e Capitolo 1 aggiornati.
- Produces: PDF compilato e prove di assenza di errori bibliografici o difetti visivi introdotti.

- [ ] **Step 1: Compilare l'intero documento con Biber**

Run:

```bash
latexmk -pdf -interaction=nonstopmode -halt-on-error main.tex
```

Expected: exit code `0` e generazione di `main.pdf`.

- [ ] **Step 2: Controllare i log**

Run:

```bash
rg -n 'undefined|Citation.*not found|Biber error|ERROR|FATAL' main.log main.blg
```

Expected: nessuna citazione o riferimento irrisolto e nessun errore Biber.

- [ ] **Step 3: Renderizzare e ispezionare le pagine rilevanti**

Run:

```bash
mkdir -p tmp/pdfs/final
pdftoppm -png -r 120 main.pdf tmp/pdfs/final/main
```

Ispezionare l'inizio del Capitolo 1 e tutte le pagine della bibliografia. Expected: testo leggibile, citazioni numeriche renderizzate, voci bibliografiche non troncate e assenza di sovrapposizioni o caratteri mancanti.

- [ ] **Step 4: Eseguire il controllo finale delle modifiche**

Run:

```bash
git diff --check
git status --short
```

Expected: nessun errore di whitespace; soltanto i file previsti e gli artefatti di compilazione già tracciati risultano modificati.

- [ ] **Step 5: Salvare la correzione del conteggio nella specifica e il piano**

```bash
git add docs/superpowers/specs/2026-08-14-revisione-introduzione-bibliografia-design.md docs/superpowers/plans/2026-08-14-revisione-introduzione-bibliografia.md main.pdf
git commit -m "docs: verify bibliography revision"
```
