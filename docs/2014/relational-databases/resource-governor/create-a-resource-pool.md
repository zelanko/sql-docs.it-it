---
title: Creare un pool di risorse | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- resource pools [SQL Server], create
- Resource Governor, resource pool create
ms.assetid: 44dd0567-a4c8-4c72-89ff-e76f6ddef344
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f4d18ef352c3e5ab6342e573d16bc3deaed5db72
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68211998"
---
# <a name="create-a-resource-pool"></a>Creare un pool di risorse
  È possibile creare un pool di risorse utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Prima di iniziare:**  [limitazioni e restrizioni](#LimitationsRestrictions), [autorizzazioni](#Permissions)  
  
-   **Per creare un pool di risorse usando:**  [SQL Server Management Studio](#CreRPProp), [Transact-SQL](#CreRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 La percentuale massima della CPU deve essere uguale o maggiore della percentuale minima della CPU. La percentuale massima della memoria deve essere uguale o maggiore della percentuale minima della memoria.  
  
 La somma delle percentuali minime della CPU e delle percentuali minime della memoria per tutti i pool di risorse non deve superare 100.  
  
###  <a name="Permissions"></a> Autorizzazioni  
 Per creare un pool di risorse è necessaria l'autorizzazione CONTROL SERVER.  
  
##  <a name="CreRPProp"></a>Creare un pool di risorse usando SQL Server Management Studio  
 **Per creare un pool di risorse utilizzando[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire Esplora oggetti ed espandere in modo ricorsivo il nodo **Gestione** fino a **Resource Governor**incluso.  
  
2.  Fare clic con il pulsante destro del mouse su **Resource Governor**, quindi su **Proprietà**.  
  
3.  Nella griglia **Pool di risorse** fare clic sulla prima colonna nella riga vuota. Questa colonna è etichettata con un asterisco (*).  
  
4.  Fare doppio clic sulla cella vuota nella colonna **Nome** . Digitare il nome che si desidera utilizzare per il pool di risorse.  
  
5.  Selezionare o fare doppio clic su qualsiasi altra cella della riga che si desidera modificare e immettere i nuovi valori.  
  
6.  Per salvare le modifiche, fare clic su **OK**.  
  
##  <a name="CreRPTSQL"></a>Creare un pool di risorse usando Transact-SQL  
 **Per creare un pool di risorse utilizzando[!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  Eseguire l'istruzione `CREATE RESOURCE POOL` specificando i valori di proprietà da impostare.  
  
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
 [Resource Governor](resource-governor.md)   
 [Abilita Resource Governor](enable-resource-governor.md)   
 [Pool di risorse Resource Governor](resource-governor-resource-pool.md)   
 [Modificare le impostazioni del pool di risorse](change-resource-pool-settings.md)   
 [Eliminare un pool di risorse](delete-a-resource-pool.md)   
 [Configurare Resource Governor usando un modello](configure-resource-governor-using-a-template.md)   
 [Gruppo del carico di lavoro Resource Governor](resource-governor-workload-group.md)   
 [Funzione di classificazione Resource Governor](resource-governor-classifier-function.md)   
 [CREARE un POOL di risorse &#40;&#41;Transact-SQL](/sql/t-sql/statements/create-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
