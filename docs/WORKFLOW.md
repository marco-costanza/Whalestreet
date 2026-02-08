# Workflow WhaleStreet: da Cursor a Vercel

Guida semplice al flusso che usi per aggiornare il sito: **modifiche in Cursor → Git → GitHub → Vercel**.

---

## Il flusso in 4 passi

```
1. MODIFICHE (Cursor)  →  2. COMMIT (salvataggio locale)  →  3. PUSH (GitHub)  →  4. VERCEL (sito online)
```

| Passo | Cosa succede | Dove lo fai |
|-------|----------------|-------------|
| **1. Modifiche** | Cambi testo, immagini, colori nella Homepage (`index.html`) o altri file | Cursor: chiedi all'AI o modifica a mano |
| **2. Commit** | Salvi una "fotografia" delle modifiche con una descrizione | Cursor: pannello Source Control (icona ramo) o terminale |
| **3. Push** | Invii i commit dal tuo computer a GitHub | Cursor: pulsante "Sync" o "Push" o "Publish Branch" in Source Control |
| **4. Vercel** | Vercel vede il nuovo codice su GitHub e aggiorna il sito | Automatico (nessun click) |

---

## Come ottimizzare il processo

### ✅ Fare spesso commit piccoli
- **Meglio:** un commit per ogni modifica logica (es. "Aggiorna testo hero", "Aggiungi link Twitter").
- **Evita:** un solo commit enorme con 10 modifiche diverse: se qualcosa va storto è più difficile tornare indietro.

### ✅ Scrivere sempre un messaggio di commit chiaro
- Esempi buoni: "Aggiungi logo WhaleStreet", "Correggi link contatti nel footer".
- Esempi da evitare: "fix", "update", "modifiche".

### ✅ Controllare prima di fare push
- Apri la Homepage (`index.html`) in Cursor e verifica che le modifiche siano quelle che volevi.
- Se usi l'anteprima del browser, ricarica la pagina per vedere le ultime modifiche.

### ✅ Un push = un deploy su Vercel
- Ogni volta che fai push su GitHub, Vercel ricostruisce e aggiorna il sito. Non serve fare nulla su Vercel.

---

## Come evitare errori

1. **Prima di modificare:** se stai per fare un cambiamento grosso, chiedi a Cursor di fare un commit dello stato attuale. Così hai un "punto di ripristino".
2. **Dopo le modifiche:** controlla che il sito in locale funzioni (apri la Homepage `index.html` nel browser).
3. **Prima del push:** leggi il messaggio di commit e assicurati che descriva bene cosa hai fatto.
4. **Se qualcosa va storto:** puoi tornare a un commit precedente (in Cursor puoi chiedere: "torna al commit dove avevo fatto X").

---

## Backup: i commit SONO i tuoi backup

- **Ogni commit** è una versione salvata del progetto.
- **GitHub** tiene una copia di tutti i commit che hai pushato: quindi hai il backup anche online.
- **Non serve** creare cartelle "backup" a mano: basta fare commit regolari con messaggi chiari.

---

## Dove cliccare in Cursor (riepilogo)

| Cosa vuoi fare | Dove andare |
|----------------|-------------|
| Vedere cosa è cambiato | **Source Control** (icona ramo nella barra laterale sinistra) |
| Fare commit | Source Control → scrivi messaggio nella casella in alto → pulsante **✓ Commit** |
| Inviare su GitHub | Source Control → pulsante **Sync Changes**, **Push** o **Publish Branch** |
| Vedere la cronologia dei commit | Source Control → **GRAPH** in alto o **...** → View History |

---

## Riferimenti rapidi

- **Guida ai commit (messaggi, esempi):** [COMMIT_GUIDE.md](COMMIT_GUIDE.md)
- **Registro delle modifiche del sito:** [../CHANGELOG.md](../CHANGELOG.md)
