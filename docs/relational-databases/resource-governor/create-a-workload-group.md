---
title: Creare un gruppo di carico di lavoro | Microsoft Docs
description: Informazioni su come creare un gruppo di carico di lavoro usando SQL Server Management Studio o Transact-SQL. È necessaria l'autorizzazione CONTROL SERVER.
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, workload group create
- workload groups [SQL Server], create
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: eb23f8926cff87651ba0feda1b398112dec930af
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2020
ms.locfileid: "86456839"
---
# <a name="create-a-workload-group"></a>Creare un gruppo di carico di lavoro

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  È possibile creare un gruppo di carico di lavoro utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#LimitationsRestrictions), [Autorizzazioni](#Permissions)  
  
-   **Per creare un gruppo di carico di lavoro usando:**  [SQL Server Management Studio](#CreRPProp), [Transact-SQL](#CreRPTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitazioni e restrizioni

 **REQUEST_MAX_MEMORY_GRANT_PERCENT**  
  
 La quantità di memoria utilizzata per la creazione dell'indice in una tabella partizionata non allineata è proporzionale al numero di partizioni interessate. Se la memoria totale necessaria supera il limite per query (REQUEST_MAX_MEMORY_GRANT_PERCENT) imposto dall'impostazione del gruppo di carico di lavoro, la creazione dell'indice potrebbe non essere completata. Poiché il gruppo di carico di lavoro predefinito consente a una query di superare il limite per query con la memoria minima necessaria per la compatibilità con SQL Server 2005, l'utente potrebbe essere in grado di eseguire la stessa creazione dell'indice nel gruppo di carico di lavoro predefinito, se nel pool di risorse predefinito è configurata una quantità di memoria totale sufficiente per eseguire una query.  
  
 Per la creazione dell'indice è possibile utilizzare un'area di lavoro per la memoria maggiore rispetto a quanto inizialmente garantito per le prestazioni. Questa speciale gestione è supportata da Resource Governor, tuttavia, la concessione iniziale ed eventuali concessioni di memoria aggiuntiva sono limitate dalle impostazioni di gruppo del carico di lavoro e dal pool di risorse.  
  
###  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni

 Per creare un gruppo di carico di lavoro è necessaria l'autorizzazione CONTROL SERVER.  
  
##  <a name="create-a-workload-group-using-sql-server-management-studio"></a><a name="CreRPProp"></a> Creare un gruppo di carico di lavoro utilizzando SQL Server Management Studio

 **Per creare un gruppo di carico di lavoro utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  In Esplora oggetti espandere in modo ricorsivo il nodo **Gestione** fino al pool di risorse incluso in cui è contenuto il gruppo di carico di lavoro da modificare.  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella **Gruppi del carico di lavoro** , quindi scegliere **Nuovo gruppo del carico di lavoro**.  
  
3.  Nella griglia **Pool di risorse** assicurarsi che il pool di risorse in cui si desidera aggiungere il gruppo di carico di lavoro sia evidenziato.  
  
4.  La griglia **Gruppi del carico di lavoro per il pool di risorse** presenterà una nuova riga con un nome vuoto e i valori predefiniti nelle altre colonne.  
  
5.  Fare clic sulla cella **Nome** e immettere un nome per il gruppo di carico di lavoro.  
  
6.  Selezionare o fare doppio clic su qualsiasi altra cella della riga di cui si desidera modificare le impostazioni predefinite e immettere i nuovi valori.  
  
7.  Per salvare le modifiche, fare clic su **OK**.  

##  <a name="create-a-workload-group-using-transact-sql"></a><a name="CreRPTSQL"></a> Creare un gruppo di carico di lavoro utilizzando Transact-SQL  
 **Per creare un gruppo di carico di lavoro utilizzando [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  Eseguire l'istruzione CREATE WORKLOAD GROUP specificando i valori delle proprietà da impostare.  
  
2.  Eseguire l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
### <a name="example-transact-sql"></a>Esempio (Transact-SQL)

 Nell'esempio seguente viene creato un gruppo di carico di lavoro denominato `groupAdhoc` nel pool di risorse denominato `poolAdhoc`.  
  
```sql
CREATE WORKLOAD GROUP groupAdhoc  
USING poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche

 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [Abilitare Resource Governor](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Creare un pool di risorse](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [Modificare le impostazioni dei gruppi di carico di lavoro](../../relational-databases/resource-governor/change-workload-group-settings.md)   
 [Creare e testare una funzione di classificazione definita dall'utente](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)  
  
  
