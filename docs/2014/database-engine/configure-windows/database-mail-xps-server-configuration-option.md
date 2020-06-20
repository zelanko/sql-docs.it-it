---
title: Opzione di configurazione del server Stored procedure estese di posta elettronica database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Database Mail XPs option
- Database Mail [SQL Server], enabling
ms.assetid: e22c4e63-1792-473b-af11-14a7931ca9ed
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 83e91bf5070362b1db56907a1c5b016cf816b968
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935362"
---
# <a name="database-mail-xps-server-configuration-option"></a>Opzione di configurazione del server Database Mail XPs
  Usare l'opzione **Stored procedure estese di posta elettronica database** per abilitare Posta elettronica database nel server. I valori possibili sono:  
  
-   **0** per indicare che Posta elettronica database non è disponibile (valore predefinito).  
  
-   **1** per indicare che Posta elettronica database è disponibile.  
  
 L'impostazione diventa effettiva immediatamente e non richiede l'arresto e il riavvio del server.  
  
 Dopo aver abilitato Posta elettronica database, è necessario configurare un database host di Posta elettronica database per l'utilizzo di tale funzionalità.  
  
 Quando l'applicazione Posta elettronica database viene configurata tramite **Configurazione guidata posta elettronica database** , le stored procedure estese dell'applicazione vengono abilitate nel database **msdb** . Se si esegue la **Configurazione guidata**, è possibile ignorare l'esempio **sp_configure** riportato di seguito.  
  
 L'impostazione dell'opzione **Stored procedure estese di posta elettronica database** su 0 impedisce l'avvio di Posta elettronica database. Se quando si imposta l'opzione su 0 l'applicazione è già in esecuzione, continuerà a essere eseguita fino a quando non rimane inattiva per il periodo di tempo impostato nell'opzione **DatabaseMailExeMinimumLifeTime** .  
  
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
  
## <a name="see-also"></a>Vedere anche  
 [Posta elettronica database](../../relational-databases/database-mail/database-mail.md)  
  
  
