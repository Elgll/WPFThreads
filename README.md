# wpfThreads

OBIETTIVO:
Il programma realizzato prevede, attraverso istruzioni multithread, tre oggetti che visualizzano l’incremento di tre contatori con velocità diverse.

INTERFACCIA GRAFICA:
A livello grafico si definisce la struttura dell’interfaccia con del codice scritto in linguaggio Xaml. La prima cosa che si fa è scrivere il titolo del progetto e definire la visualizzazione dell'applicazione al centro della pagina:



A questo punto si definisce la griglia in cui saranno inseriti i pulsanti ossia oggetti di cui è possibile definire la dimensione e aspetti come il colore e le funzioni che possono eseguire se cliccati. Questi saranno due collocati alla riga 0 (Grid.Row=”0”) e avranno la funzione di:
-Il primo bottone (btnGo) sarà collegato nel code-behind ad un metodo attraverso un gestore di eventi e farà partire l’incremento dei tre contatori;
-ll secondo (btnClear) nel code-behind sarà utilizzato per azzerare i contatori,l’interfaccia grafica e la progressive bar.


Nella riga 1 della griglia saranno visualizzati i tre processi più quello che somma i loro valori e il loro incremento una volta avviata l’esecuzione. Essi sono definiti da oggetti TextBlock di cui si definiscono gli attributi ossia il nome, la grandezza del font. Sotto di essi sarà presente una progressive bar che mostra, in base al valore della somma dei dei tre contatori, a che punto del loro incremento ci si trova. Anche questa è definita da attributi come il nome e la sua grandezza specificata  solo in base all’altezza.











CODE-BEHIND:
Si tratta del codice che lavora dietro a ciò che si vede durante l’esecuzione che permette gli aggiornamenti della grafica che mostrano l’esecuzione dei processi.

Si definiscono innanzitutto i valori massimi raggiungibili,i tempi a cui i contatori si dovranno incrementare e i contatori stessi a 0:




A questo punto si inizializza un costrutto lock, un costrutto primitivo che gestisce l’accesso alla risorsa garantendo la mutua esclusione e quindi l’utilizzo della risorsa da parte di un solo thread ( piccolo segmento di codice indipendente, processo leggero) e il semaforo che permetterà l’incremento dei tre processi uno dopo l’altro nei relativi tempi impostati.



Adesso si definisce nel code-behind legato al primo pulsante il blocco momentaneo del pulsante che fa partire i processi (che in caso contrario andrebbero ad intralciarsi nel caos in cui venisse cliccato nuovamente il bottone), il valore massimo della progressive bar costituito dalla somma dei GiRI.



Si dichiarano e inizializzano quindi i thread:
-i primi tre saranno quelli che si incrementano durante l’esecuzione attraverso dei metodi definiti sotto;



-il quarto accompagnato da un  Dispatcher.invoke ( metodo con cui è  possibile eseguire il thread del codice che riesce a passare ad ogni iterazione a scrivere e poi lasciare il thread dell’interfaccia grafica aggiornarsi ad ogni scrittura, in questo modo è possibile vedere l’incremento di GIRI) e una lambda expression come parametro. In questo metodo si aggiorna l’interfaccia grafica:



E si inizializza il semaforo.

