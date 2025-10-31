# Piano di lavoro: Roadmap con Checkbox

## ✅ Fase 1: Creazione struttura iniziale (COMPLETATA)

- [x] Inizializzazione repository, licenza MIT, README.md e Git hooks tramite Husky
- [x] Configurazione Next.js + TypeScript + ESLint/Prettier: build e lint passano su commit
- [x] Installato e configurato Tailwind/PostCSS, definiti primi design tokens in `globals.css`
- [x] Struttura cartelle e alias path pronta: `src/app`, `src/components`, `src/lib`, alias in `tsconfig.json`
- [x] Creati layout.tsx, navbar, footer e home placeholder responsive in `src/app`

**Deliverable**: Repository con build e lint passanti; theme base; layout e home funzionanti.

---

## ✅ Fase 2: Creazione DB e utenti (COMPLETATA)

- [x] Selezione DB (SQLite per dev, PostgreSQL ready) e setup Prisma; variabili `DATABASE_URL`
- [x] Modellare `User`, `Role` e relazioni; eseguire migrazioni
- [x] Implementare auth email/password (NextAuth credentials); sessioni sicure
- [x] RBAC base (middleware, guardie su rotte/pagine)
- [x] Script seed admin iniziale + seed demo con dati fittizi

**Deliverable**: Schema DB migrato; login/logout operativi; aree protette per ruolo; admin creato.

**Nota**: OAuth (Google/Microsoft) verrà implementato come step finale (post-MVP).

---

## ✅ Fase 3: Definizione funzionalità evolutive (COMPLETATA)

- [x] Raccolta requisiti e stesura user stories con criteri di accettazione
- [x] Backlog con priorità (MoSCoW) e stima high-level
- [x] Definizione milestone trimestrali e Definition of Done
- [x] Mappatura flussi principali (documentazione)

**Deliverable**: Documento stories, backlog ordinato, roadmap e diagrammi di flusso.

---

## ✅ Fase 4: Make up grafico (COMPLETATA)

- [x] Definire design system (token, componenti base, stati e interazioni)
- [x] Costruire UI kit: `Button`, `Input`, `Card`, `Modal`, `Table` con varianti
- [x] Layout responsive e navigazione (header/sidebar/mobile menu) in `src/components` + `src/app`
- [x] Accessibilità base (contrasti, focus, aria-attributes)

**Deliverable**: UI kit riusabile, layout responsive e controlli accessibili pronti per integrazione.

---

## ✅ Fase 5: Finalizzazione prototipo (COMPLETATA)

- [x] Integrare flussi end-to-end (login → dashboard → navigazione base)
- [x] Test smoke e bugfix priorità alta (build produzione verificata)
- [x] Preparare demo script e seed di dati fittizi
- [x] Istruzioni di deploy (README, env di esempio, comandi build)
- [x] Creazione pagine base (campaigns, budget-requests, approvals, reports)
- [x] Form nuova richiesta budget (placeholder funzionante)

**Deliverable**: Prototipo dimostrabile stabile con guida di esecuzione/deploy.

---

## ✅ Fase 6: Core Functionality - CRUD Operations (COMPLETATA)

### API e Backend
- [x] Creare API route per nuova richiesta budget (`POST /api/budget-requests`)
- [x] Creare API route per lista richieste (`GET /api/budget-requests`)
- [x] Creare API route per dettaglio richiesta (`GET /api/budget-requests/[id]`)
- [x] Creare API route per aggiornare richiesta (`PUT /api/budget-requests/[id]`)
- [x] Creare API route per campagne (`GET /api/campaigns`)
- [x] Integrazione form nuova richiesta con API POST

### Frontend - Pagine da Popolare
- [x] Lista richieste budget con dati reali dal DB
- [x] Lista campagne con dati reali
- [x] Form nuova richiesta budget funzionante con validazione
- [ ] Dettaglio richiesta budget (visualizzazione/editing) - Opzionale per v1

**Deliverable**: CRUD completo per richieste budget e campagne operativo.

---

## ✅ Fase 7: Workflow Approvazioni (COMPLETATA)

### Stati e Transizioni
- [x] Implementare stati richiesta (PENDING_APPROVAL → APPROVED/REJECTED)
- [x] Logica di transizione stati nel backend (API PUT)
- [x] Azioni approva/rifiuta nel frontend
- [x] Pagina approvazioni con lista richieste in attesa

### Permessi e Visibilità
- [x] Base RBAC implementato (solo utenti autenticati)
- [ ] RBAC avanzato per approvazioni (chi può approvare) - Da implementare
- [ ] Filtri per ruolo (manager vede solo le proprie verticali) - Da implementare
- [ ] Notifiche quando richiesta richiede approvazione - Da implementare

**Deliverable**: Workflow approvazioni base completo e funzionante. RBAC avanzato rimandato a fase successiva.

---

## 🎨 Fase 8: UI/UX Enhancement

### Componenti Aggiuntivi
- [ ] Select/Dropdown per filtri
- [ ] DatePicker per selezioni date
- [ ] Loading states e skeleton loaders
- [ ] Toast/Notifications per feedback azioni
- [ ] Badge componenti per stati

### Paginazione e Filtri
- [ ] Paginazione tabelle (campagne, richieste)
- [ ] Filtri avanzati (canale, owner, stato, date range)
- [ ] Ricerca full-text su campagne e richieste
- [ ] Ordinamento colonne tabelle

**Deliverable**: UI/UX migliorata con componenti avanzati e filtri operativi.

---

## 📊 Fase 9: Export e Reporting

### Export Dati
- [ ] Export CSV allocazioni campagne
- [ ] Export CSV richieste budget
- [ ] Export PDF report dashboard
- [ ] Template export personalizzabili

### Report e Visualizzazioni
- [ ] Grafici trend spesa (chart library integration)
- [ ] Report dashboard personalizzabili
- [ ] Confronti periodi (periodo corrente vs precedente)
- [ ] Dashboard analytics avanzate

**Deliverable**: Sistema completo di export e report operativo.

---

## 🔐 Fase 10: Autenticazione Avanzata

### OAuth Providers
- [ ] Integrazione Azure AD / Entra ID
- [ ] OAuth Google (opzionale)
- [ ] Sincronizzazione ruoli da AD
- [ ] Migrazione utenti esistenti a OAuth

**Deliverable**: Autenticazione enterprise-ready con OAuth.

---

## 🔍 Fase 11: Audit e Sicurezza

### Logging e Audit
- [ ] Audit log modifiche budget
- [ ] Storico versioni richieste
- [ ] Tracciamento chi/modifica/cosa/quando
- [ ] Dashboard audit log per admin
- [ ] Export audit log

**Deliverable**: Sistema completo di audit e tracciabilità.

---

## 🔔 Fase 12: Notifiche e Comunicazioni

### Notifiche In-App
- [ ] Sistema notifiche per nuove approvazioni
- [ ] Badge contatori in menu
- [ ] Centro notifiche (dropdown/bell icon)
- [ ] Notifiche scadenze richieste

### Email (Opzionale)
- [ ] Email reminder scadenze
- [ ] Email conferma approvazioni
- [ ] Email notifica nuove richieste
- [ ] Template email personalizzabili

**Deliverable**: Sistema di notifiche operativo.

---

## ⚡ Fase 13: Performance e Ottimizzazione

### Ottimizzazioni
- [ ] Lazy loading componenti pesanti
- [ ] Caching query frequenti
- [ ] Ottimizzazione immagini/assets
- [ ] Code splitting ottimizzato
- [ ] Database indexing strategico

### Test
- [ ] Test unitari componenti critici
- [ ] Test E2E flussi principali
- [ ] Test performance (lighthouse score >90)
- [ ] Load testing API endpoints

**Deliverable**: Applicazione ottimizzata con test coverage adeguata.

---

## 🌐 Fase 14: Deploy e Infrastruttura

### Migrazione Database
- [ ] Migrazione a PostgreSQL/Azure SQL
- [ ] Migrazione dati da SQLite
- [ ] Setup connection pooling
- [ ] Backup automatizzati
- [ ] Disaster recovery plan

### Integrazioni Enterprise
- [ ] API REST/GraphQL per Power Platform
- [ ] Integrazione Power BI
- [ ] Integrazione Power Automate
- [ ] Webhook per eventi sistema
- [ ] Documentazione API completa

**Deliverable**: Infrastruttura produzione-ready con integrazioni enterprise.

---

## 📌 Stato Attuale del Progetto

### ✅ Completato
- [x] Struttura progetto Next.js completa
- [x] Autenticazione email/password funzionante
- [x] RBAC base implementato
- [x] UI Kit completo (Button, Input, Card, Modal, Table)
- [x] Layout responsive con sidebar
- [x] Dashboard con dati reali dal database
- [x] Seed script con dati demo
- [x] Navigazione funzionante (tutte le pagine create)
- [x] Form nuova richiesta budget (struttura pronta)
- [x] Documentazione completa (README, DEMO.md, DEPLOY.md)

### ✅ Completato di Recente
- [x] API CRUD complete per richieste budget
- [x] Form nuova richiesta integrato con backend
- [x] Lista richieste budget con dati reali
- [x] Lista campagne con dati reali
- [x] Workflow approvazioni base (approva/rifiuta)

### 🔄 In Corso
- [ ] Miglioramenti UX (loading states, error handling)

### 📋 Prossimi Step Prioritari
1. ✅ **P0 - Core Functionality**: Completato - API CRUD e pagine popolate
2. ✅ **P1 - Workflow Approvazioni**: Completato - Approvazioni base funzionanti
3. **P2 - UI Enhancement**: Aggiungere filtri, paginazione, notifiche
4. **P3 - RBAC Avanzato**: Implementare controlli permessi per approvazioni

---

## Note Generali

### Processo di Validazione
1. Code review obbligatoria per nuove feature
2. Test manuali su browser principali (Chrome, Firefox, Safari)
3. Build di produzione deve passare senza errori
4. Documentazione aggiornata per ogni nuova funzionalità

### Ambiente di Sviluppo
- **Database**: SQLite per sviluppo, PostgreSQL per produzione
- **Autenticazione**: NextAuth.js (v5) con credentials provider
- **UI Framework**: Next.js 16, React 19, Tailwind CSS 4
- **ORM**: Prisma 6

### Credenziali Demo
- **Admin**: `admin@example.com` / `admin123`
- **Demo Users**: Password `demo123` per tutti
  - `elena.ferri@digimax.mock`
  - `marco.neri@digimax.mock`
  - `chiara.bianchi@digimax.mock`
