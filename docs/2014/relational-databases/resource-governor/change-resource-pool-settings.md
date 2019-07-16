---
title: Modificare le impostazioni del pool di risorse | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool alter
- resource pools [SQL Server], alter
ms.assetid: 49438285-a011-4dac-bd4f-f35cd90fda61
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6392c8211e073183b68d2d04e9c949317d6a33a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68198948"
---
# <a name="change-resource-pool-settings"></a>Modificare le impostazioni del pool di risorse
  È possibile modificare le impostazioni di un pool di risorse utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#LimitationsRestrictions), [Autorizzazioni](#Permissions)  
  
-   **Per modificare le impostazioni per un pool di risorse usando:**  [SQL Server Management Studio](#ChgRPProp), [Transact-SQL](#ChgRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 La percentuale massima della CPU deve essere uguale o maggiore della percentuale minima della CPU. La percentuale massima della memoria deve essere uguale o maggiore della percentuale minima della memoria.  
  
 La somma delle percentuali minime della CPU e delle percentuali minime della memoria per tutti i pool di risorse non deve superare 100.  
  
###  <a name="Permissions"></a> Autorizzazioni  
 Per modificare le impostazioni di un pool di risorse è necessaria l'autorizzazione CONTROL SERVER.  
  
##  <a name="ChgRPProp"></a> Modificare le impostazioni di un pool di risorse utilizzando SQL Server Management Studio  
 **Per modificare le impostazioni di un pool di risorse utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire Esplora oggetti ed espandere in modo ricorsivo il nodo **Gestione** fino a **Pool di risorse**incluso.  
  
2.  Fare clic con il pulsante destro del mouse sul pool di risorse da modificare, quindi scegliere **Proprietà**.  
  
3.  Nella pagina **Proprietà di Resource Governor** selezionare la riga per il pool di risorse nella griglia **Pool di risorse** se non è selezionata automaticamente.  
  
4.  Selezionare o fare doppio clic sulle celle della riga da modificare e immettere i nuovi valori.  
  
5.  Per salvare le modifiche, fare clic su **OK**.  
  
##  <a name="ChgRPTSQL"></a> Modificare le impostazioni di un pool di risorse utilizzando Transact-SQL  
 **Per modificare le impostazioni di un pool di risorse utilizzando [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  Eseguire l'istruzione `ALTER RESOURCE POOL` specificando i valori di proprietà da modificare.  
  
2.  Eseguire l'istruzione **ALTER RESOURCE GOVERNOR RECONFIGURE** .  
  
### <a name="example-transact-sql"></a>Esempio (Transact-SQL)  
 Nell'esempio seguente viene modificata l'impostazione relativa alla percentuale massima della CPU per il pool di risorse denominato `poolAdhoc`.  
  
```  
ALTER RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 25);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Resource Governor](resource-governor.md)   
 [Abilitare Resource Governor](enable-resource-governor.md)   
 [Creare un pool di risorse](create-a-resource-pool.md)   
 [Eliminare un pool di risorse](delete-a-resource-pool.md)   
 [Gruppo di carico di lavoro di Resource Governor](resource-governor-workload-group.md)   
 [Funzione di classificazione di Resource Governor](resource-governor-classifier-function.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
