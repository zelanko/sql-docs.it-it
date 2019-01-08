---
title: Visualizzare proprietà di Resource Governor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql12.swb.rg.properties.f1
helpviewer_keywords:
- Resource Governor, properties
ms.assetid: de3510df-f792-4a9d-80fa-f198fd36cdc8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c1093297892ea2e03cb9583a1e5c40a1c2a85b19
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52781264"
---
# <a name="view-resource-governor-properties"></a>View Resource Governor Properties
  È possibile creare o configurare entità Resource Governor, ad esempio pool di risorse e gruppi di carico di lavoro, tramite la pagina Proprietà di Resource Governor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
1.  **Prima di iniziare:**  [Autorizzazioni](#Permissions)  
  
2.  **Per visualizzare le proprietà di Resource Governor, utilizzando:**  [Pagina delle proprietà di Resource Governor](#ViewRGProp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
 Oltre a visualizzare le proprietà di entità Resource Governor, è possibile eseguire diverse attività di configurazione tramite la pagina **Proprietà di Resource Governor** . Per altre informazioni, vedere gli argomenti seguenti:  
  
-   [Abilitare Resource Governor](enable-resource-governor.md)  
  
-   [Disabilitare Resource Governor](disable-resource-governor.md)  
  
-   [Creare un pool di risorse](create-a-resource-pool.md)  
  
-   [Creare un gruppo di carico di lavoro](create-a-workload-group.md)  
  
-   [Modificare le impostazioni del pool di risorse](change-resource-pool-settings.md)  
  
-   [Modificare le impostazioni dei gruppi di carico di lavoro](change-workload-group-settings.md)  
  
-   [Spostare un gruppo di carico di lavoro](move-a-workload-group.md)  
  
 Dopo aver aggiunto, eliminato o spostato un gruppo di carico di lavoro o un pool di risorse e quindi aver scelto **OK** , verrà eseguita l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
 Se l'operazione di creazione o riconfigurazione del pool di risorse o gruppo di carico di lavoro non viene completata, viene visualizzato un messaggio di riepilogo degli errori sotto il titolo della pagina delle proprietà. Per visualizzare un messaggio di errore dettagliato, fare clic sulla freccia GIÙ sul messaggio di errore.  
  
 È possibile determinare se è presente una configurazione in sospeso eseguendo una query sulla vista a gestione dinamica [sys.dm_resource_governor_configuration](/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql) per ottenere lo stato corrente di is_configuration_pending.  
  
###  <a name="Permissions"></a> Permissions  
 Per visualizzare le proprietà di Resource Governor è necessaria l'autorizzazione VIEW SERVER STATER. Per le attività di configurazione di Resource Governor è necessaria l'autorizzazione CONTROL SERVER.  
  
##  <a name="ViewRGProp"></a> Visualizzare la pagina delle proprietà di Resource Governor  
 **Per visualizzare le proprietà di Resource Governor tramite la pagina Proprietà di Resource Governor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire Esplora oggetti ed espandere in modo ricorsivo il nodo **Gestione** fino a **Resource Governor**.  
  
2.  Fare clic con il pulsante destro del mouse su **Resource Governor** , quindi fare clic su **Proprietà**. In questo modo viene aperta la pagina **Proprietà di Resource Governor** .  
  
3.  Per le descrizioni dei campi nella pagina, vedere [Proprietà di Resource Governor](#RGProp).  
  
4.  Per salvare eventuali modifiche, fare clic su **OK**.  
  
##  <a name="RGProp"></a> Proprietà di Resource Governor  
 **Nome della funzione di classificazione**  
 Consente di specificare la funzione di classificazione selezionandola nell'elenco.  
  
 **Abilitare Resource Governor**  
 Consente di abilitare o disabilitare Resource Governor selezionando o deselezionando la casella di controllo.  
  
 **Pool di risorse**  
 Consente di creare o modificare la configurazione del pool di risorse utilizzando la griglia fornita. Questa griglia viene popolata con le informazioni sui pool interni e sui pool predefiniti. Selezionare un pool da utilizzare facendo clic sulla prima colonna nella riga del pool. Per creare un nuovo pool di risorse, fare clic sulla riga preceduta dall'asterisco (**\***).  
  
 **Name**  
 Consente di specificare il nome del pool di risorse.  
  
 **% CPU minima**  
 Consente di specificare la larghezza di banda media garantita della CPU concessa per tutte le richieste nel pool di risorse, in caso di conflitto di CPU. L'intervallo è compreso tra 0 e 100.  
  
 **% massima CPU**  
 Consente di specificare la larghezza di banda media massima della CPU concessa per tutte le richieste nel pool di risorse in caso di conflitto di CPU. L'intervallo è compreso tra 0 e 100. L'impostazione predefinita è 100.  
  
 **% memoria minima**  
 Consente di specificare la quantità minima di memoria riservata al pool di risorse non condivisibile con altri pool di risorse. L'intervallo è compreso tra 0 e 100.  
  
 **% memoria massima**  
 Consente di specificare la memoria totale del server utilizzabile dalle richieste in questo pool di risorse. L'intervallo è compreso tra 0 e 100. L'impostazione predefinita è 100.  
  
 Per altre informazioni, vedere [crea POOL di risorse &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql).  
  
 **Gruppi del carico di lavoro per pool di risorse**  
 Consente di creare o modificare la configurazione del gruppo del carico di lavoro utilizzando la griglia fornita. Questa griglia viene popolata con le informazioni sui gruppi interni e sui gruppi predefiniti. Selezionare un gruppo da utilizzare facendo clic sulla prima colonna nella riga del pool. Per creare un nuovo gruppo del carico di lavoro, fare clic sulla riga preceduta dall'asterisco (**\***).  
  
 **Name**  
 Consente di specificare il nome del gruppo del carico di lavoro.  
  
 **Priorità**  
 Consente di specificare l'importanza relativa di una richiesta nel gruppo del carico di lavoro. Le impostazioni disponibili sono Minima, Media e Massima.  
  
 **Numero massimo di richieste**  
 Consente di specificare il numero massimo di richieste simultanee eseguibili nel gruppo del carico di lavoro. Deve essere 0 o un valore intero positivo.  
  
 **Tempo CPU (sec)**  
 Consente di specificare la quantità massimo di tempo della CPU utilizzabile da una richiesta. Deve essere 0 o un valore intero positivo. Se è 0, il tempo è illimitato.  
  
 **% concessione memoria**  
 Consente di specificare la quantità massima di memoria utilizzabile dal pool da una richiesta singola. L'intervallo è compreso tra 0 e 100.  
  
 **Timeout concessione (sec)**  
 Consente di specificare il tempo massimo di attesa di una query per la disponibilità di una risorsa, prima che la query generi un errore. Deve essere 0 o un valore intero positivo.  
  
 **Grado di parallelismo**  
 Consente di specificare il grado massimo di parallelismo (DOP) per le richieste parallele. L'intervallo è da 0 a 64.  
  
 Per altre informazioni, vedere [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-workload-group-transact-sql).  
  
## <a name="view-resource-governor-properties-by-using-transact-sql"></a>Visualizzare le proprietà di Resource Governor utilizzando Transact-SQL  
 **Visualizzare le proprietà di Resource Governor utilizzando Transact-SQL**  
  
1.  Per visualizzare le definizioni delle entità resource governor, usare le [Viste del catalogo di Resource Governor &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql).  
  
2.  Per visualizzare le configurazioni correnti delle entità resource governor, usare le [Viste a gestione dinamica relative a Resource Governor &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [Resource Governor](resource-governor.md)   
 [Abilitare Resource Governor](enable-resource-governor.md)   
 [Pool di risorse di Resource Governor](resource-governor-resource-pool.md)   
 [Gruppo di carico di lavoro di Resource Governor](resource-governor-workload-group.md)   
 [Funzione di classificazione di Resource Governor](resource-governor-classifier-function.md)  
  
  
