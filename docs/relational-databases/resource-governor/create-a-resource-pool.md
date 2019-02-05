---
title: Creare un pool di risorse | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- resource pools [SQL Server], create
- Resource Governor, resource pool create
ms.assetid: 44dd0567-a4c8-4c72-89ff-e76f6ddef344
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: 4fa512ba301aa1fc0c1783b96717545eca2790db
ms.sourcegitcommit: cebfa2610ea36e3c5ad510c214590035ecb499c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/04/2019
ms.locfileid: "55689764"
---
# <a name="create-a-resource-pool"></a>Creare un pool di risorse
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  È possibile creare un pool di risorse utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Per informazioni sulle entità dei pool di risorse, vedere [Pool di risorse di Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md).  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#LimitationsRestrictions), [Autorizzazioni](#Permissions)  
  
-   **Per creare un pool di risorse usando:**  [SQL Server Management Studio](#CreRPProp), [Transact-SQL](#CreRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 La percentuale massima della CPU deve essere uguale o maggiore della percentuale minima della CPU. La percentuale massima della memoria deve essere uguale o maggiore della percentuale minima della memoria.  
  
 La somma delle percentuali minime della CPU e delle percentuali minime della memoria per tutti i pool di risorse non deve superare 100.  
  
###  <a name="Permissions"></a> Permissions  
 Per creare un pool di risorse è necessaria l'autorizzazione CONTROL SERVER.  
  
##  <a name="CreRPProp"></a> Creare un pool di risorse utilizzando SQL Server Management Studio  
 **Per creare un pool di risorse utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire Esplora oggetti ed espandere in modo ricorsivo il nodo **Gestione** fino a **Resource Governor**incluso.  
  
2.  Fare clic con il pulsante destro del mouse su **Resource Governor**, quindi su **Proprietà**.  
  
3.  Nella griglia **Pool di risorse** fare clic sulla prima colonna nella riga vuota. Questa colonna è etichettata con un asterisco (*).  
  
4.  Fare doppio clic sulla cella vuota nella colonna **Nome** . Digitare il nome che si desidera utilizzare per il pool di risorse.  
  
5.  Selezionare o fare doppio clic su qualsiasi altra cella della riga che si desidera modificare e immettere i nuovi valori.  
  
6.  Per salvare le modifiche, fare clic su **OK**.  
  
##  <a name="CreRPTSQL"></a> Creare un pool di risorse utilizzando Transact-SQL  
 **Per creare un pool di risorse utilizzando [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  Eseguire l'istruzione [CREATE RESOURCE POOL](../../t-sql/statements/create-resource-pool-transact-sql.md) o [CREATE EXTERNAL RESOURCE POOL](../../t-sql/statements/create-external-resource-pool-transact-sql.md) specificando i valori delle proprietà da impostare.  
  
2.  Eseguire l'istruzione **ALTER RESOURCE GOVERNOR RECONFIGURE** .  
  
### <a name="example-transact-sql"></a>Esempio (Transact-SQL)  
 Nell'esempio seguente viene creato un pool di risorse denominato `poolAdhoc`.  
  
```  
CREATE RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 20);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [Abilitare Resource Governor](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Pool di risorse di Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Modificare le impostazioni del pool di risorse](../../relational-databases/resource-governor/change-resource-pool-settings.md)   
 [Eliminare un pool di risorse](../../relational-databases/resource-governor/delete-a-resource-pool.md)   
 [Configurare Resource Governor utilizzando un modello](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [Gruppo di carico di lavoro di Resource Governor](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Funzione di classificazione di Resource Governor](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)  
  
  
