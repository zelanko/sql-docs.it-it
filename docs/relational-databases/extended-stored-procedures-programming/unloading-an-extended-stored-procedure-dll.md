---
title: Scaricamento di una DLL di stored procedure estesa | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
author: rothja
ms.author: jroth
ms.openlocfilehash: 76007876547b863f050d1e3fa494cbd8b30a5fc0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717653"
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>Caricamento di una DLL di stored procedure estesa
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Utilizzare invece la funzionalità di integrazione con CLR.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]carica una DLL di stored procedure estesa non appena viene effettuata una chiamata a una delle funzioni della dll. La DLL rimane caricata fino a che il server non viene spento o fino a che l'amministratore di sistema non utilizza l'istruzione DBCC per scaricarla. Ad esempio, questo comando Scarica il **xp_hello.dll**, consentendo all'amministratore di sistema di copiare una versione più recente di questo file nella directory senza arrestare il server:  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [DBCC dllname &#40;FREE&#41; &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)  
  
  
