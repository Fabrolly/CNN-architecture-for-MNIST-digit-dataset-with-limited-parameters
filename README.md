### Design of a CNN architecture for MNIST digit dataset with max 7,5k

ATTENZIONE: Questo README é una conversione automatica del file "relazione.pdf" che é formattato in modo migliore e contiene immagini di esempio! Leggi quello!

## Introduzione

Il progetto è stato realizzato su google ​ **colab** ​ in ​ **python** ​, servendosi delle librerie Keras,
**Keras_metrics** ​ (è già presente il comando pip per installarla) e ​ **Pandas** ​.

## Analisi del Dataset e Reshape dei dati

Il dataset, appena ​ **caricato** ​ tramite le funzioni dedicate di keras,
presenta la forma riportata a ​ **sinistra** ​.
Per la rete convoluzionale ho bisogno di una ​ **dimensione**
diversa da quella fornita, che rappresenta il canale colore della
mia immagine. Trattandosi di immagini in ​ **scala di grigi** ​, tale
dimensione è solamente 1.
Eseguo quindi il ​ **reshape dei dati** ​ come segue:
Le immagini appaiono come seguono:


## Definizione del modello e numero di parametri per layer

La definizione del modello, per
questa consegna, ​ **impone** ​ un
vincolo sul numero di ​ **parametri**
da utilizzare di massimo ​ **7500** ​.
Per avere performance migliori ho
cercato di avere un modello che
più si avvicinasse al numero
limite di parametri, ottenendo un
modello da ​ **7482 parametri** ​.
In particolare ci sono due livelli
**CONV2D** ​ di keras, aventi
rispettivamente le seguenti
caratteristiche:
● **9** ​ filtri con kernel size ​ **6**
● **7** ​ filtri con kernel size ​ **6**
Il ​ **MaxPooling2D** ​ è stato impostato per dimezzare la dimensione: ce ne sono presenti due,
quindi il dimezzamento è doppio. Ho provato ad usare ​ **AveragePooling2D** ​ ma le
performance sembravano essere leggermente ​ **peggiori** ​.
Successivamente, dopo il layer che si occupa del flattering dei dati, ci sono due livelli
**DENSE** ​ rispettivamente da ​ **47** ​ e ​ **32** ​ neuroni con funzione di attivazione ​ **RELU,** ​che
generalmente è quella che si comporta meglio.
Entrambi i suddetti sono seguiti da un livello che si occupa di fare il ​ **dropout** ​ dei dati per
aiutare a prevenire il fenomeno ​ **dell’overfitting** ​ (settati a 0,2)
La ​ **loss** ​ che ho scelto, trattandosi di dati categorizzati, è la ​ **categorical_crossentropy** ​.
**L’ottimizzatore** ​ che mi sembra aver dato performance più stabili anche in base
all’esperienza pregressa con i precedenti laboratori e assignment è ​ **ADAM** ​con learning rate
non specificato, ovvero lasciato come di default da keras a 0,001.


## Training del modello

#### Per la fase di training ho utilizzato un ​ early_stop ​ sulla ​ validation loss ​ con un valore di

patience pari a ​ **3** ​ per evitare overfitting.
Come limite ​ **massimo** ​ ho scelto di mettere ​ **50 epoche.**
Ho impostato uno ​ **split** ​ del ​ **20%** ​ per rappresentare il ​ **validation set** ​ a partire dai dati di
training. Il ​ **batch size** ​ è stato impostato a 200.
A seconda dell’esecuzione, la fase di fit ​ **si arresta automaticamente intorno all’epoca 40**
come mostrato della figura che segue

## Performance sui dati di training e di validation

**L’accuracy** ​ ottenuta nella fase di training sul ​ **validation set** ​ è del​ **98,24%** ​(a seconda

#### dell’esecuzione sono arrivato anche a picchi di circa ​ 98,50% ​).

Sul ​ **training** ​ ​ **set** ​ invece ​ **l’accuracy** ​ è intorno al ​ **97,8%.**
Si riportano come richiesto l’andamento dei valori di di ​ **accuracy** ​ e di ​ **loss** ​ sui dati di train e
di validation


## Predizione sul test set

Applico il modello a ​ **dati che il modello stesso non ha mai visto** ​ tramite l’istruzione sopra.
Per poter fare una veloce ​ **analisi visiva** ​ dei risultati ho stampato alcune delle immagini
contenute nel test set con sopra la dicitura “PRED: ​ **x** ​” dove ​ **x** ​ indica la classificazione
dell’immagine corrispettiva.
Da questa analisi, seppur molto approssimativa, le performance del ​ **modello sembrano
essere molto buone** ​ anche su numeri rappresentati in modo po’ ​ **strano** ​ come i seguenti:
Vediamo ora ​ **tramite le label del test set** ​ quanto effettivamente il nostro modello è
performante su dati che non ha mai visto


## Performance sul test set

L’accuracy sui dati di test è pari al ​ **98,57%** ​quindi leggermente superiore a quella ottenuta
sul validation test precedentemente.

### Errori sul test set

Riporto qui ​ **alcuni errori** ​ di predizione, a dimostrazione che alcuni numeri del dataset mnist
sono scritti in modo abbastanza approssimativo.
Anche un “umano” avrebbe potuto predire la seguente immagine come un 4 scritto male.
**Riporto altri tre esempi significativi in tal senso:**
_Nonostante gli errori è possibile notare come il modello sbagli comunque in modo
“ragionevole”_


Avviene però anche che con ​ **dati sporchi** ​ (vedi sulla sinistra del seguente esempio) il
modello predica il ​ **risultato corretto** ​ con per altro ​ **poca incertezza** ​:
_Riporto altri esempi generali direttamente dalla funzione presente anche nel source code._



