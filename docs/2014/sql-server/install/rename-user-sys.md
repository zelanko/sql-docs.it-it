---
title: Rinominare l'utente sys | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- sys user names [SQL Server]
ms.assetid: d622d646-83e4-4b6f-9a21-77b301af04b5
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8e227e4d382dac627626b977427aae05d0295744
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582334"
---
# <a name="rename-user-sys"></a>Rinominare l'utente sys
  È stato rilevato il nome utente **sys** in un database. Questo nome è riservato. Rinominare l'utente prima di eseguire l'aggiornamento. Se l'utente non viene rinominato, il database si troverà in stato sospetto dopo il processo di aggiornamento e non sarà disponibile finché non viene portato online.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrizione  
 Utente **sys** è riservato.  
  
## <a name="corrective-action"></a>Azione correttiva  
  
### <a name="before-upgrade-procedure"></a>Procedura precedente all'aggiornamento  
 Prima dell'aggiornamento, in ogni database che contiene l'utente **sys**, eseguire le operazioni seguenti:  
  
1.  Creare un nuovo utente.  
  
2.  Usare le istruzioni seguenti per visualizzare tutte le autorizzazioni concesse dall'utente **sys** e concesse all'utente **sys**.  
  
    ```  
    -- Return permissions granted by user sys.  
    SELECT * FROM sysprotects WHERE grantor = USER_ID('sys')  
    -- Return permissions granted to user sys.  
    SELECT * FROM sysprotects WHERE uid = USER_ID('sys')  
    ```  
  
3.  Trasferire la proprietà di tutti gli oggetti appartenenti **sys** al nuovo utente, usare **sp_changeobjectowner**.  
  
4.  Eliminare l'utente **sys**.  
  
5.  Per ripristinare le autorizzazioni originali acquisite nel passaggio 2, usare la clausola AS *new_user* clausola dell'istruzione GRANT.  
  
6.  Modificare gli script in modo che facciano riferimento al nuovo utente. Ad esempio, gli script che contengono istruzioni come `SELECT * FROM sys.my`_`table` devono essere modificati in `SELECT * FROM new_user.my_table`.  
  
### <a name="after-upgrade-procedure"></a>Procedura successiva all'aggiornamento  
 Se l'utente **sys** è stato rinominato non prima dell'aggiornamento, eseguire le operazioni seguenti:  
  
1.  Eseguire l'istruzione `ALTER DATABASE db_name SET ONLINE`. Il database sarà in modalità SINGLE_USER.  
  
2.  Seguire tutti i passaggi riportati nella sezione "Procedura precedente all'aggiornamento".  
  
3.  Eseguire l'istruzione `ALTER DATABASE db_name SET MULTI_USER`.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
