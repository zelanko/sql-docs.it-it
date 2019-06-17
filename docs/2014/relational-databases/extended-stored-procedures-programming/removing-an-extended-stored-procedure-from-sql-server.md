---
title: Rimozione di un'estesa Stored Procedure da SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- deleting extended stored procedures
- removing extended stored procedures
- extended stored procedures [SQL Server], removing
- dropping extended stored procedures
ms.assetid: 7827e574-3f59-4279-9a9b-532582e041cb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bcb58ac180861641803147d1dfea621bd52df9a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62512026"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>Rimozione di una stored procedure estesa da SQL Server
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Utilizzare invece la funzionalità di integrazione con CLR.  
  
 Per eliminare ogni funzione di stored procedure estesa in una definite dall'utente DLL stored procedure estesa, un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] amministratore di sistema deve eseguire il **sp_dropextendedproc** stored procedure, che specifica il nome di sistema il funzione e il nome della DLL in cui risiede la funzione. Ad esempio, questo comando rimuove la funzione **xp_hello**, che si trova in una DLL denominata xp_hello. dll, da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 A partire [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], **sp_dropextendedproc** non elimina le stored procedure estese di sistema. Al contrario, l'amministratore di sistema può negare l'autorizzazione EXECUTE per la stored procedure estesa per il **pubblica** ruolo.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
