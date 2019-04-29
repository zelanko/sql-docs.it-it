---
title: Concedere le autorizzazioni su una dimensione (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 834cfe3629aed196c27391c48829b6b66884b82d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62989375"
---
# <a name="grant-permissions-on-a-dimension-analysis-services"></a>Concedere le autorizzazioni per una dimensione (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La sicurezza delle dimensioni viene usata per impostare le autorizzazioni su un oggetto dimensione e non sui relativi dati. In genere, consentire o negare l'accesso alle operazioni di elaborazione rappresenta l'obiettivo principale quando si impostano le autorizzazioni su una dimensione.  
  
 Probabilmente però l'obiettivo non è controllare le operazioni di elaborazione, bensì l'accesso dei dati a una dimensione o gli attributi e le gerarchie in essa contenuti. Si supponga, ad esempio, che una società con divisioni di vendita regionali non desideri autorizzare l'accesso alle informazioni sulle prestazioni di vendita agli utenti esterni alla divisione. Per consentire o negare l'accesso a parti di dati della dimensione per diversi elementi costituenti, è possibile impostare le autorizzazioni sugli attributi della dimensione e sui membri della dimensione. Si noti che non è possibile negare l'accesso a un singolo oggetto dimensione, ma solo ai relativi dati. Se l'obiettivo immediato è consentire o negare l'accesso ai membri di una dimensione, compresi i diritti di accesso alle singole gerarchie di attributi, vedere [Concedere l'accesso personalizzato ai dati della dimensione &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) per altre informazioni.  
  
 La parte restante di questo argomento descrive le autorizzazioni che è possibile impostare sull'oggetto dimensione, tra cui:  
  
-   Autorizzazioni di Lettura o Lettura/Scrittura: è possibile solo scegliere tra Lettura e Lettura/Scrittura. Non è possibile specificare "nessuno". Come indicato, se l'obiettivo consiste nel limitare l'accesso ai dati della dimensione, vedere [Concedere l'accesso personalizzato ai dati della dimensione &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) per informazioni dettagliate.  
  
-   Autorizzazioni di elaborazione: impostare tale opzione quando gli scenari richiedono una strategia di elaborazione che prevede autorizzazioni personalizzate per singoli oggetti.  
  
-   Autorizzazioni Lettura definizione: in genere è consigliabile impostare tale opzione per supportare l'elaborazione interattiva in uno strumento o per fornire visibilità in un modello. Lettura definizione consente di visualizzare la struttura di una dimensione senza l'autorizzazione per i relativi dati o la possibilità di modificarne la definizione.  
  
 Quando si definiscono i ruoli per una dimensione, le autorizzazioni disponibili variano a seconda che l'oggetto sia una dimensione del database autonoma, interna al database ma esterna a un cubo, o una dimensione del cubo.  
  
> [!NOTE]  
>  Per impostazione predefinita, le autorizzazioni per una dimensione del database vengono ereditate da una dimensione del cubo. Se, ad esempio, si abilita l'autorizzazione **Lettura/Scrittura** su una dimensione del database Customer, la dimensione del cubo Customer eredita l'autorizzazione **Lettura/Scrittura** nel contesto del ruolo corrente. È possibile deselezionare le autorizzazioni ereditate se si vuole eseguire l'override di un'impostazione di autorizzazione.  
  
## <a name="set-permissions-on-a-database-dimension"></a>Impostare le autorizzazioni su una dimensione del database  
 Le dimensioni del database sono oggetti autonomi all'interno di un database, consentendo il riuso della dimensione all'interno dello stesso modello. Considerare la dimensione DATE del database usata più volte in un modello come dimensioni Order Date, Ship Date e Due Date del cubo. Poiché le dimensioni del cubo e del database sono oggetti peer in un database, è possibile impostare le autorizzazioni di elaborazione indipendentemente per ogni oggetto.  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], espandere il nodo **Ruoli** relativo al database appropriato in Esplora oggetti, quindi fare clic su un ruolo del database o creare un nuovo ruolo del database.  
  
2.  Nel riquadro **Dimensioni** il set di dimensioni deve essere impostato su **Tutte le dimensioni del database**.  
  
     Per impostazione predefinita, le autorizzazioni sono impostate su **Lettura**.  
  
     Sebbene sia disponibile l'autorizzazione **Lettura/Scrittura** , è consigliabile non usarla. L'autorizzazione**Lettura/Scrittura** viene usata per gli scenari di writeback delle dimensioni, che sono stati deprecati. Vedere [Funzionalità di Analysis Services deprecate in SQL Server 2016](../../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md).  
  
     Facoltativamente, è possibile impostare le autorizzazioni **Lettura definizione** ed **Elaborazione** per i singoli oggetti dimensione, a condizione che tali autorizzazioni non siano già impostate a livello di database. Vedere [Concedere le autorizzazioni di elaborazione &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) e [Concedere le autorizzazioni di lettura definizione per i metadati degli oggetti &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-read-definition-permissions-on-object-metadata-analysis-services.md) per informazioni dettagliate.  
  
## <a name="set-permissions-on-a-cube-dimension"></a>Impostare le autorizzazioni su una dimensione del cubo  
 Le dimensioni del cubo sono dimensioni del database che sono state aggiunte a un cubo. Di conseguenza, sono strutturalmente dipendenti dai gruppi di misure associati. Sebbene sia possibile elaborare questi oggetti in modo atomico, in relazione all'autorizzazione è consigliabile gestire il cubo e le dimensioni del cubo come una sola entità.  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], espandere il nodo **Ruoli** relativo al database appropriato in Esplora oggetti, quindi fare clic su un ruolo del database o creare un nuovo ruolo del database.  
  
2.  Nel **quote** riquadro modificare la dimensione del set \<nome-cubo > **dimensioni cubo**.  
  
     Per impostazione predefinita, le autorizzazioni vengono ereditate da una dimensione del database corrispondente. Deselezionare la casella di controllo **Eredita** per modificare le autorizzazioni da **Lettura** a **Lettura/Scrittura**. Prima di usare l'autorizzazione **Lettura/Scrittura**, leggere la nota nella sezione precedente.  
  
> [!IMPORTANT]  
>  Se per configurare le autorizzazioni del ruolo del database si usa la libreria AMO (Analysis Management Objects), qualsiasi riferimento a una dimensione del cubo nell'attributo DimensionPermission di un cubo impedisce l'ereditarietà delle autorizzazioni dall'attributo DimensionPermission del database. Per altre informazioni su AMO, vedere [Sviluppo con AMO &#40;Analysis Management Objects&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo).  
  
## <a name="see-also"></a>Vedere anche  
 [Ruoli e autorizzazioni &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)   
 [Concedere le autorizzazioni per un cubo o un modello &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [Concedere le autorizzazioni per le strutture e i modelli di data mining &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [Concedere l'accesso personalizzato ai dati della dimensione &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)   
 [Concedere l'accesso personalizzato ai dati delle celle &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
  
