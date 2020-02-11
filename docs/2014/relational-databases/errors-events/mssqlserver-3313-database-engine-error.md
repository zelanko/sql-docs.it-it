---
title: MSSQLSERVER_3313 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3313 (Database Engine error)
ms.assetid: a244227b-8553-42df-9435-034f906c4c74
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dc4d894dc03a53892b69f33dbf153cdd15fcf340
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62914519"
---
# <a name="mssqlserver_3313"></a>MSSQLSERVER_3313
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|3313|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|ERR_LOG_RID1|  
|Testo del messaggio|Durante il rollforward di un'operazione registrata nel database '%.*ls' si è verificato un errore in corrispondenza dell'ID del record di log ID %S_LSN. L'errore specifico viene in genere registrato in precedenza come errore nel registro eventi di Windows. Ripristinare il database da un backup completo oppure correggere il database.|  
  
## <a name="explanation"></a>Spiegazione  
 Si tratta di un errore di rollup per il recupero del rollforward. Tale errore ha determinato l'impostazione del database sullo stato SUSPECT. Il filegroup primario, e probabilmente altri filegroup, sono sospetti e possono essere danneggiati. Non è possibile recuperare il database durante l'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , pertanto non è disponibile. Per risolvere il problema, è necessario l'intervento dell'utente.  
  
 Se questo errore si verifica per **tempdb**, l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene arrestata.  
  
## <a name="user-action"></a>Azione dell'utente  
 Questo errore può essere causato da una condizione temporanea già presente nel sistema durante un determinato tentativo di avvio dell'istanza del server o di recupero di un database. Può inoltre essere causato da un errore permanente che si verifica ogni volta che si tenta di avviare il database. Per informazioni sulla causa, esaminare il registro eventi di Windows per cercare un errore precedente che indichi l'errore specifico.  
  
 Quando viene rilevata questa condizione di errore, generalmente in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono generati tre file nella cartella LOG[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ** di **. Nel file SQLDump*nnnn*.txt sono contenute informazioni diagnostiche avanzate relative agli errori, inclusi i dettagli sulla transazione e la pagina in cui si è verificato il problema. In genere, tali informazioni vengono utilizzate dal team del Servizio Supporto Tecnico Clienti per analizzare il motivo dell'errore.  
  
 Per informazioni sulla causa di questa occorrenza dell'errore 3313, esaminare il registro eventi di Windows per cercare un errore precedente che indichi l'errore specifico. L'azione appropriata dell'utente varia a seconda che le informazioni nel registro eventi di Windows indichino che l'errore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stato causato da una condizione temporanea o da un errore permanente. Per informazioni sulle azioni eseguibili dall'utente per risolvere l'errore 3313, vedere la documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [Ripristini di database completi &#40;modello di recupero con registrazione minima&#41;](../backup-restore/complete-database-restores-simple-recovery-model.md)   
 [MSSQLSERVER_824](mssqlserver-824-database-engine-error.md)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
