---
title: Uso del mirroring del database | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- SQL Server Native Client, database mirroring
- data access [SQL Server Native Client], database mirroring
- database mirroring [SQL Server], connecting clients to
- SQLNCLI, database mirroring
- SQL Server Native Client ODBC driver, database mirroring
- SQL Server Native Client OLE DB provider, database mirroring
ms.assetid: 71b15712-7972-4465-9274-e0ddc271eedc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4d282569bf88379e36ebb5297d3dbb9f6cf945fc
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246733"
---
# <a name="using-database-mirroring-in-sql-server-native-client"></a>Utilizzo del mirroring del database in SQL Server Native Client
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)] In alternativa, usare [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)].  
  
 Il mirroring del database, introdotto in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], è una soluzione per aumentare la disponibilità del database e la ridondanza dei dati. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client fornisce supporto implicito per il mirroring del database, pertanto lo sviluppatore non deve scrivere codice né eseguire altre azioni dopo che è stato configurato per il database.  
  
 Il mirroring del database, implementato per ogni database, consente di conservare una copia di un database di produzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in un server di standby. Tale server può essere warm standby o hot standby, a seconda della configurazione e dello stato della sessione di mirroring del database. Un server hot standby supporta il failover rapido senza perdita di transazioni di cui è stato eseguito il commit, mentre un server warm standby supporta la forzatura del servizio (con possibile perdita di dati).  
  
 Il database di produzione è denominato *database principale*, mentre la copia di standby viene chiamata *database mirror*. Il database principale e il database mirror devono trovarsi in istanze separate di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (istanze server) e, se possibile, risiedere in computer separati.  
  
 L'istanza del server di produzione, chiamata *server principale*, comunica con l'istanza del server di standby, chiamata *server mirror*. I server principale e mirror fungono da partner all'interno di una *sessione*di mirroring del database. Se si verifica un errore nel server principale, il server mirror è in grado di creare un database nel database principale tramite un processo chiamato *failover*. Partner_A e Partner_B, ad esempio, sono due server partner, con il database principale inizialmente su Partner_A come server principale e il database mirror che risiede in Partner_B come server mirror. Se Partner_A passa alla modalità offline, il database su Partner_B può eseguire il failover per diventare il database principale corrente. Quando Partner_A si unisce alla sessione di mirroring, diventa il server mirror e il database diventa il database mirror.  
  
 Le configurazioni del mirroring del database alternative offrono livelli diversi di prestazioni e sicurezza dei dati e supportano forme diverse di failover. Per altre informazioni, vedere [Mirroring del database &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
 È possibile utilizzare un alias quando si specifica il nome del database mirror.  
  
> [!NOTE]  
>  Per informazioni sui tentativi di connessione iniziali e su quelli di riconnessione a un database con mirroring, vedere [Connettere client a una sessione di mirroring del database &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md).  
  
## <a name="programming-considerations"></a>Considerazioni sulla programmazione  
 Quando si verifica un errore nel server di database principale, l'applicazione client riceve errori in risposta a chiamate API che indicano che la connessione al database è stata persa. In questo caso qualsiasi modifica al database di cui non sia stato eseguito il commit viene persa e viene eseguito il rollback della transazione corrente. In una situazione di questo tipo l'applicazione deve chiudere la connessione (o rilasciare l'oggetto origine dati) e stabilirla nuovamente. La connessione viene reindirizzata in maniera trasparente al database mirror che ora viene utilizzato come server principale.  
  
 Quando viene stabilita una connessione, il server principale invia l'identità del proprio partner di failover al client da utilizzare quando si verifica il failover. Nei casi in cui un'applicazione ha provato a stabilire una connessione dopo che si è verificato un errore nel server principale, il client non conosce l'identità del partner di failover. Per consentire ai client di far fronte a questo scenario, una proprietà di inizializzazione e una parola chiave della stringa di connessione associata consentono al client di specificare l'identità del partner di failover. L'attributo client viene utilizzato solo in questo scenario. Se è disponibile, il server principale non viene utilizzato. Se il server partner di failover fornito dal client non si riferisce a un server utilizzato come partner di failover, la connessione viene rifiutata dal server. Per consentire alle applicazioni di adattarsi alle modifiche di configurazione, l'identità del partner di failover effettivo può essere determinata ispezionando l'attributo dopo che è stata stabilita la connessione. È consigliabile memorizzare nella cache le informazioni sul partner per aggiornare la stringa di connessione oppure escogitare una strategia per eseguire un nuovo tentativo nel caso in cui il primo tentativo di stabilire una connessione non riesca.  
  
> [!NOTE]  
>  È necessario specificare in modo esplicito il database che dovrà essere utilizzato da una connessione se si desidera utilizzare questa caratteristica in un DSN, una stringa di connessione oppure una proprietà o un attributo di connessione. Se non si esegue questa operazione, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client non proverà ad eseguire il failover nel database partner.  
>   
>  Il mirroring è una caratteristica del database. Nelle applicazioni che utilizzano più database potrebbe non essere possibile sfruttare questa caratteristica.  
>   
>  Per i nomi di server, inoltre, non viene fatta distinzione tra maiuscole e minuscole, mentre tale distinzione viene fatta per i nomi di database. È pertanto consigliabile assicurarsi di utilizzare la stessa combinazione tra maiuscole e minuscole nei DSN e nelle stringhe di connessione.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Provider OLE DB di SQL Server Native Client  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client supporta il mirroring del database tramite gli attributi della stringa di connessione e connessione. La proprietà SSPROP_INIT_FAILOVERPARTNER è stata aggiunta al set di proprietà DBPROPSET_SQLSERVERDBINIT e la parola chiave **FailoverPartner** è un nuovo attributo di stringa di connessione per DBPROP_INIT_PROVIDERSTRING. Per ulteriori informazioni, vedere [utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 La cache di failover viene mantenuta fino a quando il provider viene caricato, ovvero fino a quando non viene chiamato **CoUninitialize** o a condizione che l'applicazione disponga di un riferimento a un oggetto gestito da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] native client OLE DB provider, ad esempio un oggetto origine dati.  
  
 Per informazioni dettagliate sul [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporto del provider OLE DB Native Client per il mirroring del database, vedere [proprietà di inizializzazione e autorizzazione](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Driver ODBC di SQL Server Native Client  
 Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC di Native Client supporta il mirroring del database tramite gli attributi della stringa di connessione e connessione. In particolare, l'attributo SQL_COPT_SS_FAILOVER_PARTNER è stato aggiunto per l'utilizzo con le funzioni [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) e [SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) . e la parola chiave **Failover_Partner** è stata aggiunta come nuovo attributo della stringa di connessione.  
  
 La cache di failover viene gestita finché nell'applicazione è allocato almeno un handle di ambiente. Viene invece persa quando l'ultimo handle di ambiente viene deallocato.  
  
> [!NOTE]  
>  Gestione driver ODBC è stato migliorato per supportare la specifica del nome del server di failover.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Connettere client a una sessione di mirroring del database &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)   
 [Mirroring del database &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
