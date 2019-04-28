---
title: Stati del database | Microsoft Docs
ms.custom: ''
ms.date: 07/15/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.DATABASESTATES.F1
helpviewer_keywords:
- emergency database state [SQL Server]
- verifying database states
- viewing database states
- displaying database states
- database states [SQL Server]
- current database state
- offline database state [SQL Server]
- suspect database state
- recovery pending database state [SQL Server]
- states [SQL Server], databases
- online database state
- states [SQL Server]
- restoring database state [SQL Server]
ms.assetid: b7f1f111-ca73-4a89-b567-a98d64d6ecb3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5b6e2072e06e1ea5d61802a4c6a006737bc04762
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62871697"
---
# <a name="database-states"></a>Stati del database
  Lo stato di un database è sempre specifico e può essere ad esempio ONLINE, OFFLINE o SUSPECT. Per verificare lo stato corrente di un database, selezionare la colonna **state_desc** nella vista del catalogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) oppure la proprietà **Status** nella funzione [DATABASEPROPERTYEX](/sql/t-sql/functions/databasepropertyex-transact-sql) .  
  
## <a name="database-state-definitions"></a>Definizioni degli stati del database  
 Nella tabella seguente sono riportate le definizioni degli stati del database.  
  
|State|Definizione|  
|-----------|----------------|  
|ONLINE|Il database è disponibile per l'accesso. Il filegroup primario è online sebbene sia possibile che la fase di annullamento del recupero non sia stata completata.|  
|OFFLINE|Il database non è disponibile. Un database viene portato offline a seguito di un'azione esplicita da parte dell'utente e rimane tale finché l'utente non interviene. È ad esempio possibile che il database sia stato portato offline per consentire lo spostamento di un file su un nuovo disco. In tal caso verrà portato nuovamente online dopo il completamento dell'operazione di spostamento.|  
|RESTORING|È in corso il ripristino di uno o più file del filegroup primario oppure il ripristino di uno o più file secondari viene eseguito offline. Il database non è disponibile.|  
|RECOVERING|È in corso il recupero del database. Il processo di recupero è uno stato temporaneo. Il database verrà portato automaticamente online se il recupero ha esito positivo. Se invece ha esito negativo, il database verrà contrassegnato come sospetto. Il database non è disponibile.|  
|RECOVERY PENDING|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ha rilevato un errore correlato a una risorsa durante il recupero. Il database non è danneggiato, tuttavia i file potrebbero risultare mancanti oppure limitazioni relative alle risorse di sistema ne potrebbero impedire l'avvio. Il database non è disponibile. Per risolvere il problema che ha causato l'errore e consentire il completamento del processo di recupero, è necessario un ulteriore intervento da parte dell'utente.|  
|SUSPECT|Almeno il filegroup primario è sospetto e potrebbe essere danneggiato. Non è possibile recuperare il database durante l'avvio di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Il database non è disponibile. Per risolvere il problema, è necessario l'intervento dell'utente.|  
|EMERGENCY|L'utente ha modificato il database e impostato lo stato su EMERGENCY. Il database è in modalità utente singolo e può corretto o ripristinato. Il database è contrassegnato come READ_ONLY, la registrazione è disabilitata e l'accesso è limitato ai soli membri del ruolo predefinito del server **sysadmin** . L'opzione EMERGENCY viene usata principalmente per attività di risoluzione dei problemi. È ad esempio possibile impostare lo stato EMERGENCY per un database contrassegnato come sospetto in modo da consentire all'amministratore di sistema di accedere in sola lettura al database. Solo i membri del ruolo predefinito del server **sysadmin** possono impostare lo stato EMERGENCY per un database.|  
  
## <a name="related-content"></a>Contenuto correlato  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
 [Stati di mirroring &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [Stati dei file](file-states.md)  
  
  
