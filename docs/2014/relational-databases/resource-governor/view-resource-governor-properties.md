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
ms.openlocfilehash: 35d4720a8fe8b8c1b404a97e27b36896f36dd5f7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63209690"
---
# <a name="view-resource-governor-properties"></a>View Resource Governor Properties
  È possibile creare o configurare entità Resource Governor, ad esempio pool di risorse e gruppi di carico di lavoro, tramite la pagina Proprietà di Resource Governor in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
1.  **Prima di iniziare:**  [Autorizzazioni](#Permissions)  
  
2.  **Per visualizzare le proprietà di Resource Governor usando:**  [Pagina Proprietà di Resource Governor](#ViewRGProp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
 Oltre a visualizzare le proprietà di entità Resource Governor, è possibile eseguire diverse attività di configurazione tramite la pagina **Proprietà di Resource Governor** . Per altre informazioni, vedere gli argomenti seguenti:  
  
-   [Abilitare Resource Governor](enable-resource-governor.md)  
  
-   [Disabilitare Resource Governor](disable-resource-governor.md)  
  
-   [Creare un pool di risorse](create-a-resource-pool.md)  
  
-   [Creazione di un gruppo di carico di lavoro](create-a-workload-group.md)  
  
-   [Modificare le impostazioni del pool di risorse](change-resource-pool-settings.md)  
  
-   [Modificare le impostazioni dei gruppi di carico di lavoro](change-workload-group-settings.md)  
  
-   [Spostare un gruppo di carico di lavoro](move-a-workload-group.md)  
  
 Dopo aver aggiunto, eliminato o spostato un gruppo di carico di lavoro o un pool di risorse e quindi aver scelto **OK** , verrà eseguita l'istruzione ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
 Se l'operazione di creazione o riconfigurazione del pool di risorse o gruppo di carico di lavoro non viene completata, viene visualizzato un messaggio di riepilogo degli errori sotto il titolo della pagina delle proprietà. Per visualizzare un messaggio di errore dettagliato, fare clic sulla freccia GIÙ sul messaggio di errore.  
  
 È possibile determinare se è presente una configurazione in sospeso eseguendo una query sulla vista a gestione dinamica [sys.dm_resource_governor_configuration](/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql) per ottenere lo stato corrente di is_configuration_pending.  
  
###  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per visualizzare le proprietà di Resource Governor è necessaria l'autorizzazione VIEW SERVER STATER. Per le attività di configurazione di Resource Governor è necessaria l'autorizzazione CONTROL SERVER.  
  
##  <a name="view-the-resource-governor-properties-page"></a><a name="ViewRGProp"></a>Visualizzare la pagina delle proprietà Resource Governor  
 **Per visualizzare le proprietà di Resource Governor tramite la pagina proprietà Resource Governor in[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]aprire Esplora oggetti ed espandere in modo ricorsivo il nodo **Gestione** fino a **Resource Governor**.  
  
2.  Fare clic con il pulsante destro del mouse su **Resource Governor** , quindi fare clic su **Proprietà**. In questo modo viene aperta la pagina **Proprietà di Resource Governor** .  
  
3.  Per le descrizioni dei campi nella pagina, vedere [Proprietà di Resource Governor](#RGProp).  
  
4.  Per salvare eventuali modifiche, fare clic su **OK**.  
  
##  <a name="resource-governor-properties"></a><a name="RGProp"></a>Proprietà Resource Governor  
 **Nome della funzione di classificazione**  
 Consente di specificare la funzione di classificazione selezionandola nell'elenco.  
  
 **Abilitare Resource Governor**  
 Consente di abilitare o disabilitare Resource Governor selezionando o deselezionando la casella di controllo.  
  
 **Pool di risorse**  
 Consente di creare o modificare la configurazione del pool di risorse utilizzando la griglia fornita. Questa griglia viene popolata con le informazioni sui pool interni e sui pool predefiniti. Selezionare un pool da utilizzare facendo clic sulla prima colonna nella riga del pool. Per creare un nuovo pool di risorse, fare clic sulla riga preceduta dall'asterisco (**&#42;**).  
  
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
  
 Per altre informazioni, vedere [creare un pool di risorse &#40;&#41;Transact-SQL ](/sql/t-sql/statements/create-resource-pool-transact-sql).  
  
 **Gruppi del carico di lavoro per pool di risorse**  
 Consente di creare o modificare la configurazione del gruppo del carico di lavoro utilizzando la griglia fornita. Questa griglia viene popolata con le informazioni sui gruppi interni e sui gruppi predefiniti. Selezionare un gruppo da utilizzare facendo clic sulla prima colonna nella riga del pool. Per creare un nuovo gruppo del carico di lavoro, fare clic sulla riga preceduta dall'asterisco (**&#42;**).  
  
 **Nome**  
 Consente di specificare il nome del gruppo del carico di lavoro.  
  
 **Importanza**  
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
  
## <a name="see-also"></a>Vedi anche  
 [Resource Governor](resource-governor.md)   
 [Abilita Resource Governor](enable-resource-governor.md)   
 [Pool di risorse Resource Governor](resource-governor-resource-pool.md)   
 [Gruppo del carico di lavoro Resource Governor](resource-governor-workload-group.md)   
 [Funzione di classificazione di Resource Governor](resource-governor-classifier-function.md)  
  
  
