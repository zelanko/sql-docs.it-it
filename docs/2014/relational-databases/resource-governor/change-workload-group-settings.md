---
title: Modificare le impostazioni dei gruppi di carico di lavoro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- workload groups [SQL Server], alter
- Resource Governor, workload group alter
ms.assetid: 73b6109c-2ad0-4915-b11b-d40d5a0fdc25
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 579aad71d32a629d75f1eecd76e7dacfe32d94f2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066523"
---
# <a name="change-workload-group-settings"></a>Modificare le impostazioni dei gruppi di carico di lavoro
  È possibile modificare le impostazioni di un gruppo di carico di lavoro utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#LimitationsRestrictions), [Autorizzazioni](#Permissions)  
  
-   **Per modificare le impostazioni per un gruppo di carico di lavoro, usando:**  [SQL Server Management Studio](#ChgWGProp), [Transact-SQL](#ChgWGTSQL)  
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 È possibile modificare le impostazioni del gruppo di carico di lavoro predefinito e dei gruppi di carico di lavoro definiti dall'utente.  
  
 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 La quantità di memoria utilizzata per la creazione dell'indice in una tabella partizionata non allineata è proporzionale al numero di partizioni interessate. Se la memoria totale necessaria supera il limite per query (REQUEST_MAX_MEMORY_GRANT_PERCENT) imposto dall'impostazione del gruppo di carico di lavoro, la creazione dell'indice potrebbe non essere completata. Poiché il gruppo di carico di lavoro predefinito consente a una query di superare il limite per query con la memoria minima necessaria per la compatibilità con SQL Server 2005, l'utente potrebbe essere in grado di eseguire la stessa creazione dell'indice nel gruppo di carico di lavoro predefinito, se nel pool di risorse predefinito è configurata una quantità di memoria totale sufficiente per eseguire una query.  
  
 Per la creazione dell'indice è possibile utilizzare un'area di lavoro per la memoria maggiore rispetto a quanto inizialmente garantito per le prestazioni. Questa speciale gestione è supportata da Resource Governor, tuttavia, la concessione iniziale ed eventuali concessioni di memoria aggiuntiva sono limitate dalle impostazioni di gruppo del carico di lavoro e dal pool di risorse.  
  
###  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per modificare le impostazioni di un gruppo di carico di lavoro è necessaria l'autorizzazione CONTROL SERVER.  
  
##  <a name="change-workload-group-settings-using-sql-server-management-studio"></a><a name="ChgWGProp"></a> Modificare le impostazioni di un gruppo di carico di lavoro utilizzando SQL Server Management Studio  
 **Per modificare le impostazioni di un gruppo di carico di lavoro utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  In Esplora oggetti espandere in modo ricorsivo il nodo **Gestione** fino alla cartella **Gruppi del carico di lavoro** inclusa in cui è contenuto il gruppo di carico di lavoro da modificare.  
  
2.  Fare clic con il pulsante destro del mouse sul gruppo di carico di lavoro da modificare e quindi scegliere **Proprietà**.  
  
3.  Nella pagina **Proprietà di Resource Governor** selezionare la riga per il gruppo di carico di lavoro nella griglia **Gruppi del carico di lavoro per il pool di risorse** se non è selezionata automaticamente.  
  
4.  Selezionare o fare doppio clic sulle celle della riga da modificare e immettere i nuovi valori.  
  
5.  Per salvare le modifiche, fare clic su **OK**.  
  
##  <a name="change-workload-group-settings-using-transact-sql"></a><a name="ChgWGTSQL"></a> Modificare le impostazioni di un gruppo di carico di lavoro utilizzando Transact-SQL  
 **Per modificare le impostazioni di un gruppo di carico di lavoro utilizzando Transact-SQL**  
  
1.  Eseguire l'istruzione ALTER WORKLOAD GROUPP specificando i valori delle proprietà da modificare.  
  
2.  Eseguire l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
### <a name="example-transact-sql"></a>Esempio (Transact-SQL)  
 Nell'esempio seguente viene modificata l'impostazione di percentuale di concessione di memoria massima per il gruppo di carico di lavoro denominato `groupAdhoc`.  
  
```  
ALTER WORKLOAD GROUP groupAdhoc  
WITH (REQUEST_MAX_MEMORY_GRANT_PERCENT = 30);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Resource Governor](resource-governor.md)   
 [Creare un gruppo di carico di lavoro](create-a-workload-group.md)   
 [Creare un pool di risorse](create-a-resource-pool.md)   
 [Modificare le impostazioni del pool di risorse](change-resource-pool-settings.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-workload-group-transact-sql)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
