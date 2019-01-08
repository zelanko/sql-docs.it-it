---
title: Cursori | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- results [SQL Server], cursors
- Transact-SQL cursors, about cursors
- cursors [SQL Server]
- data access [SQL Server], cursors
- result sets [SQL Server], cursors
- requesting cursors
- cursors [SQL Server], about cursors
ms.assetid: e668b40c-bd4d-4415-850d-20fc4872ee72
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8123179285b94377fff758121f535175705f29af
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52774263"
---
# <a name="cursors"></a>Cursori
  Nei database relazionali le operazioni vengono eseguite su set di righe completi. Ad esempio, il set di righe restituito dall'istruzione SELECT include tutte le righe che soddisfano le condizioni specificate nella clausola WHERE dell'istruzione. Il set di righe completo restituito dall'istruzione è noto come set di risultati. Le applicazioni, soprattutto le applicazioni online interattive, non sono sempre in grado di gestire in modo efficiente un intero set di risultati come singola unità. In tali applicazioni deve essere pertanto disponibile un meccanismo per l'elaborazione di una riga singola o di un blocco di righe di dimensioni ridotte. I cursori sono un'estensione dei set di risultati che implementano appunto tale meccanismo.  
  
 I cursori estendono l'elaborazione dei risultati nel modo seguente:  
  
-   Consentono il posizionamento su righe specifiche del set di risultati.  
  
-   Recuperano una riga o un blocco di righe dalla posizione corrente del set di risultati.  
  
-   Supportano la modifica dei dati delle righe in corrispondenza della posizione corrente del set di risultati.  
  
-   Supportano livelli diversi di visibilità per le modifiche apportate da altri utenti ai dati del database inclusi nel set di risultati.  
  
-   Consentono alle istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] incluse in script, stored procedure e trigger di accedere ai dati di un set di risultati.  
  
## <a name="concepts"></a>Concetti  
 Implementazione dei cursori  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supporta l'implementazione di tre tipi di cursori.  
  
 cursori Transact-SQL  
 Sono basati sulla sintassi DECLARE CURSOR e sono principalmente usati in trigger, stored procedure e script [!INCLUDE[tsql](../includes/tsql-md.md)] . [!INCLUDE[tsql](../includes/tsql-md.md)] vengono implementati nel server e gestiti dalle istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] inviate dal client al server. Possono essere inoltre inclusi in batch, stored procedure o trigger.  
  
 Cursori API (Application Programming Interface) del server  
 Supportano le funzioni dei cursori API in OLE DB e ODBC. Questi cursori sono implementati nel server. Ogni volta che un'applicazione client chiama una funzione per un cursore API, il provider OLE DB o il driver ODBC di Native Client [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] trasmette al server la richiesta di eseguire un'azione sul cursore API del server.  
  
 Cursori client  
 Sono implementati internamente dal driver ODBC di Native Client [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e dalla DLL che implementa l'API ADO. I cursori client vengono implementati mediante la memorizzazione nella cache del client di tutte le righe del set di risultati. Ogni volta che un'applicazione client chiama una funzione per un cursore API, la DLL ADO o il driver ODBC di Native Client [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] esegue l'operazione del cursore nelle righe del set di risultati memorizzate nella cache del client.  
  
 Tipo di cursori  
 Forward-only  
 I cursori forward-only non supportano lo scorrimento, ma solo le operazioni di recupero seriale delle righe dall'inizio alla fine del cursore. Le righe vengono prelevate dal database solo quando si esegue l'operazione di recupero. Gli effetti delle istruzioni INSERT, UPDATE e DELETE eseguite dall'utente corrente o da altri utenti che coinvolgono le righe del set di risultati sono visibili nel momento in cui le righe vengono recuperate dal cursore.  
  
 Poiché non è supportato lo scorrimento a ritroso del cursore, la maggior parte delle modifiche apportate alle righe nel database in seguito al recupero non sono visibili tramite il cursore. Nei casi in cui un valore usato per determinare la posizione della riga all'interno del set di risultati viene modificato, ad esempio tramite l'aggiornamento di una colonna coperta da un indice cluster, il valore modificato sarà visibile tramite il cursore.  
  
 Anche se i modelli di cursore API del database considerano un cursore forward-only un tipo distinto di cursore, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non fa questa distinzione. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] considera il forward-only e lo scorrimento come opzioni da applicare ai cursori statici, gestiti da keyset e dinamici. [!INCLUDE[tsql](../includes/tsql-md.md)] supportano i cursori dinamici, i cursori gestiti da keyset e i cursori statici forward-only. In base ai modelli di cursore dell'API di database i cursori dinamici, gestiti da keyset o statici sono sempre scorrevoli. I cursori API del database con una proprietà o un attributo impostato su forward-only vengono implementati in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] come cursori forward-only dinamici.  
  
 Static  
 Il set di risultati completo di un cursore statico viene compilato nel database **tempdb** all'apertura del cursore. Un cursore statico visualizza sempre il set di risultati così come è visualizzato all'apertura del cursore. I cursori statici rilevano poche modifiche o addirittura nessuna, ma utilizzano un numero relativamente ridotto di risorse per lo scorrimento.  
  
 Nel cursore non vengono riportate né le modifiche al database che hanno effetto sull'appartenenza del set di risultati, né le modifiche apportate ai valori inclusi nelle colonne delle righe del set di risultati. Un cursore statico non visualizza le nuove righe inserite nel database dopo l'apertura del cursore, anche se tali righe soddisfano le condizioni di ricerca dell'istruzione SELECT del cursore. Non visualizza inoltre gli aggiornamenti eseguiti da altri utenti nelle righe del set di risultati. Un cursore statico riflette invece le operazioni di eliminazione di righe dal database dopo l'apertura del cursore. Il risultato delle operazioni UPDATE, INSERT e DELETE non viene mai riportato nel cursore statico, né le modifiche eseguite sulla stessa connessione in cui è stato aperto il cursore (a meno che il cursore non venga chiuso e riaperto).  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sono sempre di sola lettura.  
  
 Poiché il set di risultati di un cursore statico viene archiviato in una tabella di lavoro in **tempdb**, la lunghezza delle righe non può essere maggiore della lunghezza di riga massima consentita per le tabelle di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] definisce i cursori statici come cursori di tipo insensitive. Alcune API di database li identificano come cursori snapshot.  
  
 Keyset  
 L'appartenenza e l'ordine delle righe di un cursore gestito da keyset vengono fissati al momento dell'apertura del cursore. I cursori gestiti da keyset vengono controllati da un set di identificatori univoci, ovvero chiavi, noti come keyset. Le chiavi sono costituite da un set di colonne che identificano in modo univoco le righe del set di risultati. Il keyset corrisponde al set di valori chiave di tutte le righe risultanti dall'istruzione SELECT al momento dell'apertura del cursore. Il keyset di un cursore gestito da keyset viene compilato nel database **tempdb** all'apertura del cursore.  
  
 Dynamic  
 I cursori dinamici sono l'opposto dei cursori statici. Quando si scorre un cursore dinamico vengono visualizzate tutte le modifiche apportate alle righe del set di risultati corrispondente. I valori di dati, l'ordine e l'appartenenza delle righe del set di risultati possono variare a ogni operazione di recupero. I risultati delle istruzioni UPDATE, INSERT e DELETE eseguite da tutti gli utenti sono visibili nel cursore. Gli aggiornamenti sono visibili immediatamente se eseguiti nel cursore tramite una funzione API quale **SQLSetPos** o la clausola WHERE CURRENT OF [!INCLUDE[tsql](../includes/tsql-md.md)] . Gli aggiornamenti eseguiti all'esterno del cursore risultano visibili solo dopo l'operazione di commit, a meno che il livello di isolamento della transazione non sia impostato su read uncommitted. I piani dinamici del cursore non usano mai indici spaziali.  
  
## <a name="requesting-a-cursor"></a>Richiesta di cursori  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supporta due metodi per richiedere un cursore:  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)]  
  
     Il linguaggio [!INCLUDE[tsql](../includes/tsql-md.md)] supporta una sintassi per l'utilizzo dei cursori creati in base alla sintassi del cursore ISO.  
  
-   Funzioni per i cursori delle API di database  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] supporta la funzionalità per i cursori delle API di database seguenti:  
  
    -   ADO ([!INCLUDE[msCoName](../includes/msconame-md.md)] ActiveX Data Object)  
  
    -   OLE DB  
  
    -   ODBC (Open Database Connectivity)  
  
 Questi due metodi non devono essere implementati entrambi nella stessa applicazione. In un'applicazione in cui le funzionalità del cursore sono state implementate tramite le API, non è consentito richiedere un cursore [!INCLUDE[tsql](../includes/tsql-md.md)] tramite l'istruzione [!INCLUDE[tsql](../includes/tsql-md.md)] DECLARE CURSOR. L'istruzione DECLARE CURSOR può essere eseguita solo dopo il ripristino di tutti i valori predefiniti degli attributi dei cursori API.  
  
 Se non è stato richiesto né un cursore [!INCLUDE[tsql](../includes/tsql-md.md)] , né un cursore API, per impostazione predefinita [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] restituisce all'applicazione un set di risultati completo, ovvero un set di risultati predefinito.  
  
## <a name="cursor-process"></a>Processo del cursore  
 [!INCLUDE[tsql](../includes/tsql-md.md)] e i cursori API prevedono una sintassi diversa, ma per tutti i cursori di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] viene usata la seguente procedura generale:  
  
1.  Associare un cursore al set di risultati di un'istruzione [!INCLUDE[tsql](../includes/tsql-md.md)] e definirne le caratteristiche, ad esempio se le righe del cursore sono aggiornabili.  
  
2.  Eseguire l'istruzione [!INCLUDE[tsql](../includes/tsql-md.md)] per popolare il cursore.  
  
3.  Recuperare le righe del cursore da visualizzare. L'operazione che consente di ottenere una riga o un blocco di righe da un cursore è definita operazione di recupero. L'esecuzione di una serie di operazioni di recupero in avanti o a ritroso è definita scorrimento.  
  
4.  Facoltativamente, eseguire operazioni di modifica (aggiornamento o eliminazione) sulla riga che si trova nella posizione corrente del cursore.  
  
5.  Chiudere il cursore.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Cursor Behaviors](native-client-odbc-cursors/cursor-behaviors.md) [How Cursors Are Implemented](native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
## <a name="see-also"></a>Vedere anche  
 [DECLARE CURSOR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-cursor-transact-sql)   
 [Cursori &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/cursors-transact-sql)   
 [Funzioni per i cursori &#40;Transact-SQL&#41;](/sql/t-sql/functions/cursor-functions-transact-sql)   
 [Stored procedure per cursori &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/cursor-stored-procedures-transact-sql)  
  
  
