# Illustrazione delle manifestazioni osservabili dell'annegamento attivo

## Obiettivo

Creare un'illustrazione originale e priva di vincoli di licenza che sintetizzi visivamente gli indicatori dell'annegamento attivo descritti nella Sezione 1.1.1 della tesi.

## Contenuto visivo

La scena mostrerà un unico soggetto adulto generico, visto lateralmente in una sezione della piscina. La linea dell'acqua sarà chiaramente visibile e dividerà la porzione emersa da quella sommersa.

Il soggetto presenterà:

- corpo in posizione prevalentemente verticale;
- testa reclinata all'indietro;
- bocca appena al di sopra della superficie;
- braccia aperte lateralmente e orientate verso il basso, come nel tentativo di spingere l'acqua;
- gambe piegate o sospese, senza una chiara azione propulsiva;
- assenza di gesti volontari di richiamo.

## Stile e composizione

- stile: illustrazione scientifica vettoriale pulita, simile a una figura di manuale didattico;
- formato: orizzontale, rapporto 3:2;
- palette: azzurri e blu sobri per l'acqua, incarnato e abbigliamento neutri;
- sfondo: essenziale, senza dettagli decorativi o persone aggiuntive;
- inquadratura: figura intera, centrata, con spazio sufficiente attorno agli arti;
- testo: nessuna scritta, etichetta, freccia, logo o filigrana;
- tono: clinico e informativo, non drammatico né fotorealistico.

## Vincoli di accuratezza

L'immagine non deve rappresentare una normale nuotata, una richiesta di aiuto volontaria o una persona che agita entrambe le mani sopra la testa. La postura deve comunicare una risposta istintiva finalizzata soprattutto a mantenere le vie respiratorie sopra la superficie.

La scena non deve contenere ferite, elementi macabri, soccorritori, attrezzature di salvataggio o testo incorporato.

## Asset e integrazione

L'immagine finale sarà salvata in:

`figures/manifestazioni-annegamento-attivo.png`

Il commento segnaposto in `chapters/01-introduzione.tex` sarà sostituito da una figura LaTeX con:

- ambiente `figure` e posizionamento `[htbp]`;
- larghezza massima indicativa `0.72\textwidth`;
- didascalia: “Rappresentazione schematica delle principali manifestazioni osservabili dell'annegamento attivo.”;
- etichetta: `fig:manifestazioni-annegamento-attivo`.

## Verifica

Prima dell'integrazione saranno controllati postura, anatomia, assenza di testo e coerenza con gli indicatori descritti. Dopo l'inserimento sarà compilato il progetto e verrà verificata visivamente la pagina interessata per escludere tagli, sovrapposizioni o spostamenti problematici del contenuto.
