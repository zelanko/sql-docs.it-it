---
title: Impostazioni (conversione) (DB2ToSQL) del progetto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 538c93cf-c5bb-43d5-b758-186d9fb00c19
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a446fd4ce116ee19aa8b38d1ae6d8213e35c16e1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273022"
---
# <a name="project-settings-conversion-db2tosql"></a>Impostazioni progetto (conversione) (DB2ToSQL)
La pagina di conversione del **impostazioni del progetto** finestra di dialogo contiene impostazioni che consentono di personalizzare la modalità SSMA Converte la sintassi di DB2 per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintassi.  
  
Nel riquadro di conversione è disponibile nel **impostazioni del progetto** e **impostazioni di progetto predefinite** finestre di dialogo:  
  
-   Per specificare le impostazioni per tutti i progetti SSMA, il **strumenti** menu fare clic su **impostazioni di progetto predefinite**, selezionare tipo di progetto di migrazione per i quali impostazioni sono necessarie per essere visualizzati o modificati da  **Versione di destinazione della migrazione** elenco a discesa, quindi fare clic su **generali** nella parte inferiore del riquadro a sinistra e quindi fare clic su **conversione**.  
  
-   Per specificare le impostazioni per il progetto corrente, il **strumenti** menu fare clic su **le impostazioni del progetto**, quindi fare clic su **generale** nella parte inferiore del riquadro di sinistra e quindi fare clic su **Conversione**.  
  
## <a name="conversion-messages"></a>Conversione dei messaggi  
  
### <a name="generate-messages-about-issues-applied"></a>Generare i messaggi sui problemi applicati  
Specifica se SSMA genera messaggi informativi durante la conversione, li visualizza nel riquadro di Output e li aggiunge al codice convertito.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** No  
  
**Modalità completa:** No  
  
## <a name="miscellaneous-options"></a>Opzioni varie  
  
### <a name="cast-rownum-expressions-as-integers"></a>Espressioni ROWNUM cast come numeri interi  
Quando SSMA converte le espressioni ROWNUM, l'espressione viene convertita in una clausola TOP, seguita dall'espressione. L'esempio seguente illustra ROWNUM in un'istruzione DB2 DELETE:  
  
`DELETE FROM Table1`  
  
`WHERE ROWNUM < expression and Field1 >= 2`  
  
L'esempio seguente mostra l'oggetto risultante [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
`DELETE TOP (expression-1)`  
  
`FROM Table1`  
  
`WHERE Field1>=2`  
  
La parte superiore è necessario che l'espressione di clausole TOP restituisce un numero intero. Se il valore integer è negativo, l'istruzione genererà un errore.  
  
-   Se si seleziona **Sì**, SSMA viene eseguito il cast dell'espressione come un numero intero.  
  
-   Se si seleziona **No**, SSMA contrassegnerà tutte le espressioni non integer come un errore nel codice convertito.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/Full:** No  
  
**Ottimistica modalità:** Yes  
  
### <a name="default-schema-mapping"></a>Mapping dello Schema predefinito  
Questa impostazione specifica come vengono eseguito il mapping degli schemi DB2 a schemi SQL Server. Sono disponibili in questa impostazione di due opzioni:  
  
1.  **Schema di database:** In questo schema DB2 in modalità 'sch1' verrà mappato per impostazione predefinita allo schema di SQL Server 'dbo' nel database di SQL Server 'sch1'.  
  
2.  **Schema allo schema:** In questa modalità DB2 lo schema 'sch1' verrà mappato per impostazione predefinita allo schema di SQL Server 'sch1' nel database di SQL Server predefinito fornito nella finestra di dialogo di connessione.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Schema di database  
  
### <a name="conversion-ways-of-merge-statement"></a>Modalità di conversione dell'istruzione MERGE  
  
-   Se si seleziona **utilizzo dell'istruzione INSERT, UPDATE, istruzione DELETE**, SSMA Converte l'istruzione merge in INSERT, UPDATE, DELETE istruzioni.  
  
-   Se si seleziona **istruzione utilizzando MERGE**, SSMA Converte l'istruzione merge in istruzione MERGE in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!WARNING]  
> Questa opzione di impostazione di progetto è disponibile solo in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Usando l'istruzione MERGE  
  
### <a name="convert-calls-to-subprograms-that-use-default-arguments"></a>Convertire le chiamate a sottoprogrammi che usano argomenti predefiniti  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] le funzioni non supportano l'omissione dei parametri nella chiamata di funzione. Inoltre, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedure e funzioni non supportano le espressioni come valori di parametro predefiniti.  
  
-   Se si seleziona **Yes** e una chiamata di funzione vengono omessi parametri, SSMA inserirà la parola chiave **predefinita** in funzione e chiamata nella posizione corretta. Quindi, contrassegnerà la chiamata con un avviso.  
  
-   Se si seleziona **No**, SSMA contrassegnerà le chiamate di funzione come errori.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Yes  
  
### <a name="convert-count-function-to-countbig"></a>Converti la funzione COUNT in COUNT_BIG  
Se le funzioni di conteggio sono probabile che restituire i valori maggiori di 2.147.483.647, ovvero 2<sup>31</sup>-1, è necessario convertire le funzioni di COUNT_BIG.  
  
-   Se si seleziona **Sì**, SSMA convertirà tutti gli usi del conteggio di COUNT_BIG.  
  
-   Se si seleziona **No**, le funzioni rimarrà come conteggio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà restituito un errore se la funzione restituisce un valore maggiore di 2<sup>31</sup>-1.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/Full:** Yes  
  
**Ottimistica modalità:** no  
  
### <a name="convert-forall-statement-to-while-statement"></a>Convertire FORALL istruzione WHILE istruzione  
Definisce il modo SSMA tratterà cicli FORALL sugli elementi della raccolta PL/SQL.  
  
-   Se si seleziona **Sì**, SSMA consente di creare un ciclo WHILE in cui gli elementi della raccolta vengono recuperati uno alla volta.  
  
-   Se si seleziona **No**, SSMA genera un set di righe dalla raccolta utilizzando metodo nodes () e lo usa come una singola tabella. Questo è più efficiente, ma rende meno leggibile il codice di output.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** No  
  
**Modalità completa:** Yes  
  
### <a name="convert-foreign-keys-with-set-null-referential-action-on-column-that-is-not-null"></a>Convertire le chiavi esterne con operazione referenziale SET NULL nella colonna che è non NULL  
DB2 consente la creazione di vincoli di chiave esterna, in cui un'operazione SET NULL può non essere adottata perché non sono consentiti valori null nella colonna di riferimento. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta tale configurazione della chiave esterna.  
  
-   Se si seleziona **Yes**, SSMA genererà referenziali come in DB2, ma è necessario apportare modifiche manuali prima di caricare il vincolo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ad esempio, è possibile scegliere NO ACTION anziché SET NULL.  
  
-   Se si seleziona **No**, il vincolo verrà contrassegnato come errore.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** No  
  
### <a name="convert-function-calls-to-procedure-calls"></a>Convertire le chiamate di funzione per le chiamate di procedura  
Alcune funzioni di DB2 sono definite come transazioni autonomi o contenere istruzioni che non è valide in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In questi casi, SSMA consente di creare una procedura e una funzione che è un wrapper per la procedura. La funzione convertita chiama la procedura di implementazione.  
  
SSMA è possibile convertire le chiamate alla funzione wrapper in chiamate alla procedura. Ciò consente di creare codice più leggibile e può migliorare le prestazioni. Tuttavia, il contesto non sempre consente ad esempio, è possibile sostituire una chiamata di funzione nell'elenco SELECT con una chiamata di routine. SSMA presenta alcune opzioni per coprire i casi comuni:  
  
-   Se si seleziona **sempre**, SSMA tenta di convertire le chiamate di funzione wrapper in chiamate di procedura. Se il contesto corrente non supporta questa conversione, viene generato un messaggio di errore. In questo modo, non le chiamate di funzione vengono lasciate nel codice generato.  
  
-   Se si seleziona **quando possibile**, SSMA rende un'operazione di spostamento per le chiamate di procedura solo se la funzione ha parametri di output. Quando lo spostamento non è possibile, viene rimossa l'attributo di output del parametro. In tutti gli altri casi SSMA lascia le chiamate di funzione.  
  
-   Se si seleziona **Never**, SSMA lascerà tutte le chiamate di funzione come chiamate di funzione. In alcuni casi questa scelta potrebbe essere accettabile a causa di motivi di prestazioni.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Quando possibile  
  
### <a name="convert-lock-table-statements"></a>Convertire le istruzioni di blocco tabella  
SSMA è possibile convertire molte istruzioni di blocco TABLE in hint di tabella. SSMA non è possibile convertire qualsiasi istruzione di blocco nella tabella che contengono partizioni, parte, @dblinke le clausole NOWAIT e verranno contrassegnate come tali istruzioni con messaggi di errore di conversione.  
  
-   Se si seleziona **Sì**, SSMA convertirà supportate le istruzioni di blocco TABLE in hint di tabella.  
  
-   Se si seleziona **No**, SSMA contrassegnerà tutte le istruzioni di blocco nella tabella con i messaggi di errore di conversione.  
  
Nella tabella seguente viene illustrato come SSMA converte le modalità di blocco DB2:  
  
|||  
|-|-|  
|DB2 Modalità di blocco|Hint di tabella SQL Server|  
|CONDIVISIONE DI RIGA|ROWLOCK, HOLDLOCK|  
|RIGA ESCLUSIVO|HOLDLOCK ROWLOCK, XLOCK,|  
|SHARE UPDATE = RIGA CONDIVISIONE|ROWLOCK, HOLDLOCK|  
|CONDIVIDI|TABLOCK, HOLDLOCK|  
|CONDIVISIONE DI RIGA ESCLUSIVO|HOLDLOCK TABLOCK, XLOCK,|  
|ESCLUSIVO|TABLOCKX, HOLDLOCK|  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Yes  
  
### <a name="convert-open-for-statements-for-ref-cursor-out-parameters"></a>Convertire le istruzioni di OPEN FOR per i parametri REF CURSOR OUT  
In DB2, l'istruzione OPEN-FOR è utilizzabile per restituire un set di risultati a un parametro OUT di tipo REF CURSOR del sottoprogramma. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], le stored procedure restituire direttamente i risultati delle istruzioni SELECT.  
  
SSMA è possibile convertire numerose istruzioni OPEN FOR in istruzioni SELECT.  
  
-   Se si seleziona **Sì**, SSMA Converte l'istruzione OPEN FOR in un'istruzione SELECT, che restituisce il set di risultati al client.  
  
-   Se si seleziona **No**, SSMA genererà un messaggio di errore nel codice convertito e nel riquadro di Output.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Yes  
  
### <a name="convert-record-as-a-list-of-separates-variables"></a>Convertire i record come un elenco di variabili separa  
SSMA è possibile convertire i record di DB2 in separa le variabili e le variabili XML con struttura specifica.  
  
-   Se si seleziona **Sì**, SSMA converte il record in un elenco di variabili separa quando possibile.  
  
-   Se si seleziona **No**, SSMA converte il record in variabili XML con struttura specifica.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Yes  
  
### <a name="convert-substr-function-calls-to-substring-function-calls"></a>Convertire le chiamate di funzione SUBSTR alle chiamate di funzione SUBSTRING  
SSMA è possibile convertire le chiamate di funzione SUBSTR DB2 in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sottostringa** chiamate, a seconda del numero di parametri di funzione. Se SSMA non è possibile convertire una chiamata di funzione SUBSTR o il numero di parametri non è supportato, SSMA convertirà la chiamata di funzione SUBSTR in una chiamata di funzione SSMA personalizzata.  
  
-   Se si seleziona **Yes**, SSMA convertirà chiamate di funzione SUBSTR che usano tre parametri in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sottostringa**. Altre funzioni SUBSTR verranno convertiti per chiamare la funzione SSMA personalizzata.  
  
-   Se si seleziona **No**, SSMA convertirà la chiamata di funzione SUBSTR in una chiamata di funzione SSMA personalizzata.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Yes  
  
**Modalità completa:** No  
  
### <a name="convert-subtypes"></a>Convertire sottotipi  
SSMA è possibile convertire i sottotipi di PL/SQL in due modi:  
  
-   Se si seleziona **Yes**, creerà SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definite dall'utente tipo da un sottotipo e usarlo per ogni variabile del sottotipo.  
  
-   Se si seleziona **No**, SSMA verrà sostituire tutte le dichiarazioni di origine del sottotipo di con il tipo sottostante e convertire il risultato come di consueto. In questo caso, non tipi aggiuntivi vengono creati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** No  
  
### <a name="convert-synonyms"></a>Converte i sinonimi  
I sinonimi per gli oggetti di DB2 seguenti possono essere migrati a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Le tabelle e oggetti  
  
-   Le viste e le viste di oggetti  
  
-   Funzioni e stored procedure  
  
-   Viste materializzate  
  
I sinonimi per gli oggetti di DB2 seguenti possono essere sostituiti da riferimenti diretti agli oggetti:  
  
-   Sequenze  
  
-   Pacchetti  
  
-   Oggetti dello schema di classe Java  
  
-   Tipi di oggetto definito dall'utente  
  
Impossibile eseguire la migrazione di altri sinonimi. SSMA genera messaggi di errore per il sinonimo e a tutti i riferimenti che usano il sinonimo.  
  
-   Se si seleziona **Yes**, verrà creato SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sinonimi e riferimenti a oggetti diretti in base all'elenco precedente incluse.  
  
-   Se si seleziona **No**, SSMA creerà riferimenti a oggetti diretti per tutti i sinonimi elencati di seguito.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Yes  
  
### <a name="convert-tochardate-format"></a>Convertire TO_CHAR (date, formato)  
SSMA è possibile convertire TO_CHAR(date, format) DB2 in procedure dal database sysdb.  
  
-   Se si seleziona **funzione usando TO_CHAR_DATE**, SSMA converte TO_CHAR (date, formato) in TO_CHAR_DATE funzioni usando della lingua inglese per la conversione.  
  
-   Se si seleziona **funzione usando TO_CHAR_DATE_LS (NLS care)**, SSMA converte TO_CHAR (date, formato) in TO_CHAR_DATE_LS funzioni usando della lingua di sessione per la conversione  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Tramite la funzione TO_CHAR_DATE  
  
**Modalità completa:** Tramite la funzione TO_CHAR_DATE_LS (NLS care)  
  
### <a name="convert-transaction-processing-statements"></a>Convertire le istruzioni di elaborazione delle transazioni  
SSMA è possibile convertire le istruzioni di elaborazione delle transazioni DB2:  
  
-   Se si seleziona **Yes**, SSMA converte le istruzioni di elaborazione delle transazioni DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istruzioni.  
  
-   Se si seleziona **No**, SSMA contrassegna la transazione di elaborazione di istruzioni come errori di conversione.  
  
> [!NOTE]  
> DB2 viene aperto in modo implicito le transazioni. Per emulare questo comportamento nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario aggiungere manualmente le istruzioni BEGIN TRANSACTION in cui si desidera avviare le transazioni. In alternativa, è possibile eseguire il comando SET IMPLICIT_TRANSACTIONS ON all'inizio della sessione. SSMA SET IMPLICIT_TRANSACTIONS ON viene aggiunto automaticamente durante la conversione di subroutine con transazioni autonomi.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Yes  
  
### <a name="emulate-db2-null-behavior-in-order-by-clauses"></a>Emulare il comportamento di null DB2 in clausole ORDER BY  
I valori NULL vengono ordinati in modo diverso in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e DB2:  
  
-   In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], NULL i valori sono i valori più bassi in un elenco ordinato. In un elenco in ordine crescente, verranno visualizzati per primi i valori NULL.  
  
-   In DB2, i valori NULL sono i valori più alti in un elenco ordinato. Per impostazione predefinita, i valori NULL visualizzato per ultimi in un elenco in ordine crescente.  
  
-   DB2 include le clausole di valori null e valori null cognome, che consente di modificare la modalità DB2 Ordina i valori null.  
  
SSMA è possibile emulare DB2 ORDER BY comportamento tramite il controllo dei valori NULL. Quindi prima di tutto gli ordini di valori NULL nell'ordine specificato e quindi ordini da altri valori.  
  
-   Se si seleziona **Sì**, SSMA convertirà l'istruzione di DB2 in modo che emula il comportamento di DB2 ORDER BY.  
  
-   Se si seleziona **No**, SSMA ignorerà le regole di DB2 e generare un messaggio di errore quando rileva le clausole di valori null e valori null cognome.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** No  
  
**Modalità completa:** Yes  
  
### <a name="emulate-row-count-exceptions-in-select"></a>Emulare le eccezioni di conteggio righe in SELECT  
Se un'istruzione SELECT con una clausola INTO non restituisce alcuna riga, DB2 genera un'eccezione NO_DATA_FOUND. Se l'istruzione restituisce due o più righe, viene generato l'eccezione TOO_MANY_ROWS. L'istruzione convertita in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non genera alcuna eccezione se il conteggio delle righe è diverso da uno.  
  
-   Se si seleziona **Sì**, SSMA aggiunge chiamata a sysdb procedure db_error_exact_one_row_check dopo ogni istruzione SELECT. Questa procedura emula le eccezioni NO_DATA_FOUND e TOO_MANY_ROWS. Questo è il valore predefinito e consente di riprodurre il comportamento di DB2 più vicino possibile. È necessario selezionare sempre **Sì** se il codice sorgente ha gestori delle eccezioni che elaborano questi errori. Si noti che se l'istruzione SELECT si verifica all'interno di una funzione definita dall'utente, questo modulo verrà convertito in una stored procedure, in quanto l'esecuzione di stored procedure e la generazione di eccezioni non è compatibile con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contesto (funzione).  
  
-   Se si seleziona **No**, non verranno generata alcuna eccezione. Che può essere utile quando SSMA converte una funzione definita dall'utente e si desidera rimanga in una funzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Yes  
  
### <a name="generate-error-for-dbmssqlparse"></a>Genera l'errore per DBMS_SQL. ANALISI  
  
-   Se si seleziona **errore**, SSMA genera l'errore in corrispondenza la conversione DBMS_SQL. L'ANALISI.  
  
-   Se si seleziona **avviso**, SSMA Genera avviso per la conversione DBMS_SQL. L'ANALISI.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Errore  
  
### <a name="generate-rowid-column"></a>Genera colonna ROWID  
Quando vengono create tabelle in SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile creare una colonna ROWID. Quando viene eseguita la migrazione dei dati, ogni riga Ottiene un nuovo valore UNIQUEIDENTIFIER generato dalla funzione NEWID ().  
  
-   Se si seleziona **Yes**, la colonna ROWID viene creata in tutte le tabelle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] genera i GUID quando si inseriscono i valori. Scegliere sempre **Sì** se si prevede di usare il Tester di SSMA.  
  
-   Se si seleziona **No**, ROWID non vengono aggiunte alle tabelle.  
  
-   **Aggiungere la colonna ROWID per le tabelle con trigger** aggiungere ROWID per le tabelle contenenti i trigger.  
  
> [!WARNING]  
> Impostazione predefinita nel caso di SQL Server 2005, SQL Server 2008 e SQL Server 2012 e 2014 **colonna ROWID aggiungere tabelle con trigger**.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Aggiungere la colonna ROWID per le tabelle con trigger  
  
**Modalità completa:** Yes  
  
### <a name="generate-unique-index-on-rowid-column"></a>Generare un indice univoco sulla colonna ROWID  
Specifica se SSMA genera colonne di indice univoco sulla colonna ROWID generato o non. Se l'opzione è impostata su "Sì", l'indice univoco viene generato e se è impostata su "NO", indice univoco non viene generato nella colonna ROWID.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Yes  
  
### <a name="local-modules-conversion"></a>Conversione di moduli locali  
Definisce il tipo di conversione sottoprogramma (dichiarato in autonomi stored procedure o funzioni) DB2 annidati.  
  
-   Se si seleziona **Inline**, le chiamate nidificate sottoprogramma verranno sostituite con il relativo corpo.  
  
-   Se si seleziona **Stored procedure**sottoprogramma nidificato verrà convertito in una stored procedure SQL Server e verranno sostituite le chiamate a questa chiamata di procedura.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Inline  
  
### <a name="use-isnull-in-string-concatenation"></a>Utilizzare ISNULL nella concatenazione di stringhe  
DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituiscono risultati diversi quando concatenazioni di stringhe includono i valori NULL. DB2 considera il valore NULL, ad esempio un set di caratteri vuota. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Restituisce NULL.  
  
-   Se si seleziona **Yes**, SSMA sostituisce il carattere di concatenazione di DB2 (|) con i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carattere di concatenazione (+). SSMA controlla anche le espressioni su entrambi i lati della concatenazione dei valori NULL.  
  
-   Se si seleziona **No**, SSMA sostituisce i caratteri di concatenazione, ma non controlla i valori NULL.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
### <a name="use-isnull-in-replace-function-calls"></a>Utilizzare ISNULL nelle chiamate di funzione REPLACE  
Istruzione ISNULL viene usato nelle chiamate di funzione REPLACE per emulare il comportamento di DB2. Le opzioni seguenti sono disponibili per questa impostazione:  
  
-   YES  
  
-   No  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** no  
  
**Modalità completa:** Yes  
  
### <a name="use-isnull-in-concat-function-calls"></a>Utilizzare ISNULL nelle chiamate di funzione CONCAT  
Istruzione ISNULL viene usato nelle chiamate di funzione CONCAT per emulare il comportamento di DB2. Le opzioni seguenti sono disponibili per questa impostazione:  
  
-   YES  
  
-   No  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** No  
  
**Modalità completa:** Yes  
  
### <a name="use-native-convert-function-when-possible"></a>Utilizzare la funzione di conversione nativa quando possibile  
  
-   Se si seleziona **Sì**, SSMA converte TO_CHAR (date, formato) nella funzione di conversione nativa quando possibile.  
  
-   Se si seleziona **No**, SSMA converte TO_CHAR (date, formato) in TO_CHAR_DATE o TO_CHAR_DATE_LS (è definito dalle opzioni di "Convertire TO_CHAR(date, format)").  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Yes  
  
**Modalità completa:** No  
  
### <a name="use-selectfor-xml-when-converting-selectinto-for-record-variable"></a>Usare SELECT... FOR XML durante la conversione Seleziona... INTO per la variabile di record  
Specifica se generare un XML set di risultati quando si seleziona in una variabile del record.  
  
-   Se si seleziona **Sì**, l'istruzione SELECT restituisce XML.  
  
-   Se si seleziona **No**, l'istruzione SELECT restituisce un set di risultati.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** no  
  
## <a name="returning-clause-conversion"></a>RESTITUZIONE di conversione clausola  
  
### <a name="convert-returning-clause-in-delete-statement-to-output"></a>Convertire l'OUTPUT clausola RETURNING nell'istruzione DELETE  
DB2 fornisce una clausola RETURNING come un modo per ottenere immediatamente valori eliminati. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tale funzionalità con la clausola OUTPUT.  
  
-   Se si seleziona **Sì**, SSMA convertirà RETURNING clausole in istruzioni DELETE in clausole OUTPUT. Poiché i trigger in una tabella possono cambiare i valori, il valore restituito potrebbe essere diverso in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rispetto a quello in DB2.  
  
-   Se si seleziona **No**, SSMA genererà un'istruzione SELECT prima delle istruzioni DELETE per recuperare i valori restituiti.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Yes  
  
### <a name="convert-returning-clause-in-insert-statement-to-output"></a>Convertire l'OUTPUT clausola RETURNING nell'istruzione INSERT  
DB2 fornisce una clausola RETURNING come un modo per ottenere immediatamente i valori inseriti. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tale funzionalità con la clausola OUTPUT.  
  
-   Se si seleziona **Sì**, SSMA convertirà una clausola RETURNING in un'istruzione INSERT in OUTPUT. Poiché i trigger in una tabella possono cambiare i valori, il valore restituito potrebbe essere diverso in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rispetto a quello in DB2.  
  
-   Se si seleziona **No**, SSMA emula la funzionalità di DB2 mediante l'inserimento e quindi selezionando valori da una tabella di riferimento.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Yes  
  
### <a name="convert-returning-clause-in-update-statement-to-output"></a>Convertire l'OUTPUT clausola RETURNING nell'istruzione UPDATE  
DB2 fornisce una clausola RETURNING come un modo per ottenere immediatamente i valori aggiornati. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tale funzionalità con la clausola OUTPUT.  
  
-   Se si seleziona **Sì**, SSMA convertirà RETURNING clausole nelle istruzioni UPDATE in clausole OUTPUT. Poiché i trigger in una tabella possono cambiare i valori, il valore restituito potrebbe essere diverso in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rispetto a quello in DB2.  
  
-   Se si seleziona **No**, SSMA genererà istruzioni SELECT dopo le istruzioni UPDATE per recuperare i valori che restituiscono.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Yes  
  
## <a name="sequence-conversion"></a>Conversione di sequenza  
  
### <a name="convert-sequence-generator"></a>Convertire il generatore di sequenze  
In DB2, è possibile usare una sequenza per generare identificatori univoci.  
  
SSMA è possibile convertire le sequenze in quanto segue.  
  
-   Tramite il generatore di sequenze di SQL Server (questa opzione è disponibile solo durante la conversione in SQL Server 2012 e SQL Server 2014).  
  
-   Tramite il generatore di sequenze SSMA.  
  
-   Utilizzando l'identità di colonna.  
  
L'opzione predefinita durante la conversione in SQL Server 2012 o SQL Server 2014 è usare il generatore di sequenze di SQL Server. Tuttavia, SQL Server 2012 e SQL Server 2014 non supporta come ottenere il valore di sequenza corrente (ad esempio quella del metodo di DB2 sequenza currval). Fare riferimento al sito di blog del team SSMA per indicazioni sulla migrazione metodo currval sequenza di DB2.  
  
SSMA fornisce inoltre un'opzione per convertire una sequenza di DB2 all'emulatore sequenza SSMA. Questo è l'opzione predefinita quando si converte in SQL Server precedente alla 2012  
  
Infine, è anche possibile convertire sequenza assegnato a una colonna nella tabella di valori identity di SQL Server. È necessario specificare il mapping tra le sequenze a una colonna identity in DB2 **tabella** scheda  
  
### <a name="convert-currval-outside-triggers"></a>Convertire CURRVAL all'esterno di trigger  
Visibile solo quando il generatore di sequenza convertire è impostato su **utilizzando l'identità di colonna**. Poiché le sequenze di DB2 sono oggetti separati dalle tabelle, usano le sequenze di molte tabelle di usano un trigger per generare e inserire un nuovo valore di sequenza. SSMA imposta come commento queste istruzioni o li contrassegna come errori durante il creazione dei commenti out genererebbero errori.  
  
-   Se si seleziona **Sì**, SSMA verrà contrassegnati tutti i riferimenti per i trigger sulle convertito di fuori sequenza CURRVAL con un avviso.  
  
-   Se si seleziona **No**, SSMA verrà contrassegnati tutti i riferimenti per i trigger sulle convertito di fuori sequenza CURRVAL con un errore.  
  
## <a name="see-also"></a>Vedere anche  
[Riferimento all'interfaccia utente &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
