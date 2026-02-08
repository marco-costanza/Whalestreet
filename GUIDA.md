# Landing Page – Solo contenuto (guida completa)

Guida per ottenere da una pagina WordPress (sorgente salvata da Chrome) **solo il codice della singola pagina**: niente header, niente menu, niente footer, niente barra admin. Include accordion fluido, layout a schermo intero e ottimizzazioni.

*(Stesso contenuto della skill Cursor: `~/.cursor/skills/landing-page-solo-contenuto/SKILL.md`)*

---

## Skill Cursor Webmaster (ecosistema)

Per diventare un webmaster PRO, usa queste skill insieme:

| Skill | Quando usarla |
|-------|---------------|
| **@landing-page-solo-contenuto** | Estrarre contenuto da pagine WordPress esistenti, togliere header/footer |
| **@webmaster-css-modern** | Layout responsive, Grid/Flexbox, animazioni, ottimizzazioni CSS |
| **@webmaster-html-accessibility** | HTML semantico, accessibilità WCAG/ARIA, SEO |
| **@landing-page-creator** | Creare landing page da zero, struttura conversion-focused, CTA |

Esempio: per creare una landing page da zero → `@landing-page-creator` + `@webmaster-css-modern` + `@webmaster-html-accessibility`. Per ripulire un export WordPress → `@landing-page-solo-contenuto`.

---

## 1. Cosa NON deve essere incluso (da rimuovere)

### 1.1 Barra admin WordPress
- **Selettore / markup:** `<div id="wpadminbar" class="nojq nojs">` … fino alla chiusura `</div>` corrispondente.
- **CSS da rimuovere/evitare:**  
  - Link: `id="admin-bar-css"` (admin-bar.min.css).  
  - Blocco `<style id="admin-bar-inline-css">` che contiene `html { margin-top: 32px !important; }` e `#wpadminbar`.
- **Motivo:** La pagina "solo contenuto" non mostra la barra admin; lasciarla appesantisce e crea spazio inutile in alto.

### 1.2 Header e menu (Astra / tema)
- **Selettore:** `<header class="site-header" … id="masthead"` fino a `</header><!-- #masthead -->`.
- **Contiene tipicamente:** Logo, menu principale, sezione destra (account, social), versione mobile (`#ast-mobile-header`, menu a tendina).
- **Tutto il blocco** da subito dopo la chiusura dello script di customizer **fino a** `</header><!-- #masthead -->` va rimosso.

### 1.3 Footer (Astra)
- **Selettore:** `<footer class="site-footer" id="colophon"` fino a `</footer><!-- #colophon -->`.
- **Rimuovere anche** l'eventuale `</div>` che chiude un wrapper subito dopo `</footer>`.

---

## 2. Cosa tenere (contenuto "singola pagina")

- **Inizio:** dalla riga che apre `<div id="content" class="site-content">`.
- **Fine:** ultima riga prima di `<footer class="site-footer"` (es. il commento `<!-- #content -->` o la chiusura `</div>` di `#content`).
- **Struttura tipica:** `#content` → `.ast-container` → contenuto Elementor (Tutor accordion "Programma del corso", ecc.).

---

## 3. Procedimento tecnico (estrazione righe)

1. **Individua i numeri di riga** cercando i marker sotto nel file HTML completo.
2. **Crea il file "solo contenuto"** con:
   - Righe **1 → N1**: da inizio file fino a subito prima di `wpadminbar` (es. fino alla fine dello script dopo `<body>`).
   - Righe **N2 → N3**: da `<div id="content"` incluso fino alla fine del contenuto (prima del `<footer`).
   - Righe **N4 → fine**: da subito dopo `</footer>` (e eventuale `</div>`) fino a `</html>`.

Esempio con `sed` (sostituisci N1, N2, N3, N4 con i numeri reali):

```bash
sed -n '1,N1p' "01_Input_Sorgente_completa_Chrome.html" > "03_Output_Pagina_completa_apribile_in_browser.html"
sed -n 'N2,N3p' "01_Input_Sorgente_completa_Chrome.html" >> "03_Output_Pagina_completa_apribile_in_browser.html"
sed -n 'N4,$p' "01_Input_Sorgente_completa_Chrome.html" >> "03_Output_Pagina_completa_apribile_in_browser.html"
```

- **N1** = ultima riga prima di `<div id="wpadminbar"` (es. 512).
- **N2** = prima riga con `<div id="content"` (es. 791).
- **N3** = ultima riga del contenuto prima di `<footer` (es. 1949).
- **N4** = prima riga dopo `</footer>` e eventuale `</div>` (es. 2076).

Verifica sempre sul file reale con una ricerca di `</header>`, `id="content"`, `site-footer`, `#colophon`.

---

## 4. Accorgimenti per risultato ottimale

### 4.1 Schermo intero (nessun riquadro/bordi)
Aggiungere in `<head>` un blocco stile (es. `<style id="landing-solo-contenuto-overrides">`):

- `html { margin-top: 0 !important; }`
- `body { margin: 0; padding: 0; }`
- `#content.site-content` e `#content .ast-container`: `max-width: 100% !important; width: 100% !important; padding: 0 !important; margin: 0 !important;` (e `padding-left/right: 0` per `.ast-container`).

### 4.2 Accordion "Programma del corso" (Tutor)
- Le sezioni devono **restare aperte** (più sezioni apribili, nessuna chiusura automatica) e **aprirsi/chiudersi con animazione fluida** (no scatto).
- **CSS:** `.tutor-accordion-item-body { overflow: hidden; transition: max-height 0.35s ease-out, opacity 0.25s ease-out; }` e stati con `data-closed="true"` (max-height: 0) / non true (opacity: 1).
- **JS** (dopo `tutor-front.js`): intercetta il click su `.tutor-accordion .tutor-accordion-item-header` (preventDefault + stopImmediatePropagation); toggle di `data-closed` e `max-height` (0 vs scrollHeight / 2000px) sul `.tutor-accordion-item-body`; **inizializzazione:** per ogni `.tutor-accordion-item-body` impostare `data-closed` e `max-height` in base allo stato iniziale (display: none = chiuso), poi `display: block`.

### 4.3 Ottimizzazione e peso
- **Rimuovere:** link `admin-bar-css`, blocco `admin-bar-inline-css`, link `elementor-wp-admin-bar-css`. Opzionale: rimuovere dal `<body>` la classe `admin-bar` e in coda alla pagina gli script `elementor-admin-bar-js-before`, `elementor-admin-bar.min.js`, `hoverintent-js`, `admin-bar.min.js`.

### 4.4 Frammento per blocco "HTML personalizzato" WordPress
- Estrarre **solo** il blocco da `<div id="content" class="site-content">` fino al commento `<!-- #content -->` (incluso).
- Salvarlo in un file separato (es. `04_Output_Solo_markup_per_blocco_HTML_WordPress.html`). Nel blocco WordPress l'aspetto può differire; per aspetto fedele usare `03_Output_Pagina_completa_apribile_in_browser.html`.

---

## 5. Riepilogo marker HTML (Astra + Elementor + Tutor)

| Cosa | Cerca nel sorgente |
|------|---------------------|
| Inizio admin bar | `<div id="wpadminbar"` |
| Inizio header | `<header class="site-header"` oppure `id="masthead"` |
| Fine header | `</header><!-- #masthead -->` |
| Inizio contenuto | `<div id="content" class="site-content">` |
| Fine contenuto | `<!-- #content -->` |
| Inizio footer | `<footer class="site-footer" id="colophon"` |
| Fine footer | `</footer><!-- #colophon -->` |

---

## 6. File del workflow

| File | Uso |
|------|-----|
| `01_Input_Sorgente_completa_Chrome.html` | Input: sorgente completa da Chrome. Sostituisci con la tua pagina. |
| `02_Riferimento_Pagina_vuota_header_footer.html` | Riferimento: pagina vuota dello stesso sito per identificare header/footer. Sostituisci con la tua. |
| `03_Output_Pagina_completa_apribile_in_browser.html` | Output: pagina completa (head + body + CSS + JS). Apri in browser. |
| `04_Output_Solo_markup_per_blocco_HTML_WordPress.html` | Output: solo markup `#content`. Incolla in blocco HTML WordPress. |
