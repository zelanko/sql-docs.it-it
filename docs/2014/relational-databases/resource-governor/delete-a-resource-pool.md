---
title: Eliminare un pool di risorse | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool delete
- resource pools [SQL Server], delete
ms.assetid: 3bdd348b-6582-4ffa-80ef-d49e50596ce5
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a67b0e2262fa3007597091b6087cc937bb0f3276
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063623"
---
# <a name="delete-a-resource-pool"></a>Eliminare un pool di risorse
  È possibile eliminare un pool di risorse utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o Transact-SQL.  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#LimitationsRestrictions), [Autorizzazioni](#Permissions)  
  
-   **Per eliminare un pool di risorse usando:** [SQL Server Management Studio](#DelRPSSMS), [Transact-SQL](#DelRPTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
 Non è possibile eliminare un pool di risorse contenente gruppi di carico di lavoro.  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 Non è possibile eliminare pool di risorse predefiniti o interni di Resource Governor. Non è possibile eliminare un pool di risorse contenente gruppi di carico di lavoro. Per altre informazioni, vedere [Delete a Workload Group](delete-a-workload-group.md).  
  
###  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per eliminare un pool di risorse è necessaria l'autorizzazione CONTROL SERVER.  
  
##  <a name="delete-a-resource-pool-using-object-explorer"></a><a name="DelRPSSMS"></a> Eliminare un pool di risorse utilizzando Esplora oggetti  
 **Per eliminare un pool di risorse utilizzando SQL Server Management Studio**  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire Esplora oggetti ed espandere in modo ricorsivo il nodo **Gestione** fino a **Resource Governor**incluso.  
  
2.  Fare clic con il pulsante destro del mouse sul pool di risorse da eliminare, quindi scegliere **Elimina**.  
  
3.  Nella finestra **Elimina oggetto** , il pool di risorse è indicato nell'elenco **Oggetto da eliminare** . Per eliminare il pool di risorse, fare clic su **OK**.  
  
    > [!NOTE]  
    >  Se si tenta di eliminare un pool di risorse in cui è contenuto un gruppo di carico di lavoro, si verificherà un errore.  
  
##  <a name="delete-a-resource-pool-using-transact-sql"></a><a name="DelRPTSQL"></a> Eliminare un pool di risorse utilizzando Transact-SQL  
 **Per eliminare un pool di risorse utilizzando Transact-SQL**  
  
1.  Eseguire l'istruzione `DROP RESOURCE POOL` specificando il nome del pool di risorse da eliminare.  
  
2.  Eseguire l'istruzione **ALTER RESOURCE GOVERNOR RECONFIGURE** .  
  
### <a name="example-transact-sql"></a>Esempio (Transact-SQL)  
 Nell'esempio seguente viene eliminato un gruppo di carico di lavoro denominato `poolAdhoc`.  
  
```  
DROP RESOURCE POOL poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Resource Governor](resource-governor.md)   
 [Pool di risorse di Resource Governor](resource-governor-resource-pool.md)   
 [Creare un pool di risorse](create-a-resource-pool.md)   
 [Modificare le impostazioni del pool di risorse](change-resource-pool-settings.md)   
 [Gruppo di carico di lavoro di Resource Governor](resource-governor-workload-group.md)   
 [Funzione di classificazione di Resource Governor](resource-governor-classifier-function.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-workload-group-transact-sql)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
