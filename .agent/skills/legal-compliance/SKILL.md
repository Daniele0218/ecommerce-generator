---
name: legal-compliance
description: Genera pagine legali GDPR-compliant per e-commerce italiani. Usa quando il workflow raggiunge la fase di conformita legale, o quando l'utente chiede privacy policy, cookie policy, termini e condizioni, GDPR. Copre GDPR, ePrivacy, D.lgs. 70/2003, Codice del Consumo.
metadata:
  version: 1.0.0
---

# Skill: Legal Compliance per E-Commerce Italia

## Framework Legale Applicabile
- **GDPR** (Reg. UE 2016/679) — protezione dati personali
- **D.lgs. 196/2003** (Codice Privacy, aggiornato da D.lgs. 101/2018)
- **Direttiva ePrivacy** (2002/58/CE) + **Linee Guida Garante Cookie** (10 giugno 2021)
- **D.lgs. 70/2003** — commercio elettronico
- **D.lgs. 206/2005** — Codice del Consumo
- **Reg. UE 2024/3228** — abolizione piattaforma ODR (da marzo 2025)

## Dati Legalmente Obbligatori da Mostrare
Per D.lgs. 70/2003 art. 7, sul sito DEVONO essere visibili:
- **Ragione sociale / Nome ditta**
- **Sede legale** (indirizzo completo)
- **P.IVA**
- **Email di contatto**

**NON obbligatori sul sito** (anche se il titolare li possiede):
- PEC (obbligatoria per comunicazioni PA, non per il sito)
- Numero di telefono
- Codice Fiscale (se diverso dalla P.IVA)

## 4 Pagine Obbligatorie — SEMPRE
Per OGNI store e-commerce generato, creare SEMPRE queste 4 pagine:

### 1. Privacy Policy (`privacy-policy.html`)
**Base:** GDPR artt. 13-14
**Contenuto minimo:**
- Identita e contatti del titolare
- Categorie di dati raccolti (navigazione, checkout, acquisto, cookie)
- Finalita e base giuridica (tabella: finalita / base / dati)
- Destinatari e terze parti (adapta in base ai servizi attivi)
- Trasferimenti extra-UE (se applicabile, con garanzie SCCs)
- Periodo di conservazione (acquisti 10 anni, navigazione 24 mesi, cookie per durata, consensi 5 anni)
- Diritti dell'interessato (accesso, rettifica, cancellazione, portabilita, opposizione, reclamo Garante)
- Conferimento dati (obbligatorio vs opzionale)

### 2. Cookie Policy (`cookie-policy.html`)
**Base:** ePrivacy + Linee Guida Garante 2021
**Contenuto minimo:**
- Definizione cookie
- Cookie tecnici (Shopify session/cart — NO consenso necessario)
- Cookie marketing/profilazione (solo se pixel attivi — richiedono consenso)
- Cookie analitici (se GA attivo)
- Terze parti con link alle loro policy
- Come gestire/revocare il consenso (banner, footer link, browser)

### 3. Termini e Condizioni (`termini-condizioni.html`)
**Base:** D.lgs. 70/2003 + Codice del Consumo
**Contenuto minimo:**
- Identificazione venditore (dati essenziali)
- Prodotti e prezzi (IVA inclusa + spedizione)
- Modalita di pagamento
- Processo di acquisto
- Spedizione e consegna
- Diritto di recesso 14 giorni (artt. 52-59)
- Esclusioni recesso (art. 59)
- Garanzia legale 24 mesi (artt. 128-135)
- Resi e rimborsi
- ADR (**NO riferimento a piattaforma ODR** — abolita da Reg. UE 2024/3228)
- Legge applicabile e foro competente (residenza consumatore)

### 4. Informativa Precontrattuale (`informativa-precontrattuale.html`)
**Base:** artt. 12-13 D.lgs. 70/2003
**Contenuto minimo:**
- Fasi tecniche conclusione contratto
- Archiviazione contratto
- Mezzi correzione errori
- Lingue disponibili
- Codici di condotta

## Cookie Banner — Quando e Come
**Necessario SOLO quando pixel di tracciamento sono attivi** (Meta, GA, TikTok).

### Requisiti Garante Italiano:
- 3 pulsanti con **stessa prominenza visiva**: "Accetta Tutti", "Rifiuta", "Personalizza"
- Nessun checkbox pre-selezionato
- Nessun scroll-consent o implied consent
- Pixel **bloccati** fino a consenso esplicito (injection dinamica script)
- Consenso in **localStorage** (NON sessionStorage) con versione e timestamp
- Link a cookie-policy.html nel banner
- Link "Gestisci Cookie" nel footer per riaprire il banner
- `z-index` superiore a sticky CTA

### Se NESSUN pixel attivo:
- Cookie banner NON necessario
- Le 4 pagine legali sono comunque SEMPRE obbligatorie

## Servizi Terzi Comuni — Implicazioni Privacy

| Servizio | Tipo | Cookie | Consenso | Trasferimento |
|----------|------|--------|----------|---------------|
| Shopify | Piattaforma e-commerce | Tecnici (_shopify_s, _shopify_y, cart) | Non necessario | USA (SCCs) |
| PayPal | Pagamenti | Tecnici di sessione | Non necessario | Lussemburgo (UE) |
| Meta Pixel | Marketing | Profilazione (_fbp, _fbc, fr) | Obbligatorio | USA (SCCs) |
| Google Analytics | Analytics | Analytics | Necessario (se non anonimizzato) | USA (SCCs) |
| TikTok Pixel | Marketing | Profilazione | Obbligatorio | USA/Singapore (SCCs) |

## Dati Titolare
Leggi SEMPRE `config/owner-data.json` per i dati del titolare.
Se il file non esiste, chiedi all'utente SOLO i dati essenziali:
1. Nome/Ragione Sociale
2. P.IVA
3. Sede legale (indirizzo completo)
4. Email di contatto
Poi salva in `config/owner-data.json`.

## Design Pagine Legali
- Stesso tema dello store (palette, font, Tailwind CDN)
- Header semplificato: logo + "Torna allo Store"
- Container `max-w-4xl` per leggibilita
- `<meta name="robots" content="noindex,follow">`
- Footer con P.IVA, link a tutte le pagine legali, "Gestisci Cookie"
- Responsive 390/768/1440px
- Peso < 30KB per pagina

## Come Usare i Template (PROCEDURA OBBLIGATORIA)

**NON riscrivere le pagine legali da zero.** Usa SEMPRE i template pronti in `references/`.

### Procedura:
1. **Leggi `config/owner-data.json`** — se non esiste, chiedi i dati essenziali e crealo
2. **Leggi `references/legal-data-checklist.md`** — contiene la mappatura completa dei placeholder
3. **Copia i 4 template HTML** da `references/` nella cartella output dello store
4. **Sostituisci i placeholder** `{{...}}` con i dati reali:
   - Dati titolare da `owner-data.json`
   - Palette e font dallo `store-info.json` o dalla brand identity dello store
   - Pixel ID da `config/shopify-credentials.json`
   - Data corrente per `{{LAST_UPDATED}}`
5. **Adatta le sezioni condizionali**:
   - Se Meta Pixel attivo → includi sezioni Meta nelle terze parti
   - Se TikTok Pixel attivo → includi sezioni TikTok
   - Se GA attivo → includi sezioni Google Analytics
   - Se nessun pixel → rimuovi sezione 3 (Marketing) dalla cookie policy
6. **Inserisci cookie banner** da `references/cookie-banner-template.html` nell'index.html (SOLO se pixel attivi)
7. **Aggiorna footer** di index.html con link alle 4 pagine legali + P.IVA + "Gestisci Cookie"

### Template disponibili in `references/`:
| File | Descrizione |
|------|-------------|
| `privacy-policy-template.html` | Privacy Policy completa GDPR artt. 13-14 |
| `cookie-policy-template.html` | Cookie Policy ePrivacy + Garante 2021 |
| `terms-conditions-template.html` | Termini e Condizioni D.lgs. 70/2003 + Codice Consumo |
| `precontractual-info-template.html` | Informativa Precontrattuale artt. 12-13 D.lgs. 70/2003 |
| `cookie-banner-template.html` | Snippet HTML+JS del banner GDPR (Meta + TikTok + GA) |
| `legal-data-checklist.md` | Guida completa placeholder, mappature, blocchi condizionali |
