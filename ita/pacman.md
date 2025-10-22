# Pacman 
pacman gestisce l'installazione, l'aggiornamento e la rimozione dei pacchetti software. Le operazioni principali sono richiamate tramite "flag" (lettere precedute da un trattino, es. -S, -R, -Q).

Nota Importante: **Quasi tutte le operazioni che modificano il sistema (installare, rimuovere, aggiornare) richiedono i permessi di root. Usa sudo prima di ogni comando.**

## Sincronizzazione e Aggiornamento
Il flag principale per la sincronizzazione (download/installazione/aggiornamento) è -S.

### Aggiornare tutti i pacchetti (Operazione Standard)
Questo è il comando che userai più spesso. Aggiorna le liste dei pacchetti dai repository (y) e poi aggiorna (upgrade) tutti i pacchetti obsoleti sul tuo sistema (u).

```
sudo pacman -Syu
-S: Sincronizza.

-y: Aggiorna (Refresh) le liste dei pacchetti locali.

-u: Aggiorna (Upgrade) i pacchetti installati.
```

Se sospetti che le tue liste locali siano corrotte o non sincronizzate, puoi forzare un doppio refresh `sudo pacman -Syyu`

### Aggiornare un Singolo Pacchetto
Per aggiornare un singolo pacchetto alla versione presente nei repository (se più recente), si usa lo stesso comando dell'installazione:

```sudo pacman -S <nome_pacchetto>```

**ATTENZIONE**: Su Arch Linux, che è una distribuzione rolling release, è fortemente sconsigliato aggiornare un singolo pacchetto (pacman -S <nome>) senza aggiornare il resto del sistema (pacman -Syu). Farlo può portare a "partial upgrades" (aggiornamenti parziali), dove le librerie e i programmi hanno versioni non compatibili tra loro, causando la rottura del sistema.

## Installazione e Ricerca Pacchetti
Per installare un nuovo pacchetto (o più pacchetti contemporaneamente):

```sudo pacman -S <nome_pacchetto1> <nome_pacchetto2>```

Cercare Pacchetti
Cercare nei Repository (Remoto)
Se non conosci il nome esatto, puoi cercare nei repository remoti usando -Ss:

`pacman -Ss <parola_chiave>`

Esempio: `pacman -Ss browser` cercherà tutti i pacchetti che contengono "browser" nel nome o nella descrizione.

Cercare tra i Pacchetti Installati (Locale)
Per cercare solo tra i pacchetti che hai già installato sul tuo sistema, usa `-Qs`:

`pacman -Qs <parola_chiave>`

Ottenere Informazioni Dettagliate
Per vedere tutti i dettagli di un pacchetto (versione, dipendenze, descrizione, ecc.):

### Informazioni su un pacchetto nei repository (remoto)
`pacman -Si <nome_pacchetto>`

### Informazioni su un pacchetto già installato (locale)
`pacman -Qi <nome_pacchetto>`


## Rimozione Pacchetti e Pulizia del Sistema
Il flag principale per la rimozione (Remove) è `-R`.

Rimuovere Pacchetti
Rimozione semplice (sconsigliata): Rimuove solo il pacchetto, ma lascia le sue dipendenze.

`sudo pacman -R <nome_pacchetto>`

Rimozione ricorsiva (consigliata): Rimuove il pacchetto e tutte le sue dipendenze, purché non siano usate da altri pacchetti.

`sudo pacman -Rs <nome_pacchetto>`

Rimozione completa (aggressiva): Rimuove il pacchetto, le dipendenze (s) e anche i file di configurazione di sistema (n).

`sudo pacman -Rsn <nome_pacchetto>`

### Pulire le Dipendenze Orfane
Questa è l'operazione di pulizia più importante. I pacchetti "orfani" sono dipendenze che sono state installate automaticamente per un altro programma, ma che ora (magari dopo una rimozione) non sono più richieste da nessun pacchetto installato. Occupano solo spazio.

Per rimuovere tutti i pacchetti orfani in un colpo solo:

`sudo pacman -Rns $(pacman -Qdtq)`

Spiegazione del comando interno:

`pacman -Q` (Query): Interroga il database locale.

`d`: Filtra per "dipendenze" (installate come dipendenza).

`t`: Filtra per "orfani" (non più richiesti).

`q`: "Quiet mode", stampa solo i nomi dei pacchetti, nient'altro.

### Pulire la Cache dei Pacchetti
pacman conserva una copia di ogni pacchetto installato o aggiornato nella cache (di solito in `/var/cache/pacman/pkg/`). Questo è utile per i downgrade, ma può occupare molto spazio.

**Pulizia sicura (consigliata)**: Rimuove solo le versioni dei pacchetti che non sono più installate (es. versioni vecchie).

`sudo pacman -Sc`

**Pulizia aggressiva**: Rimuove tutti i pacchetti dalla cache, anche quelli attualmente installati. Libererai molto spazio, ma se dovessi reinstallare un pacchetto, pacman dovrà riscaricarlo.

`sudo pacman -Scc`