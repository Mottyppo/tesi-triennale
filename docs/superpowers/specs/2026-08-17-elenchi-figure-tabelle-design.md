# Voci sintetiche per gli elenchi di figure e tabelle

## Obiettivo

Rendere concise e uniformi le voci mostrate nell'Elenco delle figure e nell'Elenco delle tabelle per i capitoli 1 e 2, senza modificare i contenuti dei media o le didascalie estese visualizzate nel corpo della tesi.

## Soluzione LaTeX

Ogni ambiente `figure` o `table` interessato userà l'argomento opzionale di `\caption`:

```latex
\caption[Voce sintetica per l'elenco]{Didascalia completa visualizzata nel corpo}
```

Restano invariati:

- immagini, tabelle e relativi contenuti;
- didascalie estese nel corpo del documento;
- attribuzioni e citazioni delle fonti;
- etichette `\label` e numerazione;
- posizione degli ambienti e parametri di impaginazione.

## Voci approvate

### Capitolo 1

1. `Annegamenti in piscina per fascia d'età e sesso (2022--2026)`
2. `Annegamenti in piscina per fascia d'età e tipologia (2022--2026)`
3. `Manifestazioni osservabili dell'annegamento attivo`
4. `Confronto tra annegamento attivo e passivo`
5. `Perimetro dell'elaborato`

### Capitolo 2

1. `Fasi principali della \textit{pipeline} DEWS`
2. `Processo di \textit{blob splitting} in DEWS`
3. `Relazioni tra i descrittori comportamentali di DEWS`
4. `Modelli HMM per la classificazione del comportamento`
5. `Rappresentazione delle predizioni di YOLOv1`
6. `Architettura di YOLOv1`
7. `Confronto tra il rilevatore originale di DEWS e YOLO`

## Verifica

Dopo la modifica, il progetto dovrà essere compilato con il normale flusso LaTeX. La verifica comprenderà:

- assenza di errori e riferimenti non risolti;
- corrispondenza esatta delle dodici voci approvate negli elenchi;
- conservazione delle didascalie complete accanto ai media;
- assenza di variazioni ai contenuti delle figure e delle tabelle.
