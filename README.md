# wpfThreads

SVILUPPO AMBIENTE:
Microsoft .Net è una piattaforma di sviluppo sviluppata da Microsoft che mette a disposizione dell'utente funzionalità, come lo sviluppo di applicazioni e supporta più linguaggi di programmazione.
Questa piattaforma 
Nei 20 anni passati data la progressione di WPF ( libreria di classi del framework) si chiamava inizialmente framework, poi nacque .Netcore a cui successe .Net 2.0 dopo cui si sono fermati perché essendoci  la possibilità di confondersi con la vecchia versione sono passati da .Net 3.0 a .Net 5.0.
La versione di .Net 6.0 è stata dichiarata legacy (perché non viene più sviluppata e non funzionerebbe su sistemi operativi diversi da windows) mentre la 6.1 è ancora aperta a sviluppi.


OBIETTIVO:
Il programma realizzato prevede, attraverso istruzioni multithread, tre oggetti che visualizzano l’incremento di tre contatori con velocità diverse.

INTERFACCIA GRAFICA:
A livello grafico si definisce la struttura dell’interfaccia con del codice scritto in linguaggio Xaml. La prima cosa che si fa è scrivere il titolo del progetto e definire la visualizzazione dell'applicazione al centro della pagina:

CREAZIONE PROGETTO:
si inizia creando un nuovo progetto e selezionando  il linguaggio di programmazione, la piattaforma  e i dispositivi a cui è destinata.
dopo si passa al nome del progetto e a dove lo si salva.
A questo punto si sceglie la versione di .Net (6.1) con la quale si andrà a lavorare.

SCRITTURA CODE:
Prima di mettere il contenuto si definisce la divisione tra righe e colonne attraverso grid funzione con cui si definiscono le proprietà della griglia (posizione, spazio, colore ecc..). E possibile cambiare l’icona del progetto ( dato che è .ico). (dove c’è scritto windows) il codice presenta coppie nome - valore
è detto elemento (a livello sintattico). Quindi  per esempio Weight = sono attributi mentre
i tag sono definiti come elementi. window style none = finestra senza stile, che non visualizza i tasti per la chiusura e lo spegnimento se non con alt f4.

-eventi =cosa succede quando si clicca il bottone. 
il bottone viene configurato con la property click, attraverso button click, che si forma nel metodo ( nella parte di code-behind).
la message box viene sempre visualizzata in modalità modale su windows ossia che blocca tutta la GUI in attesa della risposta.
Usiamo WPF che non esiste per altre architetture diverse da windows, Maui sta cercando di sviluppare qualcosa di universale per tutte le architetture. L XML (Linguaggio tag based)  è stato introdotto da WPF ed ha una sintassi facile da imparare simile a Xamarin. 
Usiamo il dotnet 6 perchè il 7 è più soggetto a modifiche.
Nel caso di perdita del progetto tasto destro sulla soluzione e apri cartella in esplora file.
La consegna prevede il file zippato dell’intera cartella. 
 quando con tasto destro si lavora su quella riga si sta andando ad editare il progetto.
all’interno della cartella bin e obj  ci sono i file compilati.
Il pulsante compila il progetto permette una compilazione più veloce solo del progetto che si sta sviluppando e non di tutti i progetti presenti nella soluzione. 

COME SI PRESENTA L'AMBIENTE:
Sopra c’è un’anteprima che tende  a rimpicciolire la parte riservata al codice a livello di interfaccia. Essendo un linguaggio tag-based si sviluppa all'interno dei tag (es. <Grid>)
tutto ciò che è contenuto nei tag viene definito come attributo, con cui si definisce l’estetica e le funzionalità dell’applicazione.
  Tenere il file con il nome del progetto.
Quello che vogliamo è tenere il progetto compilato al centro dello schermo e per farlo si va di fianco  in proprietà e sulla chiave inglese (pulsante che fa vedere le proprietà di quello che seleziono).
  
  STRUTTURA ATTRIBUTI E TAG:
Di solito le proprietà sono divise per categorie.
Andando su center screen il file sta in mezzo al monitor. 
Basta che manchi la chiusura di un tag per commettere errori con lo Xaml e per non far funzionare più niente.
gli attributi si scrivono in chiave nome = valore:
  
  
  INTERFACCIA UTENTE:
Si inizia con una griglia di due righe modellando l’altezza e inserendo dei bottoni di cui si definisce la grandezza e la posizione e soprattutto l’orientamento nello stack panel corrispondente alla pulsantiera.
  A questo punto si definisce la griglia in cui saranno inseriti i pulsanti ossia oggetti di cui è possibile definire la dimensione e aspetti come il colore e le funzioni che possono eseguire se cliccati. Questi saranno due collocati alla riga 0 (Grid.Row=”0”) e avranno la funzione di:
-Il primo bottone (btnGo) sarà collegato nel code-behind ad un metodo attraverso un gestore di eventi e farà partire l’incremento dei tre contatori;
-ll secondo (btnClear) nel code-behind sarà utilizzato per azzerare i contatori,l’interfaccia grafica e la progressive bar.

sul bottone si fa button click e con object sender di collega al codice c# che definirà le funzioni dei pulsanti.
Lato c# si ha un costruttore che inizializza i componenti, questo lo fa dotnet per noi. 
  
Nella riga 1 della griglia saranno visualizzati i tre processi più quello che somma i loro valori e il loro incremento una volta avviata l’esecuzione. Essi sono definiti da oggetti TextBlock di cui si definiscono gli attributi ossia il nome, la grandezza del font. Sotto di essi sarà presente una progressive bar che mostra, in base al valore della somma dei dei tre contatori, a che punto del loro incremento ci si trova. Anche questa è definita da attributi come il nome e la sua grandezza specificata  solo in base all’altezza.

  
CODE-BEHIND:
Si tratta del codice che lavora dietro a ciò che si vede durante l’esecuzione che permette gli aggiornamenti della grafica che mostrano l’esecuzione dei processi.
L’esercizio consiste di creare un thread ( piccolo programma unità di codice autonomo che gira ma il suo lavoro è definito in uno spazio più preciso, mentre l’applicazione che sta girando possiamo definirla come un processo che al suo interno ad ogni interazione fa partire un thread).
Il problema è che in thread avente la propria autonomia non può parlare con un altro thread in modo diretto modificando da fuori il valore delle variabili dato che ci potrebbe essere un problema di concorrenza motivo per cui si usa uno specifico metodo che permette tale azione.

Ma quando si incrementa il metodo il for fa 1000 giri incrementando la variabile il risultato all’esecuzione l’output continuerà ad incrementarsi del valore presente nel for (quello al centro). Se si aggiorna la grafica per l'utente risulta pesante quindi data la velocità con cui si incrementa _counter aspetta che finisce e si aggiorna però in questo modo, aggiornando di fatto la grafica di continuo.  il codice così scritto ci mette molto più tempo per elaborare e quando finisce il proprio giro (ci mette un po ') fermando il thread ad ogni giro. Quello che succede  è che nell’interfaccia grafica è che fino alla fine della sua esecuzione il processo non da output dato che è bloccante (Thread.Sleep()) quidni si congelano i controlli sulle modifiche grafiche e di codice, un applicazione scritta in questo modo lagga e la macchina non ascolta nessuno. Quindi blocca l'esecuzione ad ogni iterazione del codice creando un processo lento che blocca l’interfaccia completamente. Quello che dobbiamo fare è lanciare un thread separato dandogli una velocità, ma lasciando il thread dell’interfaccia grafica libera in modo tale che possa gestire gli eventi.
il sistema a questo punto da un errore in cui il thread secondario è andato in conflitto con il thread primario perché essi non possono usare le stesse risorse, serve perciò un “lasciapassare. 
  
Dispatcher.invoke e Lambda expression:
 Con il metodo Dispatcher.invoke è possibile eseguire il thread del codice che riesce a passare ad ogni iterazione a scrivere e poi lasciare il thread dell’interfaccia grafica aggiornarsi ad ogni scrittura, in questo modo è possibile vedere l’incremento di GIRI.
() =>  questa è una lambda che serve per passare un pezzo di codice e invoca (chiama ad esecuzione)  il thread che vogliamo eseguire facendogli fare quello che dovrebbe fare quindi permettendogli di modificare counter e la label.
Dispatcher.invoke è utilizzato quindi per l’aggiornamento dei contatori. Esso contiene un parametro e una parte detta Lambda expression che divide il blocco    ,aspetta il suo turno e invoca il codice contenuto. 
  
Ad ogni click del pulsante viene lanciato un nuovo thread e tutti i thread lavoreranno sulla stessa variabile. I thread  infatti hanno degli stati con cui si può controllare la loro esecuzione. Creando due thread (si inizializzano) che si incrementano si vedrà che vanno uno più veloce dell'altro dal momento che lavorando sulla stessa variabile. 
  
Avendo due contatori, però, si dovrebbero incrementare a 2000, ma c’è qualcosa che non torna dato che mancano dei conteggi. I processi prendono la variabile counter che viene incrementata, ma la concorrenza dei thread sulla variabile la porta ad essere già incrementata. 
  quindi è necessario bloccare l’incremento di counter con lock  che richiede un oggetto da bloccare.
Il risultato del conteggio in questo momento infatti mostra i due contatori con valori diversi in quanto il primo arriva alla cifra stabilita mentre il secondo si ferma prima. La differenza tra essi è la velocità, ma questa insieme alla quantità non è la ragione per cui non raggiungono entrambe la somma pattuita.
La funzione counter due ad una certa non aggiorna più la sua label nell’interfaccia grafica, l’ideale sarebbe avere un meccanismo che aggiorna entrambi le label alla fine del loro incremento, quindi alla fine dei processi.

  
SEMAFORI:
I semafori sono dei costrutti messi a disposizione del cuore del sistema operativo (kernel) che vengono messe a disposizione e bloccano tutto, interrompono ogni altro processo. questi costrutti sono i lock che hanno dei contatori da 0 che non può essere negativo. Signal: decremento contatore, Wait: si aspetta che il contatore diventi 0. quindi si procederà creando il semaforo costruendo una procedura bloccante.

Si dichiara quindi il semaforo in cui si specifica il valore da cui parte dichiarando nel main e impostando il valore di base nel metodo Button-Click. subito dopo si blocca il semaforo con la funzione di Wait(). 
Il Signal sarà dato alla fine delle funzioni di incremento.
Per testare la fine del lavoro con una message box si visualizza un messaggio di fine. 
L'esecuzione porta al blocco dell’interfaccia perchè il wait usato nel main windows rende una procedura che dovrebbe durare il meno possibile bloccata. 
siamo quindi obbligati alla creazione di un terzo thread per cui ci sarà bisogno di un metodo,  
in cui si attende (metodo attendi) il thread 3 esegue quindi il wait ma permetterà l’esecuzione delle funzioni di windows.
Dispatcher.invoke sarà utilizzato anche in questo caso per l’aggiornamento dei contatori. Esso contiene un parametro e una parte detta Lambda expression che divide il blocco con   () =>, aspetta il suo turno e invoca il codice contenuto.
  
Quando clicco il bottone di nuovo la seconda volta che si entra il semaforo è totalmente decrementato, quindi sparisce. Una soluzione è bloccare il pulsante fino alla fine dell’esecuzione.
Creiamo un pulsante che una volta creato è spento momentaneamente dopo il primo click che fa partire i thread contatori. con un semaforo dichiarato in locale  con un contatore da due eventi.
Il thread 3 ha una lambda expression ossia una funzione che aspetta che il semaforo sia a 0. 
a quel punto si può cliccare di nuovo  il pulsante. Il decremento del semaforo parte e si risettano i contatori.

Quindi per la scrittura dei metodi dietro ai tre bottoni creati per permettere la visualizzazione e gli incrementi tolai dei valori deti thread il codide sarà strutturato in questo modo :
-si definiscono innanzitutto i valori massimi raggiungibili,i tempi a cui i contatori si dovranno incrementare e i contatori stessi a 0:
-A questo punto si inizializza un costrutto lock, un costrutto primitivo che gestisce l’accesso alla risorsa garantendo la mutua esclusione e quindi l’utilizzo della risorsa da parte di un solo thread ( piccolo segmento di codice indipendente, processo leggero) e il semaforo che permetterà l’incremento dei tre processi uno dopo l’altro nei relativi tempi impostati.
-Adesso si definisce nel code-behind legato al primo pulsante il blocco momentaneo del pulsante che fa partire i processi (che in caso contrario andrebbero ad intralciarsi nel caos in cui venisse cliccato nuovamente il bottone), il valore massimo della progressive bar costituito dalla somma dei GiRI.
-si dichiarano e inizializzano quindi i thread:
  i primi tre saranno quelli che si incrementano durante l’esecuzione attraverso dei metodi definiti sotto;
  il quarto accompagnato da un  Dispatcher.invoke ( metodo con cui è  possibile eseguire il thread del codice che riesce a passare ad ogni iterazione a scrivere e poi   lasciare il thread dell’interfaccia grafica aggiornarsi ad ogni scrittura, in questo modo è possibile vedere l’incremento di GIRI) e una lambda expression come         parametro. In questo metodo si aggiorna l’interfaccia grafica.
  si inizializza il semaforo.

