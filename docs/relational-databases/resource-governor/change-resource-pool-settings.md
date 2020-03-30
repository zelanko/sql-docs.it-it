---
title: Modificare le impostazioni del pool di risorse | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool alter
- resource pools [SQL Server], alter
ms.assetid: 49438285-a011-4dac-bd4f-f35cd90fda61
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 8549b5a3a1675353ad0adce42fc63a460f893cae
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "72905021"
---
# <a name="change-resource-pool-settings"></a>Modificare le impostazioni del pool di risorse
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  È possibile modificare le impostazioni di un pool di risorse utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#LimitationsRestrictions), [Autorizzazioni](#Permissions)  
  
-   **Per modificare le impostazioni per un pool di risorse usando:**  [SQL Server Management Studio](#ChgRPProp), [Transact-SQL](#ChgRPTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 La percentuale massima della CPU deve essere uguale o maggiore della percentuale minima della CPU. La percentuale massima della memoria deve essere uguale o maggiore della percentuale minima della memoria.  
  
 La somma delle percentuali minime della CPU e delle percentuali minime della memoria per tutti i pool di risorse non deve superare 100.  
  
###  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per modificare le impostazioni di un pool di risorse è necessaria l'autorizzazione CONTROL SERVER.  
  
##  <a name="change-resource-pool-settings-using-sql-server-management-studio"></a><a name="ChgRPProp"></a> Modificare le impostazioni di un pool di risorse utilizzando SQL Server Management Studio  
 **Per modificare le impostazioni di un pool di risorse utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire Esplora oggetti ed espandere in modo ricorsivo il nodo **Gestione** fino a **Pool di risorse**incluso.  
  
2.  Fare clic con il pulsante destro del mouse sul pool di risorse da modificare, quindi scegliere **Proprietà**.  
  
3.  Nella pagina **Proprietà di Resource Governor** selezionare la riga per il pool di risorse nella griglia **Pool di risorse** se non è selezionata automaticamente.  
  
4.  Selezionare o fare doppio clic sulle celle della riga da modificare e immettere i nuovi valori.  
  
5.  Per salvare le modifiche, fare clic su **OK**.  

##  <a name="change-resource-pool-settings-using-transact-sql"></a><a name="ChgRPTSQL"></a> Modificare le impostazioni di un pool di risorse utilizzando Transact-SQL  
 **Per modificare le impostazioni di un pool di risorse utilizzando [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  Eseguire l'istruzione **ALTER RESOURCE POOL** o **ALTER EXTERNAL RESOURCE POOL** specificando i valori delle proprietà da modificare.  
  
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
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [Abilitare Resource Governor](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Creare un pool di risorse](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [Eliminare un pool di risorse](../../relational-databases/resource-governor/delete-a-resource-pool.md)   
 [Gruppo di carico di lavoro di Resource Governor](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Funzione di classificazione di Resource Governor](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)  
  
  
