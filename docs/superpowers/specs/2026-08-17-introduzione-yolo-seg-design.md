# Introduzione di YOLO per la segmentazione

## Obiettivo

Chiarire nel capitolo 2 che YOLOv1 è presentato come fondamento teorico della famiglia, mentre il progetto adotta una variante di YOLO per la segmentazione di istanza.

## Modifica testuale

Subito prima della sottosezione dedicata alla rappresentazione delle predizioni di YOLOv1 sarà inserito un breve paragrafo di raccordo. Il testo specificherà che la variante adottata associa a ciascun bagnante una maschera di segmentazione, oltre alla localizzazione dell'istanza, e che tale rappresentazione è più adatta alla pipeline DEWS perché conserva la sagoma necessaria al calcolo dei descrittori comportamentali.

La formulazione non affermerà che la variante di segmentazione elimina tecnicamente le bounding box. Non sarà creata una nuova sottosezione e la trattazione di YOLOv1 resterà invariata.

## Impaginazione

La tabella 2.1 non sarà modificata durante il primo intervento. Dopo l'inserimento del testo la tesi sarà ricompilata per verificare se il nuovo flusso risolve autonomamente la pagina occupata dalla sola tabella; soltanto in caso contrario sarà progettato un intervento specifico sulla tabella.
