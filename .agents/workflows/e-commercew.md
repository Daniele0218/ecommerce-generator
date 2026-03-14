---
description: Analizza link prodotto, propone brand/pricing/strategie CRO all'utente, attende conferma, poi genera store HTML completo con Shopify Buy SDK, SEO, social proof, deploy su Vercel. Include social captions e self-learning.
---

# Workflow: /build-store

## Fase 1 — SETUP
Leggi `config/shopify-credentials.json`. Se mancano domain o storefront token, chiedi all'utente e fermati.
Verifica che `api_version` sia presente (default: `2026-01`).
Se esiste `config/github-repo.txt`, leggi il nome del repo per il deploy.
Se esiste `LEARNINGS.md`, leggilo per applicare lezioni apprese.

## Fase 2 — SCRAPING E ANALISI PRODOTTO
Apri il link fornito dall'utente (Alibaba, AliExpress, 1688, Amazon, o altro).
Estrai TUTTO:
- Titolo prodotto originale
- Prezzo sorgente (costo)
- Tutte le immagini disponibili (URL)
- Descrizione completa
- Varianti (taglie, colori, materiali, quantità)
- Specifiche tecniche (materiale, dimensioni, peso)
- Categoria/nicchia del prodotto

## Fase 3 — PLANNING: DOMANDE ALL'UTENTE
PRIMA di procedere, presenta all'utente la tua analisi e fai domande su TUTTO ciò che non puoi decidere da solo. Usa questo formato:

---
### 📋 Analisi Prodotto
**Prodotto**: [titolo]
**Nicchia identificata**: [nicchia]
**Target ipotizzato**: [target demografico e psicografico]
**Prezzo sorgente**: €/$ [prezzo]
**Varianti trovate**: [elenco]

### 💰 Pricing
- **Prezzo vendita proposto**: €[prezzo] (markup [X]x)
- **Prezzo barrato proposto**: €[prezzo barrato]
- **Vuoi un prezzo diverso?**
- **Valuta**: EUR — va bene o preferisci altra valuta?

### 🎨 Brand & Design
- **Nomi brand proposti** (3 opzioni):
  1. [nome] — [perché funziona per questa nicchia]
  2. [nome] — [perché]
  3. [nome] — [perché]
- **Stile visivo proposto**: [minimale/bold/dark/soft/etc.] — [motivazione]
- **Palette proposta**: [descrizione colori con HEX]
- **Font proposti**: [heading] + [body]
- **Hai preferenze diverse?**

### 🧠 Strategia di Conversione
In base al prodotto e al target, propongo queste strategie (dimmi se vuoi aggiungerne o toglierne):

**Leve psicologiche che applicherò:**
- [✅/❌] Scarsità/urgenza — [motivazione per sì/no]
- [✅/❌] Social proof con reviews — [tipo di reviews]
- [✅/❌] PAS framework nella copy — [se il prodotto risolve un problema chiaro]
- [✅/❌] FOMO sociale — [se il target è sensibile ai trend]
- [✅/❌] Prezzo barrato con anchoring — [sempre consigliato]
- [✅/❌] Costo giornaliero — [solo se prezzo alto]
- [✅/❌] Inversione rischio (garanzia creativa) — [tipo proposto]

**Elementi strutturali:**
- [✅/❌] Sticky CTA su mobile — [sempre consigliato]
- [✅/❌] Badge pagamento sicuro — [sempre consigliato]
- [✅/❌] Threshold spedizione gratuita — [soglia proposta: €X]
- [✅/❌] Bundle "Complete the Look/Kit" — [solo se ha senso per il prodotto]
- [✅/❌] Upsell quantità (compra 2 risparmia X%) — [se il prodotto si presta]
- [✅/❌] Exit intent popup con sconto — [sì/no e motivazione]
- [✅/❌] Size guide — [solo fashion/wearable]
- [✅/❌] FAQ strategiche — [obiezioni identificate]

**Elementi avanzati (propongo solo se rilevanti):**
- [✅/❌] Advertorial/storytelling page — [se il prodotto richiede educazione]
- [✅/❌] Quiz funnel — [se ci sono varianti o personalizzazione]
- [✅/❌] Notifiche real-time acquisti — [se volume credibile]
- [✅/❌] Pagamento rateale (Klarna/Scalapay) — [se prezzo > €50]

### 🖼️ Immagini
- **Immagini dal prodotto originale**: [N immagini trovate]
- **Qualità**: [buona/mediocre/scarsa]
- **Propongo di generare con Nano Banana Pro**:
  - [✅/❌] Hero banner lifestyle — [descrizione scena proposta]
  - [✅/❌] Immagine prodotto ambientata — [contesto]
  - [✅/❌] Immagini per social media — [stile]
- **Vuoi altre immagini specifiche?**

### 📱 Social Content
- **Piattaforme target**: TikTok + Instagram (default) — altre?
- **Tone proposto per i caption**: [descrizione]
- **Genero caption e hashtag set?** [sì di default]

### 📦 Tipo di Store
- [ ] Monoprodotto (landing page singola)
- [ ] Multi-prodotto (se hai altri link da aggiungere)

### ⚡ Conferma o modifica
Dimmi cosa cambiare, oppure conferma e parto con la creazione.
---

ATTENDI la risposta dell'utente prima di procedere. Se l'utente conferma tutto, vai alla Fase 4. Se modifica qualcosa, aggiorna il piano.

## Fase 4 — BRAND IDENTITY
Leggi la skill `ui-ux-pro-max`. In base alla nicchia e alle scelte confermate:
- Definisci palette completa (primary, secondary, accent, background, text)
- Seleziona font Google (heading + body)
- Definisci tone of voice per tutta la copy
- Definisci stile fotografico per eventuali immagini generate

## Fase 5 — COPY E SEO
Leggi le skill `copywriting`, `seo-audit`, `ai-seo`, `schema-markup`.
Genera:
- Titolo prodotto ottimizzato (SEO + persuasivo)
- Descrizione prodotto (usa il framework psicologico scelto: PAS, benefit-driven, etc.)
- Headline hero section
- CTA primario e secondario
- Testi per badge urgenza/social proof (se applicabili)
- Reviews statiche credibili (nomi realistici, rating 4.5-4.8, testo che risponde a obiezioni)
- Meta title (<60 char), meta description (<160 char)
- Keywords primarie e secondarie
- FAQ strategiche (se attivate)
- Testi trust elements (garanzia, spedizione, reso)

## Fase 6 — SHOPIFY PRODUCT
Se `admin_access_token` è presente nel config:
- Crea il prodotto su Shopify via Admin API (GraphQL)
- Upload immagini su Shopify CDN
- Configura varianti e prezzi
- Imposta compare_at_price per il prezzo barrato
- Recupera il product handle per il frontend

Se admin token non presente: chiedi all'utente di creare il prodotto manualmente su Shopify e fornire il product handle.

## Fase 7 — IMAGE GENERATION
Se nella Fase 3 l'utente ha confermato la generazione immagini:
- Usa Nano Banana Pro per generare le immagini richieste
- Stile coerente con la brand identity definita nella Fase 4
- Upload su Shopify CDN (o salva nella cartella output)
- Verifica che le immagini siano di qualità sufficiente

## Fase 8 — FRONTEND GENERATION
Leggi le skill `page-cro` e `marketing-psychology`.
Genera il file HTML completo con TUTTO integrato:

**Struttura base (adatta all'ordine in base alla nicchia):**
1. Header minimal (brand name, nient'altro per monoprodotto)
2. Hero section (immagine dominante + titolo + prezzo con anchoring + CTA)
3. Badge urgenza/trust (se attivati)
4. Variant selector (se ci sono varianti)
5. Product details (descrizione con framework psicologico scelto)
6. Image gallery (griglia o slider)
7. Social proof / reviews
8. FAQ strategiche (se attivate)
9. CTA finale con urgenza
10. Footer (brand, copyright, privacy policy, P.IVA)

**Elementi tecnici obbligatori:**
- Storefront API GraphQL integrata con pattern completo (fetch prodotto, Cart API, error handling, varianti)
- ZERO SDK deprecati — solo fetch() diretto a Storefront API
- Sticky CTA su mobile (se attivato)
- Lazy loading immagini
- Animazioni CSS subtle (fade-in, hover)
- Schema JSON-LD Product
- Open Graph tags completi
- Tracking pixels (se configurati)
- Cookie banner GDPR (se pixel attivi)
- Testo scansionabile: grassetto su keyword, paragrafi brevi

**Per store multi-prodotto:**
- index.html (homepage) + product-{handle}.html per ogni prodotto
- Navigazione coerente tra pagine
- Design system condiviso

## Fase 9 — SOCIAL CONTENT
Crea `social-captions.md` con:
- 3 caption TikTok (max 150 char, hook forte, emoji, 3-5 hashtag)
- 3 caption Instagram (max 300 char, CTA "Link in bio")
- Hashtag set: 5 broad + 5 niche + 5-10 trending
- Tone coerente con brand e nicchia

## Fase 10 — PAGINE LEGALI E GDPR
Leggi la skill `legal-compliance` (`.agent/skills/legal-compliance/SKILL.md`).

1. **Dati titolare**: Leggi `config/owner-data.json`. Se non esiste, chiedi all'utente SOLO: nome/ragione sociale, P.IVA, sede legale, email contatto. Salva in `config/owner-data.json`.

2. **Genera 4 pagine legali**: Usa i template HTML pronti in `.agent/skills/legal-compliance/references/`. NON riscrivere da zero. Copia i template, sostituisci i placeholder `{{...}}` con i dati reali dello store (dati titolare, palette, font, pixel attivi). Segui `references/legal-data-checklist.md` per la mappatura completa.

3. **Cookie banner** (SOLO se pixel attivi): Se Meta Pixel, TikTok Pixel o GA sono configurati in `config/shopify-credentials.json`, inserisci il cookie banner da `references/cookie-banner-template.html` in index.html. Se nessun pixel → NON inserire banner.

4. **Aggiorna footer index.html**: Aggiungi P.IVA, link alle 4 pagine legali, link "Gestisci Cookie".

5. **Salva le 4 pagine** nella cartella output dello store: `privacy-policy.html`, `cookie-policy.html`, `termini-condizioni.html`, `informativa-precontrattuale.html`.

## Fase 11 — VALIDAZIONE
Completa questa checklist PRIMA di consegnare. Non saltare nessun punto.

**Frontend & Funzionalita:**
- [ ] HTML valido (tag chiusi, struttura corretta)
- [ ] Immagini: tutte caricano da URL reali, NO placeholder
- [ ] Buy Button: click → Cart API (cartCreate) → checkoutUrl → redirect checkout Shopify. Funzionante.
- [ ] Variant selector: funziona correttamente (se presente)
- [ ] Prezzo: corretto, con simbolo valuta, barrato se attivato
- [ ] Meta title <60 char, meta description <160 char
- [ ] Open Graph: og:title, og:description, og:image, og:type, og:url
- [ ] Schema JSON-LD Product completo
- [ ] Responsive 390px: CTA visibile, testo leggibile, immagini ok
- [ ] ZERO Lorem Ipsum, placeholder, testo filler
- [ ] ZERO URL inventati o rotti
- [ ] ZERO `{VARIABILE}` o `{{PLACEHOLDER}}` non sostituiti
- [ ] Font Google caricano correttamente
- [ ] Contrasto WCAG AA rispettato
- [ ] CTA above the fold su mobile
- [ ] HTML sotto 50KB
- [ ] Sticky CTA funziona su mobile (se attivato)
- [ ] Leve psicologiche applicate coerenti con le scelte confermate
- [ ] Trust elements presenti
- [ ] Design coerente con nicchia e brand identity

**Conformita Legale GDPR:**
- [ ] 4 pagine legali presenti e accessibili (privacy-policy, cookie-policy, termini-condizioni, informativa-precontrattuale)
- [ ] P.IVA visibile nel footer di TUTTE le pagine (index + 4 legali)
- [ ] Link alle pagine legali nel footer di index.html
- [ ] Cookie banner presente SOLO se pixel attivi (Meta, TikTok, GA)
- [ ] Cookie banner: 3 pulsanti equiprominenti (Accetta/Rifiuta/Personalizza)
- [ ] Pixel bloccati fino a consenso esplicito (no script caricati prima del consenso)
- [ ] Link "Gestisci Cookie" nel footer per riaprire il banner
- [ ] Pagine legali responsive (390/768/1440px) e < 30KB ciascuna
- [ ] Nessun placeholder `{{...}}` rimasto nelle pagine legali
- [ ] Dati titolare corretti (da owner-data.json)

**Output files:**
- [ ] social-captions.md creato
- [ ] store-info.json creato
- [ ] (Multi-prodotto) Navigazione tra pagine funziona

## Fase 12 — OUTPUT E DEPLOY
Salva tutto in `output/stores/{brand-name-lowercase}/`.

Crea `store-info.json`:
```json
{
  "brand": "Nome",
  "niche": "...",
  "target": "...",
  "palette": { "primary": "#", "secondary": "#", "accent": "#", "bg": "#" },
  "fonts": { "heading": "...", "body": "..." },
  "strategies_applied": ["scarsità", "social proof", "sticky CTA", ...],
  "products": [{ "title": "...", "price": 0, "compare_price": 0, "handle": "..." }],
  "created": "YYYY-MM-DD",
  "deployed_url": "",
  "github_repo": ""
}
```

### Architettura: 1 Store = 1 Repo GitHub = 1 Progetto Vercel
**REGOLA FONDAMENTALE**: Ogni store ha il proprio repo GitHub dedicato. MAI usare branch dello stesso repo per store diversi.

- Il workspace `ecommerce-generator` e la "fabbrica" che genera gli store — NON va deployato su Vercel
- Ogni store generato va nel suo repo: `store-{brand-name}` (es. `store-nottesud`, `store-mioaltrobrand`)
- Vercel free supporta progetti illimitati, ogni repo = 1 URL (es. `store-nottesud.vercel.app`)
- Dominio custom opzionale per ogni progetto Vercel

### Deploy: Frontend → GitHub → Vercel
Il deploy segue SEMPRE questo flusso:

**Se il repo GitHub dello store esiste gia:**
1. Copia i file generati nel repo locale
2. `git add . && git commit -m "Store update" && git push origin main`
3. Vercel auto-deploya (e gia collegato)

**Se e il primo deploy (repo non esiste):**
1. Crea repo GitHub: `gh repo create store-{brand-name} --public --clone`
2. Copia nella root del repo:
   - `index.html` (e eventuali `product-*.html`)
   - Le 4 pagine legali (`privacy-policy.html`, `cookie-policy.html`, `termini-condizioni.html`, `informativa-precontrattuale.html`)
3. NON includere nel repo: `social-captions.md`, `store-info.json` (sono file interni)
4. Push su `main`
5. Vai su vercel.com → Add New → Project → Import repo GitHub
6. Settings: Framework "Other", Output Directory ".", nessun build command
7. Deploy → URL live generata automaticamente
8. (Opzionale) Collega dominio custom in Vercel → Settings → Domains

**Dopo il deploy**, aggiorna `store-info.json` con:
- `"deployed_url": "https://store-nomebrand.vercel.app"`
- `"github_repo": "store-nomebrand"`

Fornisci sempre all'utente:
- I comandi git esatti da eseguire
- Il link Vercel per importare il repo
- Istruzioni per dominio custom se richiesto

**MAI deployare via Vercel API diretta o CLI senza repo GitHub.**
**MAI deployare il repo ecommerce-generator — e solo il tool di generazione.**

## Fase 13 — RIEPILOGO
Mostra:
```
🏪 Brand: [nome]
🎯 Nicchia: [nicchia] → Target: [target]
🎨 Palette: [primary] [secondary] [accent] [bg]
✏️ Font: [heading] + [body]
🛍️ Prodotti: [N] — [titoli]
💰 Prezzo: €[prezzo] (barrato: €[compare]) — Markup: [X]x
🧠 Strategie: [elenco strategie applicate]
📁 Files: output/stores/[brand]/
📦 GitHub: [repo url]
🚀 URL: [url Vercel o "da deployare"]
📱 Social: captions pronti
```

## Fase 14 — SELF-LEARNING
Aggiorna `LEARNINGS.md` con:
- Nicchia → strategie che hanno funzionato
- Combinazione palette/font efficace
- Errori corretti
- Pattern da riusare