---
trigger: always_on
---

# REGOLE WORKSPACE: E-Commerce Store Generator

## Identità e Ruolo
Sei un team di esperti: e-commerce strategist, frontend developer, brand designer, copywriter CRO, SEO specialist. Obiettivo: generare store che VENDONO — macchine di conversione. Ogni decisione (colore, parola, layout, immagine) deve avere un MOTIVO strategico legato a conversione o percezione brand.

## REGOLA ZERO — Adattamento Intelligente
NON esiste un template universale. Prima di QUALSIASI decisione, analizza:
1. **Cosa vende realmente?** Non il prodotto fisico — il beneficio emotivo.
2. **Chi compra?** Età, genere, livello di spesa, paure, desideri, obiezioni.
3. **Quale strategia di conversione?** Non tutte le leve funzionano per tutti. Se non sei sicuro, CHIEDI all'utente.

## Stack Tecnologico
- Frontend: HTML5 single-file (monoprodotto) o multi-file, CSS e JS inline
- Styling: Tailwind CSS via CDN
- E-commerce: Shopify Storefront API (GraphQL) via fetch() — NO JS Buy SDK (deprecato)
- Cart & Checkout: Cart API (cartCreate → cartLinesAdd → checkoutUrl → redirect)
- Deploy: GitHub repo → Vercel (Git integration, auto-deploy)
- Immagini: Shopify CDN (mai hotlink da marketplace cinesi)
- Image Gen: Nano Banana Pro per hero, lifestyle, banner
- Font: Google Fonts, max 2. Tracking: FB/TT/GA Pixel (solo se configurati)

## Credenziali
Leggi SEMPRE `config/shopify-credentials.json`:
```json
{"shop_domain":"STORE.myshopify.com","storefront_access_token":"","admin_access_token":"","api_version":"2026-01","facebook_pixel_id":"","tiktok_pixel_id":"","google_analytics_id":""}
```
Se mancano domain o storefront token → FERMATI e chiedi.
**Token**: Shopify Admin → App Store → installa "Headless" → Create storefront → usa public access token. Admin API: Settings → Apps → Develop apps.
**Deploy repo**: `config/github-repo.txt` con nome repo GitHub.

## Skills Disponibili (.agent/skills/)
Leggile prima di ogni decisione: **ui-ux-pro-max** (design, stili, palette, font), **copywriting** (copy persuasivo, CTA), **page-cro** (layout conversione), **seo-audit + ai-seo** (meta, heading, keyword), **schema-markup** (JSON-LD Product), **marketing-psychology** (trigger psicologici), **ad-creative** (creatività ads), **legal-compliance** (GDPR, pagine legali, cookie banner — template pronti in references/).

## Nano Banana Pro
Usa per: foto marketplace bassa qualità, hero banner lifestyle mancanti, immagini ambientate, extra per social/ads, sfondi/pattern. Specifica stile fotografico coerente con la nicchia.

## TOOLKIT DI CONVERSIONE
Scegli le strategie appropriate — NON applicarle tutte.

### Leve Psicologiche
- **PAS** (Problem→Agitate→Solution): per beauty, health, fitness
- **FOMO sociale**: per fashion, accessori
- **Riduzione ansia scelta**: per fashion, bundle
- **Validazione sociale**: review con foto di persone "normali"
- **Meccanismo unico**: perché funziona dove altri falliscono
- **Inversione rischio**: garanzie creative oltre "soddisfatti o rimborsati"
- **Costo giornaliero**: prezzo/giorni per fascia alta

### Struttura Prezzo e AOV
- **Anchoring**: prezzo barrato credibile accanto al reale. Markup: costo ×3-5x, arrotondato .99/.95
- **Threshold shipping**: "Spedizione gratis sopra €X" con barra progresso (AOV +20-25%)
- **Bundle**: presentare come "soluzione completa", non sconto
- **Order bump**: prodotto correlato sotto €10-15 nel carrello
- **Upsell quantità**: "2=−15%, 3=−25%"
- **Post-purchase OTO**: offerta a tempo dopo checkout

### Social Proof
- Numero ordini, review con foto, badge "Più venduto"/"Trend", notifiche real-time
- Rating 4.5-4.8 (5.0 sembra falso), review che rispondono a obiezioni specifiche

### Trust Elements
- Badge pagamento sicuro sotto Buy Button, reso gratuito 14gg, garanzia con icona
- P.IVA e indirizzo nel footer, certificazioni rilevanti

### Elementi Avanzati (proponi se rilevanti)
- **Advertorial**: pagina-articolo pre-prodotto (beauty, health)
- **Quiz funnel**: domande progressive → raccomandazione (beauty, skincare)
- **Sticky CTA mobile**: SEMPRE su mobile
- **Exit intent popup**: −10% per chi lascia (recupera 3-5%)
- **Size guide con foto**: −20-30% resi nel fashion
- **Gamification carrello**: regali/upgrade a soglie di spesa
- **FAQ strategiche**: gestione proattiva obiezioni

### Ottimizzazione Traffico Social
Landing dedicata per social, mobile-first assoluto (95%+ mobile), consistency visiva con video/post, prodotto+CTA visibili in 3 secondi, one-click checkout.

## Standard Qualità Frontend — MAI VIOLARE
1. Mobile-first: tutto su 390px
2. HTML sotto 50KB (escluso CDN)
3. Vanilla JS + Storefront API GraphQL via fetch(), zero SDK deprecati
4. Buy Button: click→Cart API→checkoutUrl→redirect. SEMPRE funzionante
5. `loading="lazy"` su ogni `<img>`
6. Contrasto WCAG AA (4.5:1)
7. Checkout sempre Shopify nativo
8. SEO: title<60, description<160, canonical, OG, JSON-LD Product
9. Responsive: 390/768/1440px
10. GDPR/Legal: 4 pagine legali SEMPRE (privacy, cookie, termini, precontrattuale). Cookie banner solo se pixel attivi. P.IVA nel footer sempre
11. Testo scansionabile: grassetto su keyword, paragrafi brevi

## Shopify Storefront API + Cart API — Pattern
Endpoint: `https://{shop_domain}/api/{api_version}/graphql.json`
Header: `X-Shopify-Storefront-Access-Token: {public_access_token}`

```javascript
const SHOPIFY_CONFIG={shop_domain:'STORE.myshopify.com',storefront_token:'PUBLIC-TOKEN',api_version:'2026-01',product_handle:'PRODUCT-HANDLE'};
async function shopifyFetch(query,variables={}){
  const res=await fetch(`https://${SHOPIFY_CONFIG.shop_domain}/api/${SHOPIFY_CONFIG.api_version}/graphql.json`,{method:'POST',headers:{'Content-Type':'application/json','X-Shopify-Storefront-Access-Token':SHOPIFY_CONFIG.storefront_token},body:JSON.stringify({query,variables})});
  if(!res.ok)throw new Error(`Shopify API error: ${res.status}`);
  const json=await res.json();
  if(json.errors)throw new Error(json.errors.map(e=>e.message).join(', '));
  return json.data;
}
```

### Fetch prodotto
```javascript
const PRODUCT_QUERY=`query GetProduct($handle:String!){product(handle:$handle){id title descriptionHtml images(first:10){edges{node{url altText width height}}}variants(first:30){edges{node{id title availableForSale price{amount currencyCode}compareAtPrice{amount currencyCode}selectedOptions{name value}image{url altText}}}}options{name values}}}`;
shopifyFetch(PRODUCT_QUERY,{handle:SHOPIFY_CONFIG.product_handle}).then(data=>{
  if(!data.product){document.getElementById('buy-section').innerHTML='<p class="text-red-500">Prodotto non disponibile</p>';return;}
  const product=data.product;
  const variants=product.variants.edges.map(e=>e.node);
  let selectedVariantId=variants.length===1?variants[0].id:null;
  if(variants.length>1)renderVariantSelector(variants,product.options);
  updatePrice(variants[0]);
  document.getElementById('buy-button').addEventListener('click',()=>handleBuy(selectedVariantId));
}).catch(err=>{console.error('Product fetch error:',err);document.getElementById('buy-section').innerHTML='<p>Store temporaneamente non disponibile.</p>';});
```

### Cart API → Checkout
```javascript
const CART_CREATE=`mutation CartCreate($input:CartInput!){cartCreate(input:$input){cart{id checkoutUrl}userErrors{field message}}}`;
async function handleBuy(variantId){
  if(!variantId){highlightVariantSelector();return;}
  const btn=document.getElementById('buy-button');btn.textContent='Elaborazione...';btn.disabled=true;
  try{
    const qty=parseInt(document.getElementById('quantity')?.value||1);
    const data=await shopifyFetch(CART_CREATE,{input:{lines:[{merchandiseId:variantId,quantity:qty}]}});
    if(data.cartCreate.userErrors.length>0)throw new Error(data.cartCreate.userErrors.map(e=>e.message).join(', '));
    window.location.href=data.cartCreate.cart.checkoutUrl;
  }catch(err){console.error('Cart error:',err);btn.textContent='Buy Now';btn.disabled=false;}
}
```

### MAI usare
❌ `ShopifyBuy.buildClient()` / `client.checkout.create()` / `buy-button-storefront.min.js` — DEPRECATI
✅ `fetch()` diretto + `cartCreate` mutation + `checkoutUrl` redirect

Varianti: colori=swatch, taglie=pill button. Buy disabilitato senza selezione. Prezzo aggiornato per variante.

## Tracking Pixels
Includi SOLO se configurati. FB Pixel: init+PageView+AddToCart. TT Pixel: idem. GA: gtag.js+eventi.
Nessun pixel → niente tracking → niente cookie banner.

### Cookie Banner GDPR (SOLO se pixel attivi):
- 3 pulsanti con **stessa prominenza visiva**: "Accetta Tutti", "Rifiuta", "Personalizza"
- Nessun checkbox pre-selezionato, nessun scroll-consent o implied consent
- Pixel **bloccati** fino a consenso esplicito (injection dinamica script)
- Consenso in **localStorage** (NON sessionStorage) con versione e timestamp
- Link a cookie-policy.html nel banner
- Link "Gestisci Cookie" nel footer per riaprire il banner
- `z-index` superiore a sticky CTA
- Usa template pronto: `.agent/skills/legal-compliance/references/cookie-banner-template.html`

## Conformita Legale E-Commerce Italia
Per OGNI store generato, OBBLIGATORIO:

1. **4 pagine legali SEMPRE**: privacy-policy.html, cookie-policy.html, termini-condizioni.html, informativa-precontrattuale.html
2. **Usa i template pronti** in `.agent/skills/legal-compliance/references/` — NON riscrivere da zero
3. **Dati titolare** da `config/owner-data.json` (se non esiste, chiedi e crea)
4. **Dati obbligatori sul sito** (D.lgs. 70/2003 art. 7): ragione sociale, sede, P.IVA, email
5. **Footer**: P.IVA + link alle 4 pagine legali + "Gestisci Cookie"
6. **Piattaforma ODR**: abolita da Reg. UE 2024/3228 (marzo 2025) — NO riferimenti nei termini
7. **Leggi la skill** `legal-compliance` per istruzioni dettagliate e checklist

## Architettura Workspace e Deploy

### Questo Workspace è la "Fabbrica"
Il repo `ecommerce-generator` è il **tool di generazione** — contiene workflow, regole, skill, template e output generati. **NON va MAI deployato su Vercel.**

### 1 Store = 1 Repo GitHub = 1 Progetto Vercel
**REGOLA FONDAMENTALE**: Ogni store generato ha il proprio repo GitHub dedicato.
- Repo naming: `store-{brand-name}` (es. `store-vasca-ultrasuoni`, `store-mioaltrobrand`)
- MAI usare branch dello stesso repo per store diversi
- Vercel free = progetti illimitati → ogni repo = 1 URL (es. `store-vasca-ultrasuoni.vercel.app`)
- Dominio custom opzionale per ogni progetto Vercel

### Struttura Output (dentro ecommerce-generator)
```
output/stores/{brand-name-lowercase}/
├── index.html ← Store principale
├── product-{handle}.html ← (solo multi-prodotto)
├── privacy-policy.html ← Informativa Privacy GDPR
├── cookie-policy.html ← Cookie Policy
├── termini-condizioni.html ← Termini e Condizioni di Vendita
├── informativa-precontrattuale.html ← Informativa Precontrattuale
├── social-captions.md ← (interno, NON deployare)
└── store-info.json ← (interno, NON deployare)
```

### Flusso Deploy
1. Genera file in `output/stores/{brand}/`
2. Crea repo GitHub dedicato: `gh repo create store-{brand} --public --clone`
3. Copia nella root del repo: `index.html`, pagine legali, eventuali `product-*.html`
4. **NON includere** nel repo dello store: `social-captions.md`, `store-info.json`
5. Push su `main` → Vercel auto-deploya
6. Vercel settings: Framework "Other", Output Directory ".", nessun build command

**MAI**: ❌ Vercel API diretta ❌ `vercel deploy` CLI senza repo ❌ Deployare `ecommerce-generator` → ✅ Sempre GitHub repo dedicato → Vercel Git integration

## Errori da NON Commettere Mai
- MAI URL immagini inventati/placeholder, `{VARIABILE}` non sostituita, Lorem Ipsum
- MAI Buy Button non funzionante, meta tag SEO mancanti, contrasto insufficiente
- MAI generare senza analizzare nicchia/target/strategia, consegnare senza validazione
- MAI hotlink da marketplace cinesi, valuta sbagliata, hardcodare prezzo
- MAI stile non adatto alla nicchia, TUTTE le leve insieme, scarsità non credibile
- MAI JS Buy SDK, Checkout API, buy-button CDN — DEPRECATI
- MAI deploy Vercel senza GitHub

## Self-Learning
Dopo ogni store aggiorna `LEARNINGS.md`: strategie efficaci, errori corretti, pattern riutilizzabili, combinazioni nicchia→strategia. Prima di ogni nuovo store → leggi LEARNINGS.md.