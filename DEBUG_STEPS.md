# Debug Steps - "Failed to fetch budget requests"

## Modifiche Applicate

### 1. Logging Dettagliato in API Route
**File**: `src/app/api/budget-requests/route.ts`

Aggiunto logging per:
- Cookie ricevuti (numero e nome)
- Cookie di autenticazione trovato
- Headers (Authorization e Cookie)
- Dettagli sessione
- Errori dettagliati con stack trace

### 2. Configurazione Auth Semplificata
**File**: `src/lib/auth.ts`

Rimossa configurazione personalizzata dei cookie (NextAuth v5 la gestisce automaticamente).

### 3. Endpoint di Test Creati

#### `/api/auth/test` - Test Autenticazione
Verifica:
- Presenza cookie
- Stato autenticazione
- Dettagli sessione
- Configurazione AUTH_SECRET

#### `/api/db/test` - Test Database
Verifica:
- Connessione database
- DATABASE_URL configurato
- Conteggio record (utenti, richieste budget)

## Passaggi per il Debugging

### Step 1: Verificare il Server è in Esecuzione
```bash
cd digimax-budget-marketing
npm run dev
```

### Step 2: Eseguire il Test del Database
Apri il browser e vai a: `http://localhost:3000/api/db/test`

**Cosa controllare:**
- ✅ `success: true`
- ✅ `databaseUrl` è impostato
- ✅ `userCount` > 0 (almeno l'admin)
- ✅ `budgetRequestCount` mostra il numero di richieste

**Se fallisce:**
- Verifica che `DATABASE_URL` sia impostato correttamente
- Verifica che il file `prisma/dev.db` esista
- Esegui `npm run db:seed:demo` se necessario

### Step 3: Eseguire il Test di Autenticazione (Senza Login)
Apri il browser e vai a: `http://localhost:3000/api/auth/test`

**Cosa controllare:**
- ✅ `authenticated: false` (normale se non loggato)
- ✅ `hasCookies: false` o `cookieCount: 0`
- ✅ `authSecret: "Set"` (non "Missing")

### Step 4: Effettuare il Login
1. Vai a `http://localhost:3000/signin`
2. Login con: `admin@example.com` / `admin123`
3. Dopo il login, verifica i cookie:
   - Apri DevTools (F12)
   - Vai su Application → Cookies → `http://localhost:3000`
   - Cerca cookie che contengono "auth" o "session"
   - Dovresti vedere un cookie tipo `authjs.session-token`

### Step 5: Test Autenticazione Dopo Login
Dopo il login, vai a: `http://localhost:3000/api/auth/test`

**Cosa controllare:**
- ✅ `authenticated: true`
- ✅ `hasCookies: true`
- ✅ `session.user.email` corrisponde all'utente loggato
- ✅ `session.user.id` è presente

**Se `authenticated: false` dopo il login:**
- I cookie non vengono impostati correttamente
- Verifica che `AUTH_SECRET` sia impostato
- Potrebbe essere un problema con NextAuth v5 beta

### Step 6: Test Budget Requests Endpoint
Dopo il login, vai a: `http://localhost:3000/budget-requests`

**Cosa controllare nel Terminale Server:**
```
GET /api/budget-requests - Starting
DATABASE_URL: file:/path/to/prisma/dev.db
Cookies received: X cookies
Auth cookie found: authjs.session-token (XXX chars)  ← DEVE essere presente
Cookie header: XXX chars  ← DEVE essere presente
Session retrieved: Yes  ← DEVE essere Yes
Session user: admin@example.com
Session user ID: X
Querying database...
Database query successful, found X requests
```

**Se vedi "No session found":**
- I cookie non vengono inviati con la richiesta
- Verifica che `credentials: "include"` sia presente nella fetch (già aggiunto)
- Potrebbe essere necessario riavviare il server

**Se vedi un errore database:**
- Controlla i log per il messaggio di errore specifico
- Verifica che `DATABASE_URL` sia corretto
- Verifica che il database esista e sia accessibile

### Step 7: Controllare la Console del Browser
Apri DevTools (F12) → Console e vai a `/budget-requests`

**Cosa controllare:**
- Se vedi errori CORS: problema di configurazione
- Se vedi errori 401: autenticazione non funziona
- Se vedi errori 500: problema lato server (guarda i log del terminale)

## Problemi Comuni e Soluzioni

### Problema: "No session found" dopo il login
**Possibili cause:**
1. Cookie non vengono impostati durante il login
   - **Soluzione**: Verifica che `AUTH_SECRET` sia impostato
   - Riavvia il server dev
2. Cookie non vengono inviati con le richieste
   - **Soluzione**: Già aggiunto `credentials: "include"` nelle fetch
3. NextAuth v5 beta ha un bug
   - **Soluzione**: Prova ad aggiornare `next-auth` alla versione più recente

### Problema: Errore Database
**Possibili cause:**
1. Percorso database relativo
   - **Soluzione**: Già fixato in `src/lib/db.ts` (usa percorso assoluto)
2. Database non inizializzato
   - **Soluzione**: Esegui `npm run db:seed:demo`
3. Permessi file database
   - **Soluzione**: Verifica che il file `prisma/dev.db` abbia permessi di lettura/scrittura

### Problema: Cookie non vengono trovati
**Possibili cause:**
1. Cookie vengono impostati su un dominio/path diverso
   - **Soluzione**: Verifica i cookie in DevTools → Application → Cookies
2. Cookie vengono cancellati
   - **Soluzione**: Non usare modalità incognito per il test

## Comandi Utili

```bash
# Avvia il server dev
npm run dev

# Inizializza il database con dati demo
npm run db:seed:demo

# Resetta il database
npm run db:reset

# Genera Prisma client
npm run prisma:generate
```

## Next Steps

Dopo aver eseguito tutti i test sopra:
1. Verifica i log nel terminale quando accedi a `/budget-requests`
2. Identifica quale step fallisce
3. Condividi i log per ulteriore assistenza

Se tutti i test passano ma l'errore persiste, potrebbe essere necessario:
- Aggiornare NextAuth v5 alla versione più recente
- Verificare se ci sono problemi noti con NextAuth v5 beta + Next.js 16
- Considerare di passare temporaneamente a NextAuth v4 per confronto

