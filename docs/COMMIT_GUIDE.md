# Guida ai commit — Cos'è e come si fa

Per qualcuno che non programma, "commit" può sembrare un termine tecnico. In pratica è **il modo in cui salvi e descrivi un insieme di modifiche** al progetto, in modo che tu (e Git) possiate sempre capire cosa è stato fatto e quando.

---

## Cos'è un commit?

- Un **commit** è come un **salvataggio con nome e data**: una "fotografia" del progetto in un certo momento, con una breve descrizione (messaggio di commit).
- **Non** invia ancora nulla su internet: le modifiche restano sul tuo computer finché non fai **Push**.
- **Sì** è il tuo "backup" locale e, dopo il push, anche su GitHub.

Quindi: **modifichi i file → fai commit (salvi con descrizione) → fai push (invii su GitHub) → Vercel aggiorna il sito.**

---

## Dove cliccare in Cursor

### 1. Aprire il pannello Source Control
- **Barra laterale sinistra:** clicca sull'icona che sembra un **ramo** (branch) o due cerchi collegati.
- Oppure: **View → Source Control** dal menu in alto.
- Oppure: **Ctrl+Shift+G** (Windows/Linux) o **Cmd+Shift+G** (Mac).

### 2. Vedere le modifiche
- Nella lista **Changes** vedi i file modificati (es. `index.html`).
- Cliccando su un file si apre il confronto (prima / dopo).

### 3. Fare il commit
- In alto nel pannello Source Control c'è una **casella di testo** ("Message"): è lì che scrivi il **messaggio di commit**.
- Scrivi una frase chiara (es. "Aggiungi logo WhaleStreet al sito").
- Poi clicca il pulsante **✓ Commit** (o **Commit** con icona check) accanto alla casella.
- Su Mac: **⌘⏎** (Cmd+Invio) per fare commit.

### 4. Inviare su GitHub (Push)
- Dopo il commit vedrai **Publish Branch** o **Sync Changes** o **Push** (pulsante con nuvola/freccia).
- Clicca per inviare i commit su GitHub. Da lì Vercel aggiornerà il sito.

---

## Come scrivere un buon messaggio di commit

### Regola breve
**Una riga che descrive COSA hai fatto (e eventualmente PERCHÉ), in italiano, all'indicativo.**

### Esempi buoni
- `Aggiungi logo WhaleStreet al sito`
- `Aggiorna testo hero con nuovo slogan`
- `Correggi link Twitter nel team`
- `Aggiungi sezione contatti`

### Esempi da evitare
- `fix` (troppo vago)
- `update` (non si capisce cosa)
- `modifiche` (non descrive nulla)
- Messaggi lunghissimi in una sola riga (meglio una frase breve).

---

## Checklist prima di ogni commit

- [ ] Le modifiche che vedi in **Changes** sono quelle che volevi?
- [ ] Hai scritto un messaggio di commit che descrive bene cosa hai fatto?
- [ ] Se è una modifica grossa, hai controllato il sito in locale (apri la Homepage `index.html` nel browser)?

Dopo il commit puoi fare **Push** / **Publish Branch** per aggiornare GitHub e quindi Vercel.

---

## Riepilogo: sequenza consigliata

1. Modifichi i file (con Cursor o chiedendo all'AI).
2. Apri **Source Control** (icona ramo).
3. Controlli la lista **Changes**.
4. Scrivi il **messaggio di commit** nella casella in alto.
5. Clicchi **Commit** (o ⌘⏎).
6. Clicchi **Publish Branch** / **Sync Changes** / **Push**.
7. Vercel aggiorna il sito da solo.

Per maggiori dettagli sul flusso completo: [WORKFLOW.md](WORKFLOW.md).
