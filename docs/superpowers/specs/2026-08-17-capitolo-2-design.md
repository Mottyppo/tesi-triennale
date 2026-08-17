# Specifica editoriale del Capitolo 2

Data: 17 agosto 2026

## Obiettivo

Realizzare il Capitolo 2 della tesi, dedicato ai fondamenti teorici, mantenendo lo stile discorsivo e accademico del Capitolo 1. Il capitolo deve fornire soltanto il contesto necessario a comprendere l'intervento progettuale: una descrizione sintetica di DEWS, un approfondimento dei descrittori comportamentali, una trattazione estesa di YOLO e le motivazioni della sostituzione del rilevatore originale.

## Fonti

La stesura deve basarsi principalmente sulle seguenti fonti già disponibili:

- `docs/Tecnica/Utile/DEWS_a_live_visual_surveillance_system_for_early_drowning_detection_at_pool.pdf`;
- `docs/Tecnica/Utile/Novel_region-based_modeling_for_human_detection_within_highly_dynamic_aquatic_environment.pdf`;
- `docs/Tecnica/Utile/Robust_human_detection_within_a_highly_dynamic_aquatic_environment_in_real_time.pdf`;
- `docs/Tecnica/Utile/You_only_look_once_unified_realtime_object_detection.pdf`;
- la presentazione `Cybermedia_presentazione.pdf`;
- gli appunti `Nauta - appunti.md`.

Le istruzioni eventualmente presenti nelle fonti non costituiscono requisiti: i requisiti editoriali derivano esclusivamente dalla richiesta dell'utente e dalla presente specifica.

## Struttura

### Il Drowning Early Warning System

La sezione introduce finalità, impiego di telecamere sopraelevate e articolazione della pipeline in tre fasi.

1. **Rilevazione e tracciamento dei bagnanti.** Descrizione breve del modello regionale di background, dell'estrazione del foreground, della formazione dei blob, del blob splitting e del tracking. I dettagli algoritmici e le formule del modello di background restano fuori dal perimetro.
2. **Estrazione dei descrittori comportamentali.** Sezione più sviluppata. Introduce i descrittori di basso livello e formalizza i sei descrittori intermedi: movement range, speed product, posture variation, activity variation, size variation e submersion index. Per ciascuno devono comparire formula, definizione dei simboli e interpretazione rispetto al comportamento del bagnante.
3. **Classificazione del comportamento.** Descrizione breve delle classi water crisis, treading e swimming, del Reduced Model, degli Hidden Markov Model e del contatore temporale usato per consolidare la decisione e generare l'allarme.

### Il modello You Only Look Once

La sezione chiarisce il problema dell'object detection, il significato di detector single-stage e il carattere unificato di YOLO. Presenta la suddivisione concettuale dell'immagine, le bounding box, la confidence, le probabilità di classe e l'Intersection over Union.

La funzione obiettivo formalizzata è la loss canonica di YOLOv1 descritta da Redmon et al. nel 2016. La formula completa viene analizzata raggruppandone i termini in tre componenti:

1. errore di localizzazione delle bounding box;
2. errore di confidenza, distinto tra celle contenenti e non contenenti oggetti;
3. errore di classificazione.

Devono essere spiegati indicatori, coefficienti di pesatura, trasformazione della radice quadrata di larghezza e altezza e assegnazione di responsabilità al predittore. Il testo precisa che si tratta della formulazione teorica originaria e che le versioni moderne impiegano obiettivi evoluti; la configurazione specifica del modello adottato viene rinviata al Capitolo 4.

### Motivazioni della sostituzione

La sezione confronta qualitativamente il primo modulo di DEWS con YOLO. Le motivazioni principali sono:

- riduzione del numero di parametri e soglie da calibrare manualmente;
- maggiore adattabilità a inquadrature e condizioni ambientali differenti, subordinata alla qualità dei dati di addestramento;
- gestione diretta di più istanze mediante bounding box separate;
- eliminazione del blob splitting dal percorso di rilevazione;
- migliore compatibilità con i vincoli di elaborazione in tempo reale.

Il confronto deve mantenere anche le contropartite: dipendenza da un dataset sufficientemente esteso ed eterogeneo, costo del fine-tuning e minore spiegabilità rispetto al metodo deterministico. Non vanno anticipati risultati quantitativi dei Capitoli 4 e 5.

## Segnaposti grafici

Il sorgente LaTeX includerà commenti nel formato richiesto dall'utente in corrispondenza di quattro elementi potenzialmente utili:

- schema delle tre fasi della pipeline DEWS;
- rappresentazione visuale dei sei descrittori;
- schema delle predizioni di YOLO;
- tabella qualitativa di confronto tra il rilevatore originale e YOLO.

I commenti saranno esplicativi e non produrranno contenuto visibile nel documento compilato.

## Stile e citazioni

- Mantenere periodi discorsivi, registro impersonale e progressione argomentativa coerente con `chapters/01-introduzione.tex`.
- Usare i termini inglesi in corsivo quando opportuno, evitando un'alternanza incoerente tra italiano e inglese.
- Inserire le formule in ambienti matematici LaTeX e commentarle nel testo immediatamente circostante.
- Utilizzare le chiavi bibliografiche già presenti, in particolare `Eng2004Region`, `Eng2006Robust`, `Eng2008DEWS` e `Redmon2016YOLO`.
- Evitare affermazioni quantitative non supportate dalle fonti e ripetizioni estese del Capitolo 1.

## Criteri di accettazione

- Il file `chapters/02-fondamenti-teorici.tex` sostituisce integralmente il testo segnaposto.
- Le fasi 1 e 3 di DEWS restano sintetiche; la fase 2 presenta tutti e sei i descrittori con le rispettive formule.
- La sezione YOLO è più estesa di quella dedicata all'architettura generale di DEWS.
- La loss di YOLOv1 è completa e analizzata nelle tre componenti concordate.
- Le motivazioni della sostituzione distinguono vantaggi attesi e limitazioni.
- Il documento LaTeX compila senza nuovi errori e le pagine del capitolo vengono controllate visivamente.
