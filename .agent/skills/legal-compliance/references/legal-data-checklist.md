# Checklist Dati Legali per E-Commerce Italia

## Dati da Chiedere al Titolare (SOLO se `config/owner-data.json` non esiste)

### Obbligatori (D.lgs. 70/2003 art. 7)
1. **Nome / Ragione Sociale** — es. "Mario Rossi" o "Rossi S.r.l."
2. **Tipo di attivita** — ditta_individuale / srl / srls / sas / snc / altro
3. **Partita IVA** — formato IT + 11 cifre
4. **Sede legale** — via, civico, CAP, citta, provincia, paese
5. **Email di contatto** — email pubblicata sul sito

### NON obbligatori sul sito (NON chiedere se non necessario)
- PEC — obbligatoria per comunicazioni PA, non per il sito web
- Telefono — opzionale
- Codice Fiscale — se diverso dalla P.IVA, non va esposto sul sito

---

## Placeholder nei Template

Usa questi placeholder nei template HTML. Sostituiscili con i dati reali:

| Placeholder | Fonte | Esempio |
|-------------|-------|---------|
| `{{STORE_NAME}}` | Nome brand dello store | NotteSud |
| `{{STORE_LOGO_HTML}}` | HTML del logo nel header/footer | `Notte<span class="text-primary">Sud</span>` |
| `{{LEGAL_NAME}}` | owner-data.json → legal_name | Militello Daniele |
| `{{BUSINESS_TYPE_LABEL}}` | owner-data.json → business_type (tradotto) | Ditta Individuale |
| `{{VAT_NUMBER}}` | owner-data.json → vat_number | IT07288450823 |
| `{{FULL_ADDRESS}}` | owner-data.json → registered_address (formattato) | Via Vittorio Emanuele 112, 90020 Vicari (PA), Italia |
| `{{CONTACT_EMAIL}}` | owner-data.json → contact_email | dmilitello04@gmail.com |
| `{{PRIMARY_COLOR}}` | Palette dello store | #1B2951 |
| `{{PRIMARY_DARK}}` | Variante dark del primary | #111D38 |
| `{{ACCENT_COLOR}}` | Colore accento | #C9A84C |
| `{{SURFACE_COLOR}}` | Colore sfondo | #F5F6FA |
| `{{FONT_HEADING}}` | Nome font heading | Poppins |
| `{{FONT_BODY}}` | Nome font body | Inter |
| `{{FONT_HEADING_URL}}` | URL Google Fonts heading | Inter:wght@400;500;600;700 |
| `{{FONT_BODY_URL}}` | URL Google Fonts body | Poppins:wght@600;700 |
| `{{LAST_UPDATED}}` | Data generazione | 27 febbraio 2026 |
| `{{CURRENT_YEAR}}` | Anno corrente | 2026 |
| `{{SHIPPING_DAYS}}` | Tempi di consegna | 5-10 |
| `{{FORUM_CITY}}` | Foro competente (citta sede) | Palermo |
| `{{STORE_CONSENT_KEY}}` | Chiave localStorage cookie | nottesud_cookie_consent |
| `{{META_PIXEL_ID}}` | ID Meta/FB Pixel ('' se non attivo) | 123456789012345 |
| `{{TIKTOK_PIXEL_ID}}` | ID TikTok Pixel ('' se non attivo) | ABCDEFGH12345 |
| `{{GA_ID}}` | ID Google Analytics ('' se non attivo) | G-XXXXXXXXXX |

### Placeholder condizionali (sezioni da includere/escludere)

| Placeholder | Quando includere |
|-------------|-----------------|
| `{{THIRD_PARTIES_MARKETING}}` | Blocco HTML con le terze parti marketing attive (Meta, TikTok, GA) |
| `{{TRANSFERS_EXTRA_EU}}` | Blocco HTML con dettagli trasferimenti extra-UE per pixel attivi |

---

## Mappatura business_type → Label

| Valore JSON | Label italiana |
|-------------|---------------|
| ditta_individuale | Ditta Individuale |
| srl | S.r.l. |
| srls | S.r.l.s. |
| sas | S.a.s. |
| snc | S.n.c. |
| spa | S.p.A. |
| cooperativa | Societa Cooperativa |
| altro | (usare il valore fornito) |

---

## Foro Competente

Determinare la citta del foro dalla **provincia** della sede legale:
- Usare il capoluogo di provincia (es. provincia PA → Palermo, MI → Milano, RM → Roma)

---

## Pagine da Generare (SEMPRE tutte e 4)

1. `privacy-policy.html` — Informativa Privacy (GDPR artt. 13-14)
2. `cookie-policy.html` — Cookie Policy (ePrivacy + Garante 2021)
3. `termini-condizioni.html` — Termini e Condizioni di Vendita (D.lgs. 70/2003 + Codice Consumo)
4. `informativa-precontrattuale.html` — Informativa Precontrattuale (artt. 12-13 D.lgs. 70/2003)

---

## Cookie Banner (SOLO se pixel attivi)

Se almeno un pixel e configurato (Meta, TikTok, GA), aggiungere:
1. Banner HTML in index.html (dopo sticky CTA)
2. JavaScript per gestione consenso
3. Link "Gestisci Cookie" nel footer

Usare il template `cookie-banner-template.html`.

Se NESSUN pixel e attivo: NON aggiungere il banner, ma le 4 pagine legali sono comunque OBBLIGATORIE.

---

## Terze Parti — Blocchi HTML Condizionali

### Meta Pixel (privacy-policy.html, sezione 4)
```html
<li>
  <strong>Meta Platforms Ireland Ltd</strong> (4 Grand Canal Square, Grand Canal Harbour, Dublino 2, Irlanda) —
  Servizio Meta/Facebook Pixel per finalita di marketing e remarketing.
  <strong>L'attivazione avviene esclusivamente previo consenso dell'utente.</strong>
  I dati possono essere trasferiti negli USA con garanzie adeguate (Clausole Contrattuali Standard).
</li>
```

### TikTok Pixel (privacy-policy.html, sezione 4)
```html
<li>
  <strong>TikTok Technology Limited</strong> (10 Earlsfort Terrace, Dublino 2, D02 T380, Irlanda) —
  Servizio TikTok Pixel per finalita di marketing, remarketing e misurazione delle campagne pubblicitarie.
  <strong>L'attivazione avviene esclusivamente previo consenso dell'utente.</strong>
  I dati possono essere trasferiti negli USA e a Singapore con garanzie adeguate (Clausole Contrattuali Standard).
</li>
```

### Google Analytics (privacy-policy.html, sezione 4)
```html
<li>
  <strong>Google LLC</strong> (1600 Amphitheatre Parkway, Mountain View, CA 94043, USA) —
  Servizio Google Analytics per finalita di analisi statistica del traffico web.
  I dati possono essere trasferiti negli USA con garanzie adeguate (Clausole Contrattuali Standard).
</li>
```

---

## Trasferimenti Extra-UE — Blocchi HTML Condizionali

### Meta (privacy-policy.html, sezione 5)
```html
<li>
  <strong>Meta Platforms Ireland Ltd</strong> — Trasferimento verso USA protetto da SCCs.
  Informativa privacy: <a href="https://www.facebook.com/privacy/policy/">https://www.facebook.com/privacy/policy/</a>
</li>
```

### TikTok (privacy-policy.html, sezione 5)
```html
<li>
  <strong>TikTok Technology Limited</strong> — Trasferimento verso USA e Singapore protetto da SCCs.
  Informativa privacy: <a href="https://www.tiktok.com/legal/privacy-policy-eea">https://www.tiktok.com/legal/privacy-policy-eea</a>
</li>
```

### Google (privacy-policy.html, sezione 5)
```html
<li>
  <strong>Google LLC</strong> — Trasferimento verso USA protetto da SCCs.
  Informativa privacy: <a href="https://policies.google.com/privacy">https://policies.google.com/privacy</a>
</li>
```