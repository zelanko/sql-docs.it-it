---
title: Configurare Resource Governor usando un modello | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, templates
ms.assetid: f342dec2-d1d6-483e-b44e-98eb7d168b5e
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: bb17a0d2b42528d886430e92b82908a3e08b5694
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720525"
---
# <a name="configure-resource-governor-using-a-template"></a>Configurare Resource Governor utilizzando un modello
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  È possibile configurare Resource Governor utilizzando un modello fornito in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   **Prima di iniziare:**  [Autorizzazioni](#Permissions)  
  
-   **Per creare un gruppo di carico di lavoro usando:** [un modello](#ConfRGTemplate)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
 Utilizzare i seguenti passaggi per aprire e modificare un modello che consente di creare un pool di risorse e un gruppo di carico di lavoro per il pool. Inoltre, questo modello consente di creare una funzione di classificazione definita dall'utente mediante la quale vengono indirizzate le nuove connessioni al gruppo predefinito o al gruppo di carico di lavoro creato.  
  
###  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] di Resource Governor nel modello è necessaria l'autorizzazione CONTROL SERVER.  
  
##  <a name="configure-resource-governor-using-a-template"></a><a name="ConfRGTemplate"></a> Configurare Resource Governor utilizzando un modello  
 **Per configurare Resource Governor utilizzando un modello di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]scegliere **Esplora modelli** dal menu **Visualizza**.  
  
2.  In **Esplora modelli**espandere **Resource Governor**, quindi fare doppio clic su **Configura Resource Governor**.  
  
3.  In **Connetti al Motore di database**immettere le informazioni necessarie e quindi fare clic su **OK**. Il modello Configure Resource Governor.sql è disponibile nell'editor di query. Utilizzare questo modello per creare e configurare un pool di risorse, un gruppo del carico di lavoro e una funzione di classificazione.  
  
4.  Per modificare i valori del modello, premere CTRL+SHIFT+M. Nella finestra di dialogo **Imposta valori per parametri modello** immettere i valori che si desidera utilizzare.  
  
5.  Per salvare le modifiche apportate al modello, fare clic su **OK**.  
  
6.  Per eseguire la query, fare clic su **Esegui**.  

## <a name="see-also"></a>Vedere anche  
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [Abilitare Resource Governor](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Pool di risorse di Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Gruppo di carico di lavoro di Resource Governor](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Funzione di classificazione di Resource Governor](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [Visualizzare proprietà di Resource Governor](../../relational-databases/resource-governor/view-resource-governor-properties.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
