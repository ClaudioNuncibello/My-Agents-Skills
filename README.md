# My Agent Skills

Collezione curata e definitiva di **Skill per Agenti AI** (Antigravity, Claude Code, Gemini CLI, Cursor). Questa libreria raccoglie le migliori discipline di ingegneria del software, modellazione di dominio e flussi di lavoro per progettare, specificare, implementare e revisionare progetti software con l'ausilio dell'Intelligenza Artificiale.

---

## 🏛️ Architettura della Libreria: Due Livelli

La cartella è organizzata su due livelli distinti ma complementari:

```
my-agent-skills/
├── skill-primitive/      ← Motori interni & discipline cognitive (Model-invoked)
└── skill/                ← Flussi di lavoro operativi & task-oriented (User & Model invoked)
```

1. **`skill-primitive/` (Fondamenta cognitive / Regole invisibili)**:
   - Non sono pensate per essere lanciate direttamente dall'utente per produrre un deliverable isolato.
   - Fungono da **disciplina interna** del modello AI durante il lavoro: ad esempio, come condurre un'intervista socratica senza deviare (`grilling`), come mantenere il glossario di business (`domain-modeling`), come scrivere codice tramite test prima del codice (`tdd`), o come progettare moduli profondi con API semplici (`codebase-design`).
   - Hanno `disable-model-invocation: false` (possono attivarsi da sole quando il modello riconosce il contesto).

2. **`skill/` (Skill operative / Workflow concreti)**:
   - Sono i punti di ingresso per l'utente (tramite `@nome-skill` o slash commands) o wrapper che orchestrano le primitive.
   - Ogni skill produce un **deliverable concreto**: un documento di specifiche (`to-spec`), una suddivisione in ticket (`to-tickets`), codice implementato e testato (`implement`), una revisione del codice (`code-review`), o un riassunto di handoff (`handoff`).

---

## 📋 Catalogo Completo delle Skill

### 1. Skill Primitive (`skill-primitive/`)

| Skill | Modalità di Invocazione | Scopo Pratico | Casi d'Uso Tipici |
| :--- | :--- | :--- | :--- |
| [`codebase-design`](./skill-primitive/codebase-design/SKILL.md) | **Model-invoked** (Autonoma) | Impone la filosofia dei *Deep Modules* di John Ousterhout: interfacce semplici che nascondono implementazioni potenti ed eliminano complessità. | Quando si progetta una nuova architettura, un modulo, un package o si pianifica un refactoring strutturale. |
| [`domain-modeling`](./skill-primitive/domain-modeling/SKILL.md) | **Model-invoked** (Autonoma) | Costruisce attivamente il glossario di business del progetto (`CONTEXT.md`) e registra le Architectural Decision Records (`docs/adr/`). | Quando si discutono requisiti, si definiscono entità e relazioni di dominio o si prendono decisioni architetturali difficili da invertire. |
| [`grilling`](./skill-primitive/grilling/SKILL.md) | **Model-invoked** (Autonoma) | Disciplina di interrogazione socratica implacabile: fa una domanda alla volta per scavare a fondo nei requisiti prima di scrivere codice. | Utilizzata come motore interno di intervista in fase di ideazione per eliminare ogni ambiguità o assunzione nascosta. |
| [`tdd`](./skill-primitive/tdd/SKILL.md) | **Model-invoked** (Autonoma) | Guida ferrea al Test-Driven Development (Red-Green-Refactor) con enfasi su test d'integrazione e mock minimi. | Durante la scrittura di qualsiasi componente logico, business logic o API per garantire correttezza e zero regressioni. |

---

### 2. Skill Operative (`skill/`)

| Skill | Modalità di Invocazione | Scopo Pratico | Casi d'Uso Tipici |
| :--- | :--- | :--- | :--- |
| [`grill-me`](./skill/grill-me/SKILL.md) | **User-invoked** (`@grill-me`) | Avvia una sessione interattiva di interrogatorio su un'idea o una feature prima di toccare il codice. | Ideale all'inizio di una task o quando hai un'idea vaga e vuoi che l'AI ti metta alle strette per chiarirla. |
| [`grill-with-docs`](./skill/grill-with-docs/SKILL.md) | **User-invoked** (`@grill-with-docs`) | Combina l'interrogatorio socratico con la produzione contestuale del glossario `CONTEXT.md` e degli ADR ufficiali. | Quando inizi un progetto nuovo o una feature complessa e vuoi lasciare una traccia formale per il team. |
| [`to-spec`](./skill/to-spec/SKILL.md) | **User-invoked** (`@to-spec`) | Converte una conversazione o una sessione di grilling in un documento di specifica formale e strutturato. | Subito dopo aver chiarito i requisiti, per ottenere un documento chiaro approvabile prima di scrivere codice. |
| [`to-tickets`](./skill/to-tickets/SKILL.md) | **User-invoked** (`@to-tickets`) | Scompone una specifica in ticket autonomi a fette verticali (*vertical slices*) ordinati per dipendenza. | Per trasformare una spec in task pratici, adatti a essere eseguiti uno alla volta in sessioni pulite. |
| [`implement`](./skill/implement/SKILL.md) | **User-invoked** (`@implement`) | Esegue un ticket o una specifica applicando TDD rigoroso, typechecking continuo e code-review finale. | Per la fase di codifica vera e propria: passi il ticket e lasci che l'agente lo implementi con standard elevati. |
| [`code-review`](./skill/code-review/SKILL.md) | **User / Model** (`@code-review`) | Revisiona il codice su due assi paralleli: correttezza funzionale (test, edge-case) e pulizia/design architettonico. | Al termine di una feature, prima di fare il commit/merge, o per fare il refactoring di codice esistente. |
| [`diagnosing-bugs`](./skill/diagnosing-bugs/SKILL.md) | **User / Model** (`@diagnosing-bugs`) | Protocollo scientifico per scovare bug sfuggenti tramite ciclo isolato: ipotesi → test riproducibile → fix minimo. | Quando un test fallisce inaspettatamente, c'è un comportamento anomalo o non si riesce a trovare la causa radice. |
| [`prototype`](./skill/prototype/SKILL.md) | **User-invoked** (`@prototype`) | Genera spike di codice rapido e usa-e-getta (UI o logica) per rispondere a dubbi tecnici di fattibilità. | Quando vuoi esplorare se una libreria o una soluzione UI funziona visivamente prima di impegnarti nell'architettura finale. |
| [`handoff`](./skill/handoff/SKILL.md) | **User-invoked** (`@handoff`) | Comprime l'intera sessione corrente in un riassunto denso e strutturato per la prossima chat o sessione. | A fine giornata, quando la chat diventa troppo lunga, o prima di riavviare l'agente per continuare il lavoro domani. |
| [`to-questionnaire`](./skill/to-questionnaire/SKILL.md) | **User-invoked** (`@to-questionnaire`) | Converte una decisione tecnica o di prodotto in un questionario a risposte multiple chiaro e compilabile. | Quando devi raccogliere feedback o scelte dal cliente finale o da colleghi non tecnici senza fargli leggere gergo tecnico. |
| [`research`](./skill/research/SKILL.md) | **User-invoked** (`@research`) | Esegue un'analisi approfondita di documentazione, pacchetti npm o standard di settore e produce un report sintetico. | Prima di scegliere una libreria o quando bisogna integrare un'API di terze parti poco conosciuta. |
| [`writing-for-agents`](./skill/writing-for-agents/SKILL.md) | **User / Reference** | Guida di riferimento per scrivere prompt, istruzioni e nuove skill formattate in modo che gli agenti non sbaglino. | Quando vuoi creare una nuova skill personalizzata o documentare convenzioni per il tuo agente. |

---

## 🔗 Workflow Completo Passo-Passo (Progettazione di un Software Generico)

Ecco il flusso di lavoro universale per **ideare, progettare, sviluppare e revisionare qualsiasi software**, dall'analisi iniziale dei requisiti al codice testato e collaudato.

```mermaid
flowchart TD
    subgraph Fase1["Fase 1: Analisi di Dominio & Requisiti"]
        A1["Tu scrivi:<br><code>@grill-with-docs</code>"] --> A2["L'AI interroga e formalizza:<br><code>grilling</code> + <code>domain-modeling</code>"]
        A2 --> A3["File generati:<br><code>CONTEXT.md</code> (glossario)<br><code>docs/adr/0001-...md</code> (decisioni)"]
    end

    subgraph Fase2["Fase 2: Specifiche & Decomposizione"]
        B1["Tu scrivi:<br><code>@to-spec</code>"] --> B2["L'AI genera l'architettura tecnica:<br><code>SPEC.md</code>"]
        B2 --> B3["Tu scrivi:<br><code>@to-tickets</code>"]
        B3 --> B4["File generati:<br><code>tickets/01-...md</code><br><code>tickets/02-...md</code>"]
    end

    subgraph Fase3["Fase 3: Sviluppo TDD & Qualità"]
        C1["Tu scrivi:<br><code>@implement tickets/01-...md</code>"] --> C2["L'AI applica:<br><code>tdd</code> + <code>codebase-design</code>"]
        C2 --> C3["File generati:<br><code>tests/...test.ts</code> (test prima)<br><code>src/...ts</code> (codice modulo)"]
        C3 --> C4["Tu scrivi:<br><code>@code-review</code>"]
    end

    subgraph Fase4["Fase 4: Chiusura & Consegna"]
        D1["Tu scrivi:<br><code>@handoff</code>"] --> D2["File generato:<br><code>HANDOFF.md</code>"]
    end

    Fase1 --> Fase2
    Fase2 --> Fase3
    Fase3 --> Fase4
```

---

### Step 1: Chiarire i Requisiti e Fissare i Termini (`@grill-with-docs`)

Prima di scrivere codice, metti l'AI in modalità "intervistatore implacabile" per eliminare ogni ambiguità nei requisiti, individuare i casi limite (*edge cases*) e formalizzare il vocabolario del software.

- **Cosa scrivi tu (Prompt):**
  ```text
  @grill-with-docs Devo progettare un nuovo software per [descrivi qui l'obiettivo o il problema che il software deve risolvere]. Fammi tutte le domande necessarie per chiarire i requisiti, sfidare le assunzioni e definire il vocabolario del dominio.
  ```
- **Cosa fa l'AI dietro le quinte:**
  - Attiva la primitiva `grilling`: ti interroga con una sola domanda alla volta su flussi principali, casi limite, fallimenti e vincoli tecnici.
  - Attiva la primitiva `domain-modeling`: man mano che i concetti chiave del software vengono chiariti, li registra formalmente.
- **File generati / modificati:**
  - 📄 [`CONTEXT.md`](./CONTEXT.md): Glossario ufficiale del software con entità, stati, regole e terminologia canonica (privo di codice, focalizzato sulle regole di business).
  - 📁 `docs/adr/0001-[decisione-architetturale].md`: Architectural Decision Record (ADR) che formalizza una scelta tecnica o architetturale non ovvia e difficile da invertire.

---

### Step 2: Trasformare l'Intervista in Specifica Tecnica (`@to-spec`)

Conclusa l'analisi dei requisiti, trasformi l'intera discussione in un documento formale di architettura e specifiche tecniche.

- **Cosa scrivi tu (Prompt):**
  ```text
  @to-spec Abbiamo chiarito tutti i requisiti e i vincoli. Ora genera il documento di specifica tecnica formale (SPEC.md) definendo architettura di sistema, contratti di interfaccia, modelli dati, flussi e criteri di accettazione.
  ```
- **Cosa fa l'AI:**
  Sintetizza i requisiti funzionali e non funzionali, i contratti di input/output, la gestione delle eccezioni e i criteri di collaudo in un documento strutturato.
- **File generati / modificati:**
  - 📄 [`SPEC.md`](./SPEC.md): Il documento tecnico di riferimento dell'intero progetto, pronto per essere approvato prima della fase di scrittura del codice.

---

### Step 3: Decomporre la Specifica in Ticket Autonomi (`@to-tickets`)

Un sistema software non si implementa in blocco: deve essere suddiviso in unità atomiche a fette verticali (*vertical slices*) ordinate per dipendenza.

- **Cosa scrivi tu (Prompt):**
  ```text
  @to-tickets Scomponi la SPEC.md in ticket di sviluppo autonomi a fette verticali, ordinati per dipendenza. Ogni ticket deve essere autosufficiente, implementabile e testabile in una singola sessione.
  ```
- **Cosa fa l'AI:**
  Analizza le dipendenze logiche tra i moduli e crea file separati per ciascun ticket con obiettivi chiari e criteri di accettazione.
- **File generati / modificati:**
  - 📁 `tickets/`
    - 📄 `tickets/01-[fondamenta-dati-e-storage].md`
    - 📄 `tickets/02-[logica-core-e-business-rules].md`
    - 📄 `tickets/03-[servizi-e-integrazioni].md`
    - 📄 `tickets/04-[interfaccia-pubblica-o-api].md`

---

### Step 4: Implementare un Ticket con TDD e Deep Modules (`@implement`)

Assegni all'agente un singolo ticket alla volta da sviluppare seguendo i massimi standard ingegneristici.

- **Cosa scrivi tu (Prompt):**
  ```text
  @implement Lavora sul ticket `tickets/01-[nome-ticket].md`. Applica TDD rigoroso: scrivi prima i test unitari e di integrazione per coprire casi ordinari ed edge cases, poi scrivi il codice minimo per farli passare.
  ```
- **Cosa fa l'AI dietro le quinte:**
  - Attiva `tdd`: scrive prima la suite di test che fallisce (**RED**), scrive l'implementazione minima necessaria affinché i test passino (**GREEN**), quindi pulisce il codice (**REFACTOR**).
  - Attiva `codebase-design`: progetta un modulo profondo (*Deep Module*) con un'interfaccia pubblica minimalista ed elegante che nasconde la complessità interna.
- **File generati / modificati:**
  - 📄 `tests/[modulo].test.ts`: Suite di test automatizzati per il modulo.
  - 📄 `src/[modulo].ts`: Codice sorgente del modulo.
  - 📄 `src/types.ts`: Definizioni dei tipi, interfacce e contratti pubblici.

---

### Step 5: Revisionare il Codice prima del Commit (`@code-review`)

Prima di considerare concluso il ticket ed eseguire il commit, effettui un controllo critico a due dimensioni.

- **Cosa scrivi tu (Prompt):**
  ```text
  @code-review Revisiona il codice implementato per il ticket prima di effettuare il commit. Verifica correttezza funzionale, assenza di regressioni, gestione degli errori e pulizia dell'architettura.
  ```
- **Cosa fa l'AI:**
  Revisiona il codice su due assi indipendenti:
  1. *Correttezza & Robustezza*: Verifica assenza di bug, memory leak, race condition e corretta gestione di tutti gli edge case.
  2. *Design & Semplicità*: Verifica che l'interfaccia non esponga dettagli interni non necessari (*information hiding*) e che rispetti la struttura del software.
- **File generati / modificati:**
  - Eventuali refactoring applicati direttamente al codice sorgente e semaforo verde per il commit Git.

---

### Step 6: Congelare lo Stato per la Prossima Sessione (`@handoff`)

A fine giornata o quando la finestra di contesto della chat diventa satura, generi un passaggio di consegne ordinato per riprendere senza attrito.

- **Cosa scrivi tu (Prompt):**
  ```text
  @handoff Abbiamo completato e testato con successo il ticket. Prepara un handoff completo per consentire a una nuova sessione di riprendere direttamente dal ticket successivo.
  ```
- **Cosa fa l'AI:**
  Sintetizza in modo compatto le decisioni prese, lo stato dei file, i test che passano e la prossima azione da intraprendere.
- **File generati / modificati:**
  - 📄 [`HANDOFF.md`](./HANDOFF.md) (oppure testo di handoff pronto per la chat successiva con riepilogo e puntamento ai file di lavoro).

---

## 🛠️ Flussi Secondari per Situazioni Specifiche

Durante il ciclo di vita del software possono verificarsi situazioni non lineari. Ecco come gestirle:

### A. Decisione Tecnica o di Progetto da Condividere (`@to-questionnaire`)
- **Situazione**: Devi prendere una decisione tra più opzioni (tecniche, architetturali o di prodotto) e vuoi raccogliere pareri o far decidere altri stakeholder senza affogarli nel gergo.
- **Prompt:**
  ```text
  @to-questionnaire Dobbiamo scegliere tra diverse opzioni per [argomento della decisione]. Prepara un questionario chiaro a scelte multiple, spiegando pro, contro e implicazioni in termini accessibili.
  ```
- **File generato:** `docs/QUESTIONARIO-[ARGOMENTO].md`.

### B. Bug Complesso o Regressione Inaspettata (`@diagnosing-bugs`)
- **Situazione**: Il software si comporta in modo anomalo o un test fallisce senza una causa evidente.
- **Prompt:**
  ```text
  @diagnosing-bugs Il software presenta un comportamento anomalo quando [descrivi il problema o l'errore]. Applica il metodo scientifico di diagnosi: formula le ipotesi, crea un test minimo isolato che riproduce il bug ed esegui il fix mirato.
  ```
- **File generati:** `tests/reproduce-[bug].test.ts` e fix mirato.

### C. Prototipo Rapido di Fattibilità Tecnica (`@prototype`)
- **Situazione**: Vuoi verificare rapidamente una libreria esterna, un algoritmo o una tecnologia prima di impegnarti nell'architettura finale.
- **Prompt:**
  ```text
  @prototype Crea uno spike rapido usa-e-getta per verificare la fattibilità di [tecnologia/algoritmo/componente]. Non implementare architetture complesse, solo codice minimo per testare il funzionamento.
  ```
- **File generati:** `src/prototypes/[nome-spike].ts`.

---

## 🚀 Come Installare e Usare le Skill

### 1. Uso Locale per un Singolo Progetto (Consigliato)
Copia le skill desiderate nella cartella `.agents/skills/` del repository su cui stai lavorando:

```bash
# Esempio all'interno del tuo progetto:
mkdir -p .agents/skills/
cp -r /percorso/a/my-agent-skills/skill/grill-me .agents/skills/
cp -r /percorso/a/my-agent-skills/skill-primitive/grilling .agents/skills/
```

### 2. Uso Globale su Antigravity IDE (Disponibile in tutti i progetti)
Se desideri avere queste skill sempre pronte in qualunque workspace su Antigravity:
- Copia le cartelle all'interno di:
  `C:\Users\<TuoUtente>\.gemini\config\skills\`

### 3. Come Richiamarle in Chat
- Nelle chat di **Antigravity**, digita semplicemente `@` per visualizzare il completamento automatico delle skill disponibili (es. `@grill-me`, `@to-spec`, `@implement`).
- Le skill primitive come `domain-modeling`, `tdd` o `codebase-design` verranno lette e rispettate automaticamente dall'agente ogni volta che il contesto operativo lo richiede.
