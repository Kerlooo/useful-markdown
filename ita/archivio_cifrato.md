# Archivio 7z cifrato su Arch Linux  
**Guida per creare, modificare e gestire un archivio protetto da password con `7z`.**  

---

## 📦 Installazione di `p7zip`  
Su Arch Linux, installa il pacchetto:  
```bash
sudo pacman -S p7zip
```

---

## 🔐 Creare un nuovo archivio cifrato  
```bash
7z a -p -mhe=on archivio_privato.7z ~/cartella_o_file_da_criptare
```
- **`a`**: Aggiungi file all'archivio.  
- **`-p`**: Richiede una password (inserirla al prompt).  
- **`-mhe=on`**: Cifra anche i nomi dei file (**obbligatorio per la privacy**).  
- **`archivio_privato.7z`**: Nome dell'archivio.  

### Esempio:  
```bash
7z a -p -mhe=on backup_segreto.7z ~/Documenti/private
```

---

## ➕ Aggiungere file a un archivio esistente  
```bash
7z u -p -mhe=on archivio_privato.7z ~/nuovo_file
```
- **`u`** (update): Aggiorna l'archivio aggiungendo/modificando file.  

### Esempio:  
```bash
7z u -p -mhe=on backup_segreto.7z ~/Scaricati/confidenziale.pdf
```

---

## 📂 Estrazione dei file  
```bash
7z x -p archivio_privato.7z
```
- **`x`**: Estrai file mantenendo la struttura delle cartelle.  

---

## 🛠️ Altre operazioni utili  

### 🔍 Listare i file nell'archivio (senza estrarre)  
```bash
7z l -p archivio_privato.7z
```

### ❌ Eliminare un file dall'archivio  
```bash
7z d -p archivio_privato.7z file_da_rimuovere.txt
```

### ✅ Verificare l'integrità dell'archivio  
```bash
7z t archivio_privato.7z
```

---

## ⚠️ Note importanti  
1. **`-mhe=on`** è essenziale per cifrare i nomi dei file (senza, sono visibili senza password!).  
2. **Non perdere la password**: Senza di essa, i dati saranno irrecuperabili.  
3. Per archivi molto grandi, puoi disattivare la compressione per velocizzare:  
   ```bash
   7z a -p -mhe=on -mx=0 archivio_veloce.7z ~/dati_grandi
   ```
   - **`-mx=0`**: Compressione disabilitata.  

---

## 🔄 Automatizzare con uno script (opzionale)  
Crea un file `backup_privato.sh`:  
```bash
#!/bin/bash  
7z u -p -mhe=on ~/backup_segreto.7z ~/cartella_privata/  
```
Rendilo eseguibile:  
```bash
chmod +x backup_privato.sh
```
Esegui lo script quando necessario:  
```bash
./backup_privato.sh
```

---

✅ **Vantaggi**:  
- Portabile (apribile con 7-Zip su Windows/macOS).  
- Sicurezza AES-256.  
- Facile da aggiornare con nuovi file.  

📁 **Alternativa avanzata**: Per una cartella sempre sincronizzata e cifrata, considera `gocryptfs` o `encfs` ([vedi guida completa](#)).  
```

### Come usare questo file?  
1. Salvarlo come `guida_7z.md`.  
2. Visualizzarlo con:  
   ```bash
   glow guida_7z.md  # (se usi Glow, pacchetto markdown viewer)
   ```
   oppure  
   ```bash
   cat guida_7z.md
   ```