---
title: Creare un gruppo di carico di lavoro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, workload group create
- workload groups [SQL Server], create
ms.assetid: 072868ec-ceff-4db6-941b-281af731a067
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1cd3b72418d0791d70d28d2dca0a434190a2d4a9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68198925"
---
# <a name="create-a-workload-group"></a>Creare un gruppo di carico di lavoro
  È possibile creare un gruppo di carico di lavoro utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#LimitationsRestrictions), [Autorizzazioni](#Permissions)  
  
-   **Per creare un gruppo di carico di lavoro usando:**  [SQL Server Management Studio](#CreWGProp), [Transact-SQL](#CreWGTSQL)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 La quantità di memoria utilizzata per la creazione dell'indice in una tabella partizionata non allineata è proporzionale al numero di partizioni interessate. Se la memoria totale necessaria supera il limite per query (REQUEST_MAX_MEMORY_GRANT_PERCENT) imposto dall'impostazione del gruppo di carico di lavoro, la creazione dell'indice potrebbe non essere completata. Poiché il gruppo di carico di lavoro predefinito consente a una query di superare il limite per query con la memoria minima necessaria per la compatibilità con SQL Server 2005, l'utente potrebbe essere in grado di eseguire la stessa creazione dell'indice nel gruppo di carico di lavoro predefinito, se nel pool di risorse predefinito è configurata una quantità di memoria totale sufficiente per eseguire una query.  
  
 Per la creazione dell'indice è possibile utilizzare un'area di lavoro per la memoria maggiore rispetto a quanto inizialmente garantito per le prestazioni. Questa speciale gestione è supportata da Resource Governor, tuttavia, la concessione iniziale ed eventuali concessioni di memoria aggiuntiva sono limitate dalle impostazioni di gruppo del carico di lavoro e dal pool di risorse.  
  
###  <a name="Permissions"></a> Autorizzazioni  
 Per creare un gruppo di carico di lavoro è necessaria l'autorizzazione CONTROL SERVER.  
  
##  <a name="CreWGProp"></a> Creare un gruppo di carico di lavoro utilizzando SQL Server Management Studio  
 **Per creare un gruppo di carico di lavoro utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  In Esplora oggetti espandere in modo ricorsivo il nodo **Gestione** fino al pool di risorse incluso in cui è contenuto il gruppo di carico di lavoro da modificare.  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella **Gruppi del carico di lavoro** , quindi scegliere **Nuovo gruppo del carico di lavoro**.  
  
3.  Nella griglia **Pool di risorse** assicurarsi che il pool di risorse in cui si desidera aggiungere il gruppo di carico di lavoro sia evidenziato.  
  
4.  La griglia **Gruppi del carico di lavoro per il pool di risorse** presenterà una nuova riga con un nome vuoto e i valori predefiniti nelle altre colonne.  
  
5.  Fare clic sulla cella **Nome** e immettere un nome per il gruppo di carico di lavoro.  
  
6.  Selezionare o fare doppio clic su qualsiasi altra cella della riga di cui si desidera modificare le impostazioni predefinite e immettere i nuovi valori.  
  
7.  Per salvare le modifiche, fare clic su **OK**.  
  
##  <a name="CreWGTSQL"></a> Creare un gruppo di carico di lavoro utilizzando Transact-SQL  
 **Per creare un gruppo di carico di lavoro utilizzando [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  Eseguire l'istruzione CREATE WORKLOAD GROUP specificando i valori delle proprietà da impostare.  
  
2.  Eseguire l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
### <a name="example-transact-sql"></a>Esempio (Transact-SQL)  
 Nell'esempio seguente viene creato un gruppo di carico di lavoro denominato `groupAdhoc` nel pool di risorse denominato `poolAdhoc`.  
  
```  
CREATE WORKLOAD GROUP groupAdhoc  
USING poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Resource Governor](resource-governor.md)   
 [Abilitare Resource Governor](enable-resource-governor.md)   
 [Creare un pool di risorse](create-a-resource-pool.md)   
 [Modificare le impostazioni dei gruppi di carico di lavoro](change-workload-group-settings.md)   
 [Creare e testare una funzione di classificazione definita dall'utente](create-and-test-a-classifier-user-defined-function.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-workload-group-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
