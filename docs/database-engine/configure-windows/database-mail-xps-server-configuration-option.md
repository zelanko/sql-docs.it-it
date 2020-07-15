---
title: Opzione di configurazione del server Stored procedure estese di posta elettronica database | Microsoft Docs
description: Informazioni sull'opzione "DatabaseMail XPs". Scoprire i diversi modi per attivare questa opzione in modo da poter usare Posta elettronica database in SQL Server.
ms.custom: ''
ms.date: 11/27/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Database Mail XPs option
- Database Mail [SQL Server], enabling
ms.assetid: e22c4e63-1792-473b-af11-14a7931ca9ed
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0d495017b9bf2a5f58a5a880f1ce9696976ebd50
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772569"
---
# <a name="database-mail-xps-server-configuration-option"></a>Opzione di configurazione del server Database Mail XPs

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Usare l'opzione **Stored procedure estese di posta elettronica database** per abilitare Posta elettronica database nel server. I valori possibili sono:  
  
- `0`: Posta elettronica database non è disponibile (impostazione predefinita).  
  
- `1`: Posta elettronica database è disponibile.  
  
 L'impostazione diventa effettiva immediatamente e non richiede l'arresto e il riavvio del server.  
  
 Dopo aver abilitato Posta elettronica database, è necessario configurare un database host di Posta elettronica database per l'utilizzo di tale funzionalità.  
  
 La configurazione di Posta elettronica database tramite la **Configurazione guidata posta elettronica database** ne abilita le stored procedure estese nel database `msdb`. Se si usa la **Configurazione guidata posta elettronica database** non è necessario usare l'esempio `sp_configure` riportato di seguito.  
  
 L'impostazione dell'opzione **Stored procedure estese di posta elettronica database** su `0` impedisce l'avvio di Posta elettronica database. Se quando si imposta l'opzione su `0` l'applicazione è in esecuzione, continuerà a essere eseguita e a inviare la posta fino a quando non rimane inattiva per il tempo configurato nell'opzione `DatabaseMailExeMinimumLifeTime`.  
  
## <a name="examples"></a>Esempi
 Nel codice di esempio seguente vengono abilitate le stored procedure estese di Posta elettronica database.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Database Mail XPs', 1;  
GO  
RECONFIGURE  
GO  
```  

Nel codice di esempio seguente vengono abilitate le stored procedure estese di Posta elettronica database, se non sono ancora abilitate.

```sql
IF EXISTS (
    SELECT 1 FROM sys.configurations 
    WHERE NAME = 'Database Mail XPs' AND VALUE = 0)
BEGIN
  PRINT 'Enabling Database Mail XPs'
  EXEC sp_configure 'show advanced options', 1;  
  RECONFIGURE
  EXEC sp_configure 'Database Mail XPs', 1;  
  RECONFIGURE  
END
```

## <a name="see-also"></a>Vedere anche
[Posta elettronica database](../../relational-databases/database-mail/database-mail.md)  
