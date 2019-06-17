---
title: Utilizzo delle notifiche delle Query | Microsoft Docs
description: Utilizzo delle notifiche delle query nel Driver OLE DB per SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], query notifications
- rowsets [SQL Server], notifications
- OLE DB Driver for SQL Server, query notifications
- notifications [OLE DB Driver for SQL Server]
- query notifications [SQL Server], OLE DB Driver for SQL Server
- canceling rowset changes
- IRowsetNotify interface
- MSOLEDBSQL, query notifications
- OLE DB Driver for SQL Server, query notifications
- consumer notification for rowset changes [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 7139e6a80e05fbe3671acc9246d42a1354da714f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796035"
---
# <a name="working-with-query-notifications"></a>Utilizzo delle notifiche delle query
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Le notifiche delle query sono state introdotte in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] e il Driver OLE DB per SQL Server. Basate sull'infrastruttura di Service Broker introdotta in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], tali notifiche consentono di comunicare alle applicazioni che i dati sono stati modificati. Questa caratteristica è particolarmente utile per le applicazioni che forniscono una cache di informazioni provenienti da un database, ad esempio un'applicazione Web, e devono essere notificate quando i dati di origine vengono modificati.  
  
 Le notifiche delle query consentono di richiedere una notifica entro un determinato periodo di timeout quando i dati sottostanti di una query cambiano. La richiesta di notifica specifica le opzioni di notifica che includono il nome del servizio, il testo del messaggio e il valore di timeout per il server. Le notifiche vengono recapitate tramite una coda di Service Broker di cui le applicazioni possono eseguire il polling delle notifiche disponibili.  
  
 La sintassi delle opzioni delle notifiche delle query è la seguente:  
  
 `service=<service-name>[;(local database=<database> | broker instance=<broker instance>)]`  
  
 Esempio:  
  
 `service=mySSBService;local database=mydb`  
  
 Le sottoscrizioni di notifica sopravvivono al processo che le avvia, in quanto un'applicazione può creare una sottoscrizione di notifica e quindi terminare. La sottoscrizione rimane valida e la notifica verrà creata se i dati vengono modificati nel periodo di timeout specificato al momento della creazione della sottoscrizione. Una notifica viene identificata dalla query eseguita, dalle opzioni di notifica e dal testo del messaggio e può essere annullata impostandone il valore di timeout su zero.  
  
 Le notifiche vengono inviate una sola volta. Per la notifica continua delle modifiche dei dati, è necessario creare una nuova sottoscrizione rieseguendo la query al termine dell'elaborazione di ogni notifica.  
  
 Le applicazioni del driver OLE DB per SQL Server in genere ricevono notifiche mediante il comando [!INCLUDE[tsql](../../../includes/tsql-md.md)] [RECEIVE](../../../t-sql/statements/receive-transact-sql.md) che consente di leggerle dalla coda associata al servizio specificato nelle opzioni di notifica.  
  
> [!NOTE]  
>  I nomi di tabella devono essere qualificati nelle query per le quali è necessaria la notifica, ad esempio `dbo.myTable`, e devono essere qualificati con nomi in due parti. La sottoscrizione non è valida se vengono utilizzati nomi in tre o quattro parti.  
  
 L'infrastruttura della notifica si basa su una caratteristica di accodamento introdotta in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. In genere, le notifiche generate sul server vengono inviate tramite queste code in modo da essere elaborate in un secondo momento.  
  
 Per utilizzare le notifiche delle query è necessario che sul server siano disponibili una coda e un servizio. Tali elementi possono essere creati utilizzando [!INCLUDE[tsql](../../../includes/tsql-md.md)] come illustrato di seguito:  
  
```  
CREATE QUEUE myQueue  
CREATE SERVICE myService ON QUEUE myQueue   
  
([https://schemas.microsoft.com/SQL/Notifications/PostQueryNotification])  
```  
  
> [!NOTE]  
>  Come indicato sopra, il servizio deve usare il contratto predefinito.  
  
## <a name="ole-db-driver-for-sql-server"></a>Driver OLE DB per SQL Server  
 Il Driver OLE DB per SQL Server supporta la notifica di tipo consumer nella modifica di set di righe. Il consumer riceve una notifica a ogni fase di modifica dei set di righe e a ogni tentativo di modifica.  
  
> [!NOTE]  
>  Il passaggio di una query di notifica al server mediante **ICommand::Execute** rappresenta l'unico modo valido per sottoscrivere le notifiche delle query con il driver OLE DB per SQL Server.  
  
### <a name="the-dbpropsetsqlserverrowset-property-set"></a>Set di proprietà DBPROPSET_SQLSERVERROWSET  
 Per supportare le notifiche delle query tramite OLE DB, il driver OLE DB per SQL Server aggiunge le nuove proprietà seguenti al set di proprietà DBPROPSET_SQLSERVERROWSET.  
  
|nome|Tipo|Descrizione|  
|----------|----------|-----------------|  
|SSPROP_QP_NOTIFICATION_TIMEOUT|VT_UI4|Numero di secondi durante i quali la notifica di query deve rimanere attiva.<br /><br /> Il valore predefinito è 432,000 secondi (5 giorni). Il valore minimo è 1 secondo e il valore massimo è 2^31-1 secondi.|  
|SSPROP_QP_NOTIFICATION_MSGTEXT|VT_BSTR|Testo del messaggio di notifica. Tale testo è definito dall'utente e non presenta un formato predefinito.<br /><br /> Per impostazione predefinita, la stringa è vuota. È possibile specificare un messaggio utilizzando da 1 a 2000 caratteri.|  
|SSPROP_QP_NOTIFICATION_OPTIONS|VT_BSTR|Opzioni di notifica delle query. Tali opzioni vengono specificate in una stringa con la sintassi *nome*=*valore*. L'utente è responsabile della creazione del servizio e della lettura delle notifiche all'esterno della coda.<br /><br /> Il valore predefinito è una stringa vuota.|  
  
 Il commit della sottoscrizione di notifica viene sempre eseguito, indipendentemente dall'esecuzione dell'istruzione in una transazione utente o in modalità di commit automatico o a prescindere se la transazione in cui è stata eseguita l'istruzione sia stata sottoposta a commit o a rollback. La notifica server viene generata in seguito a una delle condizioni di notifica non valide seguenti: modifica dello schema o dei dati sottostanti o raggiungimento del periodo di timeout, a seconda dell'evento che si verifica per primo. Le registrazioni della notifica vengono eliminate subito dopo essere state generate. In seguito alla ricezione delle notifiche, è pertanto necessario che venga effettuata nuovamente la sottoscrizione se si desidera ottenere ulteriori aggiornamenti.  
  
 Un'altra connessione o un altro thread può verificare la presenza di notifiche nella coda di destinazione. Esempio:  
  
```  
WAITFOR (RECEIVE * FROM MyQueue);   // Where MyQueue is the queue name.   
```  
  
 Si noti che SELECT * non elimina la voce dalla coda, diversamente da RECEIVE \* FROM. Di conseguenza un thread del server viene bloccato se la coda è vuota. Se al momento della chiamata sono presenti voci nella coda, vengono restituite immediatamente. In caso contrario, la chiamata resta in attesa finché non viene creata una voce della coda.  
  
```  
RECEIVE * FROM MyQueue  
```  
  
 Questa istruzione restituisce immediatamente un set di risultati vuoto se la coda è vuota. In caso contrario, restituisce tutte le notifiche della coda.  
  
 Se le proprietà SSPROP_QP_NOTIFICATION_MSGTEXT e SSPROP_QP_NOTIFICATION_OPTIONS sono diverse da Null e non vuote, l'intestazione TDS delle notifiche delle query contenente le tre proprietà definite sopra viene inviata al server a ogni esecuzione del comando. Se una di esse è Null o vuota, l'intestazione non viene inviata e viene generato DB_E_ERRORSOCCURRED, o DB_S_ERRORSOCCURRED se le proprietà sono entrambe contrassegnate come facoltative, e il valore dello stato viene impostato su DBPROPSTATUS_BADVALUE. La convalida viene effettuata in fase di esecuzione/preparazione. Analogamente, DB_S_ERRORSOCCURED viene generato quando le proprietà della notifica di query sono impostate per le connessioni alle versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precedenti a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Il valore dello stato in questo caso è DBPROPSTATUS_NOTSUPPORTED.  
  
 L'avvio di una sottoscrizione non garantisce il corretto recapito dei messaggi successivi. Inoltre, non viene effettuato alcun controllo della validità del nome di servizio specificato.  
  
> [!NOTE]  
>  La preparazione delle istruzioni non causerà mai l'avvio della sottoscrizione. Tale operazione verrà effettuata solo mediante l'esecuzione delle istruzioni. L'uso dei servizi OLE DB di base non influisce sulle notifiche delle query.  
  
 Per altre informazioni sul set di proprietà DBPROPSET_SQLSERVERROWSET, vedere [proprietà set di righe e i comportamenti](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md).  
  

  
## <a name="see-also"></a>Vedere anche  
 [Driver OLE DB per funzionalità di SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)     
  
  
