---
title: Tabelle di Base di sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system base tables [SQL Server]
- hobt [SQL Server]
- base tables
ms.assetid: 31f2df90-651f-4699-8067-19f59b60904f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 43f5e96a280614d3f69472c7d794489bf1a5ba58
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029566"
---
# <a name="system-base-tables"></a>Tabelle di base di sistema
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Le tabelle di base di sistema sono le tabelle sottostanti in cui vengono effettivamente archiviati i metadati per un database specifico. Il **master** database è speciale in questo senso perché contiene alcune tabelle aggiuntive che non si trovano in uno qualsiasi degli altri database. Queste tabelle contengono metadati persistenti il cui ambito è esteso all'intero server.  
  
> [!IMPORTANT]  
>  Le tabelle di base di sistema sono utilizzate solo in [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e non sono destinate all'utilizzo da parte di tutti gli utenti. Sono soggette a modifiche e la compatibilità non è garantita.  
  
## <a name="system-base-table-metadata"></a>Metadati della tabella di base di sistema  
 Un utente autorizzato che dispone dell'autorizzazione CONTROL, ALTER o VIEW DEFINITION in un database può visualizzare i metadati della tabella di base di sistema nel **Sys. Objects** vista del catalogo. L'utente autorizzato può anche risolvere i nomi e gli ID delle tabelle di base di sistema dell'oggetto tramite le funzioni predefinite, ad esempio [OBJECT_NAME](../../t-sql/functions/object-name-transact-sql.md) e [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md).  
  
 Per associare una tabella di base di sistema, un utente deve connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando la connessione amministrativa dedicata (DAC). Se si tenta di eseguire una query SELECT da una tabella di base di sistema senza connettersi tramite DAC, viene generato un errore.  
  
> [!IMPORTANT]  
>  L'accesso alle tabelle di base di sistema tramite DAC è progettato solo per il personale di [!INCLUDE[msCoName](../../includes/msconame-md.md)] e non è uno scenario di supporto per i clienti.  
  
## <a name="system-base-tables"></a>Tabelle di base di sistema  
 Nella tabella seguente viene indicata e descritta ogni un tabella di base sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Tabella di base|Descrizione|  
|----------------|-----------------|  
|**Sys.sysschobjs**|Esiste in ogni database. Ogni riga rappresenta un oggetto del database.|  
|**Sys.sysbinobjs**|Esiste in ogni database. Contiene una riga per ogni entità Service Broker del database. Le entità Service Broker includono gli elementi seguenti:<br /><br /> Tipo di messaggio<br /><br /> Contratto servizio<br /><br /> Service<br /><br /> I nomi e i tipi utilizzano regole di confronto binarie predefinite.|  
|**Sys.sysclsobjs**|Esiste in ogni database. Contiene una riga per ogni entità classificata che condivide le stesse proprietà comuni che includono gli elementi seguenti:<br /><br /> Assembly<br /><br /> Dispositivo di backup<br /><br /> Catalogo full-text<br /><br /> partition (funzione)<br /><br /> Schema di partizione<br /><br /> Filegroup<br /><br /> Chiave di offuscamento|  
|**Sys.sysnsobjs**|Esiste in ogni database. Contiene una riga per ogni entità dell'ambito dello spazio dei nomi. Questa tabella viene utilizzata per archiviare le entità di raccolta XML.|  
|**Sys.syscolpars**|Esiste in ogni database. Contiene una riga per ogni colonna di una tabella, vista o funzione con valori di tabella. Contiene anche righe per ogni parametro di una procedura o funzione.|  
|**Sys.systypedsubobjs**|Esiste in ogni database. Contiene una riga per ogni sottoentità tipizzata. In questa categoria rientrano solo i parametri relativi alla funzione di partizione.|  
|**Sys.sysidxstats**|Esiste in ogni database. Contiene una riga per ogni indice o statistica di tabelle e viste indicizzate<br /><br /> Nota: Ogni indice (eccetto heap) è associata una statistica che ha lo stesso nome dell'indice.|  
|**Sys.sysiscols**|Esiste in ogni database. Contiene una riga per ogni indice persistente e colonna delle statistiche.|  
|**Sys.sysscalartypes**|Esiste in ogni database. Contiene una riga per ogni tipo di sistema o tipo definito dall'utente.|  
|**Sys.sysdbreg**|Esiste nel **master** solo del database. Contiene una riga per ogni database registrato.|  
|**Sys.sysxsrvs**|Esiste nel **master** solo del database. Contiene una riga per ogni server locale, collegato o remoto.|  
|**Sys.sysrmtlgns**|Questa tabella di base di sistema esiste nel **master** solo del database. Contiene una riga per ogni mapping di account di accesso remoto. Viene utilizzata per eseguire il mapping tra gli account di accesso in ingresso che risultano provenire da un server corrispondente e un account di accesso locale effettivo.|  
|**Sys.syslnklgns**|Esiste nel **master** solo del database. Contiene una riga per ogni mapping di account di accesso collegato. I mapping di account di accesso collegati vengono utilizzati da chiamate di procedure remote e query distribuite che provengono da un server locale a un server collegato corrispondente.|  
|**Sys.sysxlgns**|Esiste nel **master** solo del database. Contiene una riga per ogni entità di server.|  
|**Sys.sysdbfiles**|Esiste in ogni database. Se la colonna **dbid** è uguale a zero, la riga rappresenta un file appartenente a questo database. Nel **master** del database, la colonna **dbid** può essere diverso da zero. In questo caso, la riga rappresenta un file master.|  
|**Sys.sysusermsg**|Esiste nel **master** solo del database. Ogni riga rappresenta un messaggio di errore definito dall'utente.|  
|**Sys.sysprivs**|Esiste in ogni database. Contiene una riga per ogni database o autorizzazione a livello di server.<br /><br /> Nota: Le autorizzazioni a livello di server vengono archiviate nel **master** database.|  
|**Sys.sysowners**|Esiste in ogni database. Ogni riga rappresenta un'entità di database.|  
|**Sys.sysobjkeycrypts**|Esiste in ogni database. Contiene una riga per ogni chiave simmetrica, crittografia o proprietà crittografica associata a un oggetto.|  
|**Sys.syscerts**|Esiste in ogni database. Contiene una riga per ogni certificato di un database.|  
|**sysasymkeys**|Esiste in ogni database. Ogni riga rappresenta una chiave asimmetrica.|  
|**Sys.ftinds**|Esiste in ogni database. Contiene una riga per ogni indice full-text del database.|  
|**Sys.sysxprops**|Esiste in ogni database. Contiene una riga per ogni proprietà estesa.|  
|**Sys.sysallocunits**|Esiste in ogni database. Contiene una riga per ogni unità di allocazione di archiviazione.|  
|**sysrowsets**|Esiste in ogni database. Contiene una riga per ogni set di righe della partizione per un indice o un heap.|  
|**Sys.sysrowsetrefs**|Esiste in ogni database. Contiene una riga per ogni riferimento di indice a un set di righe.|  
|**Sys.syslogshippers**|Esiste nel **master** solo del database. Contiene una riga per ogni server di controllo del mirroring del database.|  
|**Sys.sysremsvcbinds**|Esiste in ogni database. Contiene una riga per ogni associazione al servizio remoto.|  
|**Sys.sysconvgroup**|Esiste in ogni database. Contiene una riga per ogni istanza di servizio di Service Broker.|  
|**Sys.sysxmitqueue**|Esiste in ogni database. Contiene una riga per ogni coda di trasmissione di Service Broker.|  
|**Sys.sysdesend**|Esiste in ogni database. Contiene una riga per ogni endpoint di invio di una conversazione di Service Broker.|  
|**Sys.sysdercv**|Esiste in ogni database. Contiene una riga per ogni endpoint di ricezione di una conversazione di Service Broker.|  
|**Sys.sysendpts**|Esiste nel **master** solo del database. Contiene una riga per ogni endpoint creato nel server.|  
|**Sys.syswebmethods**|Esiste nel **master** solo del database. Contiene una riga per ogni metodo SOAP definito in un endpoint HTTP attivato per SOAP creato nel server.|  
|**Sys.sysqnames**|Esiste in ogni database. Contiene una riga per ogni spazio dei nomi o nome completo a un token ID di 4 byte.|  
|**Sys.sysxmlcomponent**|Esiste in ogni database. Ogni riga rappresenta un componente di XML Schema.|  
|**Sys.sysxmlfacet**|Esiste in ogni database. Contiene una riga per ogni facet XML (restrizione) di definizione del tipo XML.|  
|**Sys.sysxmlplacement**|Esiste in ogni database. Contiene una riga per ogni posizione XML dei componenti XML.|  
|**Sys.syssingleobjrefs**|Esiste in ogni database. Contiene una riga per ogni riferimento N-a-1 generale.|  
|**Sys.sysmultiobjrefs**|Esiste in ogni database. Contiene una riga per ogni riferimento N-a-N generale.|  
|**Sys.sysobjvalues**|Esiste in ogni database. Contiene una riga per ogni proprietà del valore generale di un'entità.|  
|**Sys.sysguidrefs**|Esiste in ogni database. Contiene una riga per ogni riferimento a ID classificati GUID.|  
  
  
