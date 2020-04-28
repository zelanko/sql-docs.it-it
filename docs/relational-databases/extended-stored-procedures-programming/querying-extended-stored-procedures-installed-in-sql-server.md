---
title: Esecuzione di query su stored procedure estese
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
ms.custom: seo-dt-2019
ms.openlocfilehash: 875d4f252058d442c91915eb69784507c39b2e94
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74095950"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>Esecuzione di query su stored procedure estese installate in SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Usare in alternativa l'integrazione CLR.  
  
 Un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utente autenticato può visualizzare le stored procedure estese attualmente definite e il nome della dll a cui appartiene, eseguendo la procedura **sp_helpextendedproc** sistema. Nell'esempio seguente viene restituita la DLL a cui appartiene **xp_hello** :  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 Se **sp_helpextendedproc** viene eseguita senza specificare una stored procedure estesa, vengono visualizzate tutte le stored procedure estese e le relative dll.  
  
> [!IMPORTANT]  
>  Verranno restituite le informazioni solo per le stored procedure estese di cui l'utente connesso è il proprietario o di cui dispone delle autorizzazioni appropriate. Solo i membri del ruolo predefinito del server **sysadmin** e del **db_owner**, **db_securityadmin**e i ruoli predefiniti del database **db_ddladmin** possono visualizzare le informazioni relative a tutte le stored procedure estese.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_helpextendedproc &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [sp_addextendedproc &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
