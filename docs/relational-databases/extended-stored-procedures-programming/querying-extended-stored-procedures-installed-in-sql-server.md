---
title: L'esecuzione di query Extended Stored procedure installate in SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f2d5584d70b32764fd9c7e11a53131626e9df444
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62742227"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>Esecuzione di query su stored procedure estese installate in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Oggetto [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utente autenticato può visualizzare attualmente definito stored procedure estese e il nome della DLL per ciascuna delle quali appartiene eseguendo il **sp_helpextendedproc** procedure di sistema. Ad esempio, l'esempio seguente restituisce le DLL a cui **xp_hello** appartiene:  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 Se **sp_helpextendedproc** viene eseguita senza specificare una stored procedure estesa, tutte le stored procedure estese e le relative DLL sono visualizzati.  
  
> [!IMPORTANT]  
>  Verranno restituite le informazioni solo per le stored procedure estese di cui l'utente connesso è il proprietario o di cui dispone delle autorizzazioni appropriate. Solo i membri del **sysadmin** ruolo predefinito del server e il **db_owner**, **db_securityadmin**e il **db_ddladmin** predefinito del database i ruoli è possono visualizzare informazioni per tutte le stored procedure estese.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_helpextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [sp_addextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
