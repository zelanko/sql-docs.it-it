---
title: Configurare Resource Governor usando un modello | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, templates
ms.assetid: f342dec2-d1d6-483e-b44e-98eb7d168b5e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3da27154a824433d214dc495bf7f236ff104274f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68198934"
---
# <a name="configure-resource-governor-using-a-template"></a>Configurare Resource Governor utilizzando un modello
  È possibile configurare Resource Governor utilizzando un modello fornito in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   **Prima di iniziare:**  [Autorizzazioni](#Permissions)  
  
-   **Per creare un gruppo di carico di lavoro usando:**  [un modello](#ConfRGTemplate)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
 Utilizzare i seguenti passaggi per aprire e modificare un modello che consente di creare un pool di risorse e un gruppo di carico di lavoro per il pool. Inoltre, questo modello consente di creare una funzione di classificazione definita dall'utente mediante la quale vengono indirizzate le nuove connessioni al gruppo predefinito o al gruppo di carico di lavoro creato.  
  
###  <a name="Permissions"></a> Autorizzazioni  
 Per istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] di Resource Governor nel modello è necessaria l'autorizzazione CONTROL SERVER.  
  
##  <a name="ConfRGTemplate"></a> Configurare Resource Governor utilizzando un modello  
 **Per configurare Resource Governor utilizzando un modello di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]scegliere **Esplora modelli** dal menu **Visualizza**.  
  
2.  In **Esplora modelli**espandere **Resource Governor**, quindi fare doppio clic su **Configura Resource Governor**.  
  
3.  In **Connetti al Motore di database**immettere le informazioni necessarie e quindi fare clic su **OK**. Il modello Configure Resource Governor.sql è disponibile nell'editor di query. Utilizzare questo modello per creare e configurare un pool di risorse, un gruppo del carico di lavoro e una funzione di classificazione.  
  
4.  Per modificare i valori del modello, premere CTRL+SHIFT+M. Nella finestra di dialogo **Imposta valori per parametri modello** immettere i valori che si desidera utilizzare.  
  
5.  Per salvare le modifiche apportate al modello, fare clic su **OK**.  
  
6.  Per eseguire la query, fare clic su **Esegui**.  
  
## <a name="see-also"></a>Vedere anche  
 [Resource Governor](resource-governor.md)   
 [Abilitare Resource Governor](enable-resource-governor.md)   
 [Pool di risorse di Resource Governor](resource-governor-resource-pool.md)   
 [Gruppo di carico di lavoro di Resource Governor](resource-governor-workload-group.md)   
 [Funzione di classificazione di Resource Governor](resource-governor-classifier-function.md)   
 [Visualizzare proprietà di Resource Governor](view-resource-governor-properties.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-workload-group-transact-sql)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
