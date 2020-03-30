---
title: Spostare un gruppo di carico di lavoro | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.rg.properties_moveworkloadgroup.f1
helpviewer_keywords:
- workload groups [SQL Server], move
- Resource Governor, workload group move
ms.assetid: f2068636-6e53-486a-a6fc-c12de2a38424
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 7f4d77bba168f84b42aab0884369cf834af3779d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68099234"
---
# <a name="move-a-workload-group"></a>Spostare un gruppo di carico di lavoro
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  È possibile spostare un gruppo di carico di lavoro di Resource Governor in un pool di risorse diverso tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o Transact-SQL.  
  
-   **Prima di iniziare:**  [Limitazioni e restrizioni](#LimitationsRestrictions), [Autorizzazioni](#Permissions)  
  
-   **Per spostare un gruppo di carico di lavoro usando:**  [SQL Server Management Studio](#MoveWGSSMS), [Transact-SQL](#MoveWGTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
 Non è possibile spostare un gruppo di carico di lavoro se un'operazione di configurazione di Resource Governor è in sospeso.  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitazioni e restrizioni  
 Non è possibile spostare un gruppo di carico di lavoro se un'operazione di configurazione di Resource Governor è in sospeso. È possibile determinare se è presente una configurazione in sospeso eseguendo una query alla vista a gestione dinamica [sys.dm_resource_governor_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md) per ottenere lo stato corrente di is_configuration_pending.  
  
###  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per spostare un gruppo di carico di lavoro è necessaria l'autorizzazione CONTROL SERVER.  
  
##  <a name="move-a-workload-group-using-sql-server-management-studio"></a><a name="MoveWGSSMS"></a> Spostare un gruppo di carico di lavoro utilizzando SQL Server Management Studio  
 **Per spostare un gruppo di carico di lavoro utilizzando [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]**  
  
1.  In Esplora oggetti espandere in modo ricorsivo il nodo **Gestione** fino a **Resource Governor**.  
  
2.  Fare clic con il pulsante destro del mouse su **Resource Governor** , quindi fare clic su **Proprietà**. In questo modo viene aperta la pagina **Proprietà di Resource Governor** .  
  
3.  Nella finestra **Pool di risorse** fare clic sul pool di risorse contenente il gruppo di carico di lavoro da spostare. Nella finestra **Gruppi del carico di lavoro** sono ora elencati i gruppi di carico di lavoro di tale pool di risorse.  
  
4.  Nella finestra **Gruppi del carico di lavoro** fare clic con il pulsante destro del mouse sulla freccia a destra, a sinistra del gruppo di carico di lavoro da spostare e fare clic su **Sposta in**. In questo modo viene visualizza una finestra **Sposta gruppo del carico di lavoro** .  
  
5.  I pool di risorse disponibili sono visualizzati nella finestra. Fare clic sul nome del pool di risorse in cui si desidera spostare il gruppo di carico di lavoro, quindi fare clic su **OK** per eseguire l'operazione.  
  
6.  Questa operazione non viene completata fino a quando non si fa clic su **OK**. Quando si fa clic su **OK**viene eseguita l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
7.  Se l'operazione di creazione o riconfigurazione del pool di risorse o gruppo di carico di lavoro non viene completata, viene visualizzato un messaggio di riepilogo degli errori sotto il titolo della pagina delle proprietà. Per visualizzare un messaggio di errore dettagliato, fare clic sulla freccia GIÙ sul messaggio di errore.  
  
##  <a name="move-a-workload-group-using-transact-sql"></a><a name="MoveWGTSQL"></a> Spostare un gruppo di carico di lavoro utilizzando Transact-SQL  
 **Per spostare un gruppo di carico di lavoro utilizzando Transact-SQL**  
  
1.  Eseguire l'istruzione **ALTER WORKLOAD GROUP** specificando il nome del gruppo di carico di lavoro da spostare e il pool di risorse in cui deve essere spostato.  
  
2.  Eseguire l'istruzione **ALTER RESOURCE GOVERNOR RECONFIGURE** .  
  
### <a name="example-transact-sql"></a>Esempio (Transact-SQL)  
 Nell'esempio seguente viene spostato un gruppo di carico di lavoro denominato `groupAdhoc` nel pool di risorse predefinito.  
  
```  
ALTER WORKLOAD GROUP groupAdhoc  
USING [default];  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [Abilitare Resource Governor](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Creare un pool di risorse](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [Creare un gruppo di carico di lavoro](../../relational-databases/resource-governor/create-a-workload-group.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
