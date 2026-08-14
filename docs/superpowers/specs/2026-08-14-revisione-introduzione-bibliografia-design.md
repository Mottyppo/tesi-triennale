# Revisione conservativa dell'introduzione e della bibliografia

## Obiettivo

Correggere il Capitolo 1 della tesi e completare la bibliografia utilizzando le fonti locali presenti in `docs/`, mantenendo invariati struttura, tono e impostazione generale del testo.

## Perimetro

- sostituire la voce bibliografica fittizia attualmente presente con una voce BibLaTeX per ciascuno dei 21 file contenuti in `docs/`;
- identificare per ogni fonte autore o ente, titolo, anno e dati editoriali disponibili, distinguendo articoli, atti di conferenza, rapporti, norme, risorse online e materiale audiovisivo;
- mantenere chiavi bibliografiche leggibili e stabili e correggere tutte le chiavi già richiamate dal Capitolo 1;
- associare le citazioni alle sole affermazioni effettivamente sostenute dalle rispettive fonti;
- lasciare in bibliografia anche le fonti non richiamate nel Capitolo 1, coerentemente con l'attuale `\nocite{*}`;
- modificare il testo solo in presenza di errori fattuali, supporto bibliografico insufficiente o formulazioni ambigue/problematiche;
- non modificare indice, struttura dei capitoli, contenuti degli altri capitoli o impostazione grafica generale.

## Criteri editoriali

La revisione sarà conservativa. Non verranno riscritti paragrafi corretti per preferenze stilistiche. In particolare, verrà corretta l'identificazione della fonte OMS: il file locale è la scheda informativa *Drowning* del 1° maggio 2026, non il *Global Status Report on Drowning Prevention 2024*. Le statistiche e le descrizioni tecniche saranno mantenute soltanto quando risultano coerenti con le fonti citate.

Per i documenti normativi verranno registrati gli estremi del documento senza attribuire alla tesi una conformità o certificazione non dimostrata. Per i PDF ottenuti da scansioni verranno ricavati i dati bibliografici dal frontespizio e dal contenuto visibile, integrandoli con metadati autorevoli quando necessario.

## Verifica

Al termine dell'intervento verranno eseguiti:

1. un controllo automatico della corrispondenza tra file locali e voci bibliografiche;
2. una ricerca delle chiavi citate ma non definite e delle voci duplicate;
3. la compilazione completa LaTeX/Biber;
4. il controllo dei log per citazioni o riferimenti irrisolti;
5. il rendering e l'ispezione visiva delle pagine aggiornate del Capitolo 1 e della bibliografia.

## Criteri di completamento

Il lavoro è concluso quando tutti i 21 file in `docs/` hanno una voce bibliografica, il Capitolo 1 non contiene citazioni irrisolte o affermazioni incompatibili con le fonti consultate e il documento viene compilato senza errori bibliografici.
