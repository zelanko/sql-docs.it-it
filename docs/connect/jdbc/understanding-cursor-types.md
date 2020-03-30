---
title: Informazioni sui tipi di cursore | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4f4d3db7-4f76-450d-ab63-141237a4f034
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5ea30d2280ffea4c2ccf09d1f884a03751ed843
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027493"
---
# <a name="understanding-cursor-types"></a>Informazioni sui tipi di cursore
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Nei database relazionali le operazioni vengono eseguite su set di righe completi. Il set di righe restituito da un'istruzione SELECT include tutte le righe che soddisfano le condizioni specificate nella clausola WHERE dell'istruzione. Il set di righe completo restituito dall'istruzione è noto come set di risultati. Le applicazioni non sono sempre in grado di gestire in modo efficiente un intero set di risultati come singola unità. In tali applicazioni deve essere pertanto disponibile un meccanismo per l'elaborazione di una riga singola o di un blocco di righe di dimensioni ridotte. I cursori sono un'estensione dei set di risultati che implementano appunto tale meccanismo.  
  
 I cursori estendono le funzionalità di elaborazione dei set di risultati nei modi seguenti:  
  
-   Consentono il posizionamento su righe specifiche del set di risultati.  
  
-   Recuperano una riga o un blocco di righe dalla posizione corrente del set di risultati.  
  
-   Supportano le modifiche ai dati della riga in corrispondenza della posizione corrente nel set di risultati.  
  
-   Supportano livelli diversi di visibilità per le modifiche apportate da altri utenti ai dati del database inclusi nel set di risultati.  
  
> [!NOTE]  
>  Per una descrizione completa dei tipi di cursore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere l'argomento "Tipi di cursore (Motore di database)" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La specifica JDBC fornisce supporto per cursori forward-only e scorrevoli sensibili o non sensibili alle modifiche apportate da altri processi e che possono essere di sola lettura o aggiornabili. Questa funzionalità viene fornita dalla classe [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)][SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="remarks"></a>Osservazioni  
 Il driver JDBC supporta i tipi di cursore seguenti:  
  
|Set di risultati<br /><br /> risultati (cursore)|Tipo di cursore di SQL Server|Caratteristiche|Proprietà<br /><br /> Metodo|Risposta<br /><br /> responseBuffering|Descrizione|  
|------------------------------------|----------------------------|---------------------|-----------------------|----------------------------|-----------------|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|N/D|Forward-only, di sola lettura|dirette|completi|L'applicazione deve eseguire una singola iterazione (in avanti) nel set di risultati. Si tratta del comportamento predefinito, corrispondente a un cursore TYPE_SS_DIRECT_FORWARD_ONLY. Tramite il driver viene letto l'intero set di risultati dal server caricandolo in memoria durante l'esecuzione dell'istruzione.|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|N/D|Forward-only, di sola lettura|dirette|adaptive|L'applicazione deve eseguire una singola iterazione (in avanti) nel set di risultati. Il comportamento corrisponde a quello di un cursore TYPE_SS_DIRECT_FORWARD_ONLY. Tramite il driver le righe vengono lette dal server quando vengono richieste dall'applicazione, riducendo così al minimo l'utilizzo della memoria sul lato client.|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|Fast forward|Forward-only, di sola lettura|cursor|N/D|L'applicazione deve eseguire una singola iterazione (in avanti) nel set di risultati utilizzando un cursore server. Il comportamento è analogo a quello di un cursore TYPE_SS_SERVER_CURSOR_FORWARD_ONLY.<br /><br /> Le righe vengono recuperate dal server in blocchi specificati dalla dimensione di recupero.|  
|TYPE_FORWARD_ONLY (CONCUR_UPDATABLE)|Dinamico (forward-only)|Forward-only, aggiornabile|N/D|N/D|L'applicazione deve eseguire una singola iterazione (in avanti) nel set di risultati per aggiornare una o più righe.<br /><br /> Le righe vengono recuperate dal server in blocchi specificati dalla dimensione di recupero.<br /><br /> Per impostazione predefinita, la dimensione di recupero viene fissata quando l'applicazione chiama il metodo [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) dell'oggetto [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md).<br /><br /> **Nota:** Il driver JDBC include una caratteristica di buffer adattivo che consente di recuperare i risultati dell'esecuzione di istruzioni da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando questi sono necessari per l'applicazione e non tutti contemporaneamente. Se ad esempio l'applicazione deve recuperare una quantità di dati eccessiva per essere caricata completamente in memoria, il buffer adattivo consente all'applicazione client di recuperare tali dati sotto forma di flusso. Il comportamento predefinito del driver è "**adaptive**". Per ottenere il buffer adattivo per i set di risultati aggiornabili forward-only, l'applicazione deve tuttavia chiamare in modo esplicito il metodo [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) dell'oggetto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) offrendo un valore **Stringa** "**adaptive"** . Per un esempio di codice, vedere [Esempio di aggiornamento di dati di grandi dimensioni](../../connect/jdbc/updating-large-data-sample.md).|  
|TYPE_SCROLL_INSENSITIVE|Statico|Scorrevole, non aggiornabile<br /><br /> Gli aggiornamenti, gli inserimenti e le eliminazioni di righe eseguiti esternamente non sono visibili.|N/D|N/D|L'applicazione richiede uno snapshot del database. Il set di risultati non è aggiornabile. È supportato solo CONCUR_READ_ONLY.  Tutti gli altri tipi di concorrenza generano un'eccezione, se utilizzati con questo tipo di cursore.<br /><br /> Le righe vengono recuperate dal server in blocchi specificati dalla dimensione di recupero.|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_READ_ONLY)|Keyset|Scorrevole, sola lettura. Gli aggiornamenti di righe eseguiti esternamente sono visibili e le eliminazioni vengono visualizzate come dati mancanti.<br /><br /> Gli inserimenti di righe eseguiti esternamente non sono visibili.|N/D|N/D|Nell'applicazione devono essere visualizzati i dati modificati solo per le righe esistenti.<br /><br /> Le righe vengono recuperate dal server in blocchi specificati dalla dimensione di recupero.|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Keyset|Scorrevole, aggiornabile<br /><br /> Gli aggiornamenti di righe eseguiti internamente ed esternamente sono visibili e le eliminazioni vengono visualizzate come dati mancanti. Gli inserimenti non sono visibili.|N/D|N/D|L'applicazione può modificare i dati nelle righe esistenti tramite l'oggetto ResultSet. L'applicazione deve inoltre essere in grado di visualizzare le modifiche apportate alle righe da altri esternamente all'oggetto ResultSet.<br /><br /> Le righe vengono recuperate dal server in blocchi specificati dalla dimensione di recupero.|  
|TYPE_SS_DIRECT_FORWARD_ONLY|N/D|Forward-only, di sola lettura|N/D|full o adaptive|Valore intero = 2003. Fornisce un cursore sul lato client di sola lettura completamente memorizzato nel buffer. Non viene creato alcun cursore server.<br /><br /> È supportato solo il tipo di concorrenza CONCUR_READ_ONLY. Tutti gli altri tipi di concorrenza generano un'eccezione, se utilizzati con questo tipo di cursore.|  
|TYPE_SS_SERVER_CURSOR_FORWARD_ONLY|Fast forward|Forward-only|N/D|N/D|Valore intero = 2004. Veloce, con accesso a tutti i dati tramite un cursore server. È aggiornabile quando viene utilizzato con il tipo di concorrenza CONCUR_UPDATABLE.<br /><br /> Le righe vengono recuperate dal server in blocchi specificati dalla dimensione di recupero.<br /><br /> Per ottenere il buffer adattivo per questo caso, l'applicazione deve chiamare in modo esplicito il metodo [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) dell'oggetto [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) offrendo un valore **Stringa** "**adaptive"** . Per un esempio di codice, vedere [Esempio di aggiornamento di dati di grandi dimensioni](../../connect/jdbc/updating-large-data-sample.md).|  
|TYPE_SS_SCROLL_STATIC|Statico|Gli aggiornamenti di altri utenti non vengono riflessi.|N/D|N/D|Valore intero = 1004. L'applicazione richiede uno snapshot del database. Si tratta del sinonimo specifico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il tipo JDBC TYPE_SCROLL_INSENSITIVE ed è caratterizzato dallo stesso comportamento dell'impostazione di concorrenza.<br /><br /> Le righe vengono recuperate dal server in blocchi specificati dalla dimensione di recupero.|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_READ_ONLY)|Keyset|Scorrevole, sola lettura. Gli aggiornamenti di righe eseguiti esternamente sono visibili e le eliminazioni vengono visualizzate come dati mancanti.<br /><br /> Gli inserimenti di righe eseguiti esternamente non sono visibili.|N/D|N/D|Valore intero = 1005. Nell'applicazione devono essere visualizzati i dati modificati per le righe esistenti. Si tratta del sinonimo specifico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il tipo JDBC TYPE_SCROLL_SENSITIVE ed è caratterizzato dallo stesso comportamento dell'impostazione di concorrenza.<br /><br /> Le righe vengono recuperate dal server in blocchi specificati dalla dimensione di recupero.|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Keyset|Scorrevole, aggiornabile<br /><br /> Gli aggiornamenti di righe eseguiti internamente ed esternamente sono visibili e le eliminazioni vengono visualizzate come dati mancanti. Gli inserimenti non sono visibili.|N/D|N/D|Valore intero = 1005. Nell'applicazione devono essere modificati i dati oppure devono essere visualizzati i dati modificati solo per le righe esistenti. Si tratta del sinonimo specifico di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per il tipo JDBC TYPE_SCROLL_SENSITIVE ed è caratterizzato dallo stesso comportamento dell'impostazione di concorrenza.<br /><br /> Le righe vengono recuperate dal server in blocchi specificati dalla dimensione di recupero.|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_READ_ONLY)|Dinamico|Scorrevole, sola lettura.<br /><br /> Gli aggiornamenti e gli inserimenti di righe eseguiti esternamente sono visibili e le eliminazioni vengono visualizzate come dati mancanti temporanei nel buffer di recupero corrente.|N/D|N/D|Valore intero = 1006. Nell'applicazione devono essere visualizzati i dati modificati per le righe esistenti, nonché le righe inserite ed eliminate nel corso della durata del cursore.<br /><br /> Le righe vengono recuperate dal server in blocchi specificati dalla dimensione di recupero.|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Dinamico|Scorrevole, aggiornabile<br /><br /> Gli aggiornamenti e gli inserimenti di righe eseguiti esternamente e internamente sono visibili e le eliminazioni vengono visualizzate come dati mancanti temporanei nel buffer di recupero corrente.|N/D|N/D|Valore intero = 1006. L'applicazione può modificare i dati per le righe esistenti oppure inserire o eliminare righe tramite l'oggetto ResultSet. L'applicazione deve inoltre essere in grado di visualizzare le modifiche, gli inserimenti e le eliminazioni apportate da altri esternamente all'oggetto ResultSet.<br /><br /> Le righe vengono recuperate dal server in blocchi specificati dalla dimensione di recupero.|  
  
## <a name="cursor-positioning"></a>Posizionamento dei cursori  
 I cursori TYPE_FORWARD_ONLY, TYPE_SS_DIRECT_FORWARD_ONLY e TYPE_SS_SERVER_CURSOR_FORWARD_ONLY supportano solo il metodo di posizionamento [next](../../connect/jdbc/reference/next-method-sqlserverresultset.md).  
  
 Il cursore TYPE_SS_SCROLL_DYNAMIC non supporta i metodi [absolute](../../connect/jdbc/reference/absolute-method-sqlserverresultset.md) e [getRow](../../connect/jdbc/reference/getrow-method-sqlserverresultset.md). È possibile ottenere un risultato simile a quello del metodo absolute tramite una combinazione di chiamate ai metodi [first](../../connect/jdbc/reference/first-method-sqlserverresultset.md) e [relative](../../connect/jdbc/reference/relative-method-sqlserverresultset.md) per i cursori dinamici.  
  
 Il metodo getRow è supportato solo dai cursori TYPE_FORWARD_ONLY, TYPE_SS_DIRECT_FORWARD_ONLY, TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, TYPE_SS_SCROLL_KEYSET e TYPE_SS_SCROLL_STATIC. Il metodo getRow con tutti i tipi di cursore forward-only restituisce il numero di righe lette fino a quel momento tramite il cursore.  
  
> [!NOTE]  
>  Quando un'applicazione esegue una chiamata non supportata ai metodi di posizionamento del cursore o al metodo getRow, viene generata un'eccezione con il messaggio "L'operazione richiesta non è supportata con questo tipo di cursore".  
  
 Solo il cursore TYPE_SS_SCROLL_KEYSET e l'equivalente TYPE_SCROLL_SENSITIVE espongono le righe eliminate. Se il cursore viene posizionato in una riga eliminata, i valori della colonna non sono disponibili e il metodo [rowDeleted](../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) restituisce "true". Le chiamate ai metodi get\<Type> generano un'eccezione con il messaggio "Impossibile ottenere un valore da una riga eliminata". Le righe eliminate non possono essere aggiornate. Se si tenta di chiamare un metodo update\<Type> in una riga eliminata, viene generata un'eccezione con il messaggio "Non è possibile aggiornare una riga eliminata". Il cursore TYPE_SS_SCROLL_DYNAMIC ha lo stesso comportamento fino a quando non viene tolto dal buffer di recupero corrente.  
  
 I cursori forward e dinamici espongono le righe eliminate in modo simile, ma solo fino a quando rimangono accessibili nel buffer di recupero. Per i cursori forward, questo comportamento è piuttosto lineare. Per i cursori dinamici, si tratta di un comportamento più complesso quando la dimensione di recupero è maggiore di 1. Un'applicazione può spostare il cursore avanti e indietro nella finestra definita dal buffer di recupero, ma la riga eliminata non viene più visualizzata all'uscita dal buffer di recupero originale in cui è stata aggiornata. Se non si desidera che in un'applicazione vengano visualizzate righe eliminate temporanee tramite i cursori dinamici, è necessario utilizzare un'istruzione FETCH RELATIVE con l'argomento 0.  
  
 Se i valori chiave della riga di un cursore TYPE_SS_SCROLL_KEYSET o TYPE_SCROLL_SENSITIVE vengono aggiornati con il cursore, la riga mantiene la propria posizione originale nel set di risultati, indipendentemente dal fatto che la riga aggiornata soddisfi i criteri di selezione del cursore. Se la riga è stata aggiornata all'esterno del cursore, nella posizione originale della riga verrà visualizzata una riga eliminata, ma la riga verrà visualizzata nel cursore solo se nel cursore era presente un'altra riga con i nuovi valori chiave, che tuttavia è stata eliminata.  
  
 Per i cursori dinamici, le righe aggiornate mantengono la posizione all'interno del buffer di recupero fino a quando la finestra definita dal buffer di recupero non viene chiusa. Successivamente, le righe aggiornate possono venire visualizzate in posizioni diverse nel set di risultati o scomparire completamente. Per le applicazioni in cui è necessario evitare le incoerenze temporanee nel set di risultati, è necessario utilizzare una dimensione di recupero pari a 1. L'impostazione predefinita è 8 righe con concorrenza CONCUR_SS_SCROLL_LOCKS e 128 righe con altre concorrenze.  
  
## <a name="cursor-conversion"></a>Conversione dei cursori  
 A volte, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può venire implementato un tipo di cursore diverso da quello richiesto e questo comportamento è noto come conversione implicita del cursore o degradazione del cursore. Per ulteriori informazioni sulla conversione implicita del cursore, vedere l'argomento "Utilizzo della conversione implicita del cursore" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Con [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], quando si aggiornano i dati tramite il set di risultati ResultSet.TYPE_SCROLL_SENSITIVE e ResultSet.CONCUR_UPDATABLE, viene generata un'eccezione con un messaggio "il cursore è READ ONLY". Questa eccezione si verifica perché in [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] è stata eseguita una conversione implicita del cursore per tale set di risultati e non è stato restituito il cursore aggiornabile richiesto.  
  
 Per ovviare a questo problema, è possibile scegliere una delle due soluzioni seguenti:  
  
-   Verificare che la tabella sottostante disponga di una chiave primaria.  
  
-   Usare [SQLServerResultSet.TYPE_SS_SCROLL_DYNAMIC](../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md) anziché ResultSet.TYPE_SCROLL_SENSITIVE durante la creazione di un'istruzione.  
  
## <a name="cursor-updating"></a>Aggiornamento dei cursori  
 Gli aggiornamenti sul posto sono supportati per i cursori se la concorrenza e il tipo di cursore supportano gli aggiornamenti. Se il cursore non è posizionato in una riga aggiornabile nel set di risultati (nessuna chiamata al metodo get\<Type> ha avuto esito positivo), una chiamata a un metodo update\<Type> genera un'eccezione con il messaggio "Il set di risultati non ha una riga corrente". In base alla specifica JDBC viene generata un'eccezione quando viene chiamato un metodo di aggiornamento per una colonna di un cursore di tipo CONCUR_READ_ONLY. Nei casi in cui la riga non è aggiornabile, ad esempio a causa di un conflitto di concorrenza ottimistica come un aggiornamento o un'eliminazione in conflitto, l'eccezione potrebbe non venire generata fino a quando non viene chiamato il metodo [insertRow](../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md), [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) o [deleteRow](../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md).  
  
 Dopo una chiamata a update\<Type>, non è possibile accedere alla colonna interessata tramite get\<Type> fino a quando non viene chiamato il metodo updateRow o [cancelRowUpdates](../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md). In questo modo è possibile evitare i problemi che possono verificarsi quando una colonna viene aggiornata utilizzando un tipo diverso da quello restituito dal server e le chiamate al metodo Get successive possono richiamare conversioni del tipo sul lato client che forniscono risultati non accurati. Le chiamate a get\<Type> generano un'eccezione con il messaggio "Impossibile accedere alle colonne aggiornate fino a quando non è stato chiamato updateRow() o cancelRowUpdates()".  
  
> [!NOTE]  
>  Se il metodo updateRow viene chiamato quando non è stata aggiornata alcuna colonna, il driver JDBC genera un'eccezione con un messaggio che indica che è stato chiamato il metodo updateRow () senza che siano state aggiornate le colonne.  
  
 Dopo la chiamata a [moveToInsertRow](../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md), viene generata un'eccezione se nel set di risultati viene chiamato qualsiasi metodo ad eccezione di get\<Type>, update\<Type>, insertRow e dei metodi di posizionamento del cursore, incluso [moveToCurrentRow](../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md). Il metodo moveToInsertRow consente di attivare in modo efficace la modalità di inserimento per il set di risultati e i metodi di posizionamento del cursore consentono di interrompere tale modalità. Le chiamate ai metodi di posizionamento relativo del cursore consentono di spostare il cursore rispetto alla posizione in cui si trovava prima della chiamata al metodo moveToInsertRow. Dopo le chiamate ai metodi di posizionamento del cursore, la posizione di destinazione finale del cursore diventa la nuova posizione del cursore.  
  
 Se la chiamata ai metodi di posizionamento del cursore eseguita in modalità di inserimento non ha esito positivo, la posizione del cursore dopo tale chiamata corrisponde alla posizione originale del cursore prima della chiamata a moveToInsetRow. Se il metodo insertRow ha esito negativo, il cursore rimane nella riga di inserimento e in modalità di inserimento.  
  
 Inizialmente, le colonne nella riga di inserimento hanno uno stato non inizializzato. Le chiamate al metodo update\<Type> consentono di impostare lo stato delle colonne come inizializzato. Una chiamata al metodo get\<Type> per una colonna non inizializzata genera un'eccezione. Una chiamata al metodo insertRow ripristina lo stato non inizializzato per tutte le colonne nella riga di inserimento.  
  
 Se quando viene chiamato il metodo insertRow vi sono colonne non inizializzate, in tali colonne viene inserito il relativo valore predefinito. Se non è disponibile un valore predefinito, ma la colonna ammette i valori Null, viene inserito NULL. Se non è disponibile un valore predefinito e la colonna non ammette i valori Null, il server restituisce un errore e viene generata un'eccezione.  
  
> [!NOTE]  
>  Le chiamate al metodo getRow eseguite in modalità di inserimento restituiscono 0.  
>   
>  Il driver JDBC non supporta eliminazioni o aggiornamenti posizionati. In base alla specifica JDBC, il metodo [setCursorName](../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md) non ha effetto e il metodo [getCursorName](../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md) quando viene chiamato genera un'eccezione.  
>   
>  I cursori di sola lettura e statici non sono mai aggiornabili.  
>   
>  In SQL Server i cursori server sono limitati a un singolo set di risultati. Se un batch o una stored procedure contiene più istruzioni, è necessario utilizzare un cursore client di sola lettura forward-only.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione dei set di risultati con il driver JDBC](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  
