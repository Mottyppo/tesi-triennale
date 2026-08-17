# Impaginazione compatta della tabella 2.1

## Obiettivo

Ridurre il peso visivo e l'altezza della tabella 2.1, mantenendo inalterata l'impaginazione delle figure 2.5 e 2.6.

## Modifica

La tabella conserverà la larghezza `\textwidth`, le tre colonne, i contenuti, la didascalia e il posizionamento `[htbp]`. Il corpo sarà ridotto da `\small` a `\footnotesize` e il fattore di spaziatura verticale `\arraystretch` passerà da `1.15` a `1.05`.

Non saranno modificate le larghezze delle colonne né sarà forzata la posizione della tabella. In questo modo la riduzione rimane moderata e coerente con la tipografia del documento.

## Verifica

La tesi sarà ricompilata e saranno controllate visivamente la pagina della tabella e le pagine delle due figure YOLO. La tabella dovrà lasciare più spazio al testo circostante senza risultare troppo densa; le figure dovranno mantenere la collocazione attuale.
