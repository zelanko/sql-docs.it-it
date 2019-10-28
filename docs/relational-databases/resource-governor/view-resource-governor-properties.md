---
title: Visualizzare proprietà di Resource Governor | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.rg.properties.f1
helpviewer_keywords:
- Resource Governor, properties
ms.assetid: de3510df-f792-4a9d-80fa-f198fd36cdc8
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 2250030405a0c6bb2512e3b8446cb76e11a7080e
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72903904"
---
# <a name="view-resource-governor-properties"></a>View Resource Governor Properties
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  È possibile creare o configurare entità Resource Governor, ad esempio pool di risorse e gruppi di carico di lavoro, tramite la pagina Proprietà di Resource Governor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 ##  <a name="BeforeYouBegin"></a> Argomenti correlati 
 Oltre a visualizzare le proprietà di entità Resource Governor, è possibile eseguire diverse attività di configurazione tramite la pagina **Proprietà di Resource Governor** . Per altre informazioni, vedere gli argomenti seguenti:  
  
-   [Abilitare Resource Governor](../../relational-databases/resource-governor/enable-resource-governor.md)  
  
-   [Disabilitare Resource Governor](../../relational-databases/resource-governor/disable-resource-governor.md)  
  
-   [Creare un pool di risorse](../../relational-databases/resource-governor/create-a-resource-pool.md)  
  
-   [Creare un gruppo di carico di lavoro](../../relational-databases/resource-governor/create-a-workload-group.md)  
  
-   [Modificare le impostazioni del pool di risorse](../../relational-databases/resource-governor/change-resource-pool-settings.md)  
  
-   [Modificare le impostazioni dei gruppi di carico di lavoro](../../relational-databases/resource-governor/change-workload-group-settings.md)  
  
-   [Spostare un gruppo di carico di lavoro](../../relational-databases/resource-governor/move-a-workload-group.md)  
  
 Dopo aver aggiunto, eliminato o spostato un gruppo di carico di lavoro o un pool di risorse e quindi aver scelto **OK** , verrà eseguita l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
 Se l'operazione di creazione o riconfigurazione del pool di risorse o gruppo di carico di lavoro non viene completata, viene visualizzato un messaggio di riepilogo degli errori sotto il titolo della pagina delle proprietà. Per visualizzare un messaggio di errore dettagliato, fare clic sulla freccia GIÙ sul messaggio di errore.  
  
 È possibile determinare se è presente una configurazione in sospeso eseguendo una query sulla vista a gestione dinamica [sys.dm_resource_governor_configuration](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md) per ottenere lo stato corrente di is_configuration_pending.  
  
##  <a name="Permissions"></a> Autorizzazioni  
 Per visualizzare le proprietà di Resource Governor è necessaria l'autorizzazione VIEW SERVER STATER. Per le attività di configurazione di Resource Governor è necessaria l'autorizzazione CONTROL SERVER.  
  
##  <a name="ViewRGProp"></a> Pagina Proprietà di Resource Governor  
 **Per visualizzare le proprietà di Resource Governor tramite la pagina Proprietà di Resource Governor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire Esplora oggetti ed espandere in modo ricorsivo il nodo **Gestione** fino a **Resource Governor**.  
  
2.  Fare clic con il pulsante destro del mouse su **Resource Governor** , quindi fare clic su **Proprietà**. In questo modo viene aperta la pagina **Proprietà di Resource Governor** .  
  
3.  Per le descrizioni dei campi nella pagina, vedere [Proprietà di Resource Governor](#RGProp).  
  
4.  Per salvare eventuali modifiche, fare clic su **OK**.  

##  <a name="RGProp"></a> Resource Governor properties  
 **Nome della funzione di classificazione**  
 Consente di specificare la funzione di classificazione selezionandola nell'elenco.  
  
 **Abilitare Resource Governor**  
 Consente di abilitare o disabilitare Resource Governor selezionando o deselezionando la casella di controllo.  
  
 **Pool di risorse**  
 Consente di creare o modificare la configurazione del pool di risorse e del pool di risorse esterne usando la griglia fornita. Questa griglia viene popolata con le informazioni sui pool interni e sui pool predefiniti. Selezionare un pool da utilizzare facendo clic sulla prima colonna nella riga del pool. Per creare un nuovo pool di risorse, fare clic sulla riga preceduta dall'asterisco ( **&#42;** ).  
  
 **Nome**  
 Consente di specificare il nome del pool di risorse.  
  
 **% CPU minima**  
 Consente di specificare la larghezza di banda media garantita della CPU concessa per tutte le richieste nel pool di risorse, in caso di conflitto di CPU. L'intervallo è compreso tra 0 e 100.  
  
 **% massima CPU**  
 Consente di specificare la larghezza di banda media massima della CPU concessa per tutte le richieste nel pool di risorse in caso di conflitto di CPU. L'intervallo è compreso tra 0 e 100. L'impostazione predefinita è 100.  
  
 **% memoria minima**  
 Consente di specificare la quantità minima di memoria riservata al pool di risorse non condivisibile con altri pool di risorse. L'intervallo è compreso tra 0 e 100.  
  
 **% memoria massima**  
 Consente di specificare la memoria totale del server utilizzabile dalle richieste in questo pool di risorse. L'intervallo è compreso tra 0 e 100. L'impostazione predefinita è 100.  
  
 Per altre informazioni, vedere [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md) e [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md).  
  
 **Gruppi del carico di lavoro per pool di risorse**  
 Consente di creare o modificare la configurazione del gruppo del carico di lavoro utilizzando la griglia fornita. Questa griglia viene popolata con le informazioni sui gruppi interni e sui gruppi predefiniti. Selezionare un gruppo da utilizzare facendo clic sulla prima colonna nella riga del pool. Per creare un nuovo gruppo del carico di lavoro, fare clic sulla riga preceduta dall'asterisco ( **&#42;** ).  
  
 **Nome**  
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
  
 Per altre informazioni, vedere [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md).  
  
## <a name="view-resource-governor-properties-using-transact-sql"></a>Visualizzare le proprietà di Resource Governor mediante Transact-SQL  
 **Visualizzare le proprietà di Resource Governor utilizzando Transact-SQL**  
  
1.  Per visualizzare le definizioni delle entità resource governor, usare le [Viste del catalogo di Resource Governor &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md).  
  
2.  Per visualizzare le configurazioni correnti delle entità resource governor, usare le [Viste a gestione dinamica relative a Resource Governor &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).  
  
## <a name="more-information"></a>Ulteriori informazioni
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [Abilitare Resource Governor](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Pool di risorse di Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Gruppo di carico di lavoro di Resource Governor](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Funzione di classificazione di Resource Governor](../../relational-databases/resource-governor/resource-governor-classifier-function.md)  
  
  
