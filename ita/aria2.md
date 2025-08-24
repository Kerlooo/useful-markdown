# aria2 
aria2 è un gestore di download versatile e leggero per la riga di comando. Supporta protocolli come HTTP/HTTPS, FTP, SFTP, BitTorrent e Metalink. È noto per la sua capacità di riprendere i download interrotti e di accelerarli utilizzando più connessioni contemporanee.

## Installazione
Per installare aria2, usa il gestore di pacchetti del tuo sistema operativo.

### Arch Linux
Come utente di Arch Linux, puoi installarlo facilmente tramite Pacman:

```bash
sudo pacman -S aria2
```

### Debian / Ubuntu
```bash 
sudo apt-get update
sudo apt-get install aria
```
### Fedora
```bash
sudo dnf install aria2
```

### macOS
Con Homebrew:
```bash
brew install aria2
```

### Windows
aria2 può essere installato tramite Chocolatey o Scoop, oppure scaricando l'eseguibile dal sito ufficiale.

## Download semplice
Per scaricare un file da un URL:
```bash
aria2c "https://esempio.com/file.zip"
```
Download da un file di testo
Puoi scaricare più file elencati in un file di testo (uno per riga) con l'opzione -i:
```bash
aria2c -i elenco_file.txt
```
Funzionalità avanzate
Riprendere un download interrotto
Una delle funzioni più utili di aria2 è la ripresa dei download. Usa l'opzione -c (o --continue).
```bash
aria2c -c "https://esempio.com/file_grande.iso"
```
**Questo è particolarmente utile su connessioni instabili.**

Download multi-connessione
Per accelerare il download, aria2 può usare più connessioni contemporaneamente. L'opzione -x (o --max-concurrent-downloads) specifica il numero di connessioni per server.
```bash
aria2c -x 5 "https://esempio.com/file_grande.zip"
```
**Un valore tra 4 e 8 è solitamente un buon punto di partenza.**

Download da più fonti
Puoi scaricare lo stesso file da più URL contemporaneamente. aria2 combina i dati scaricati da tutte le fonti.
```bash
aria2c "http://fonte1.com/file.rar" "http://fonte2.com/file.rar"
```
Limitare la velocità di download
Per evitare di saturare la tua connessione, puoi impostare un limite di velocità in byte/secondo con l'opzione `--max-download-limit`.
```bash
aria2c --max-download-limit=1M "http://esempio.com/download.zip"
```
**(In questo esempio, il limite è 1 Megabyte al secondo).**

### Download di un file .torrent
```bash
aria2c "percorso/al/file.torrent"
```
### Download di un magnet link
```bash
aria2c "magnet:?xt=urn:btih:..."
```