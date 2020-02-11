---
title: Rimozione di una stored procedure estesa da SQL Server | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62512026"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>Rimozione di una stored procedure estesa da SQL Server
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]Usare invece l'integrazione con CLR.  
  
 Per eliminare ogni funzione di stored procedure estesa in una DLL di stored procedure estesa definita dall'utente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario che un amministratore di sistema esegua il stored procedure di sistema **sp_dropextendedproc** , specificando il nome della funzione e il nome della dll in cui risiede la funzione. Ad esempio, questo comando rimuove la funzione **xp_hello**, che si trova in una dll denominata xp_hello. dll [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], da:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 A partire [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]da, **sp_dropextendedproc** non elimina le stored procedure estese di sistema. L'amministratore di sistema deve invece negare l'autorizzazione EXECUTE per il stored procedure esteso al ruolo **public** .  
  
## <a name="see-also"></a>Vedere anche  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
