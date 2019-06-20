---
title: Concedere le autorizzazioni su una dimensione (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.dimensions.f1
helpviewer_keywords:
- dimensions [Analysis Services], security
- read/write permissions
- user access rights [Analysis Services], dimensions
- permissions [Analysis Services], dimensions
ms.assetid: be5b2746-0336-4b12-827e-131462bdf605
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3efce85f27db9d0695ea56e9940ab563ed40537a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66074963"
---
# <a name="grant-permissions-on-a-dimension-analysis-services"></a>Concedere le autorizzazioni per una dimensione (Analysis Services)
  La sicurezza delle dimensioni viene usata per impostare le autorizzazioni su un oggetto dimensione e non sui relativi dati. In genere, consentire o negare l'accesso alle operazioni di elaborazione rappresenta l'obiettivo principale quando si impostano le autorizzazioni su una dimensione.  
  
 Probabilmente però l'obiettivo non è controllare le operazioni di elaborazione, bensì l'accesso dei dati a una dimensione o gli attributi e le gerarchie in essa contenuti. Si supponga, ad esempio, che una società con divisioni di vendita regionali non desideri autorizzare l'accesso alle informazioni sulle prestazioni di vendita agli utenti esterni alla divisione. Per consentire o negare l'accesso a parti di dati della dimensione per diversi elementi costituenti, è possibile impostare le autorizzazioni sugli attributi della dimensione e sui membri della dimensione. Si noti che non è possibile negare l'accesso a un singolo oggetto dimensione, ma solo ai relativi dati. Se l'obiettivo immediato è consentire o negare l'accesso ai membri di una dimensione, compresi i diritti di accesso alle singole gerarchie di attributi, vedere [Grant custom access to dimension data &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) per altre informazioni.  
  
 La parte restante di questo argomento descrive le autorizzazioni che è possibile impostare sull'oggetto dimensione, tra cui:  
  
-   Autorizzazioni di Lettura o Lettura/Scrittura: è possibile solo scegliere tra Lettura e Lettura/Scrittura. Non è possibile specificare "nessuno". Come indicato, se l'obiettivo consiste nel limitare l'accesso ai dati della dimensione, vedere [Grant custom access to dimension data &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) per informazioni dettagliate.  
  
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
  
     Sebbene sia disponibile l'autorizzazione **Lettura/Scrittura** , è consigliabile non usarla. L'autorizzazione**Lettura/Scrittura** viene usata per gli scenari di writeback delle dimensioni, che sono stati deprecati. Visualizzare [Analysis Services deprecate in SQL Server 2014](../deprecated-analysis-services-features-in-sql-server-2014.md).  
  
     Facoltativamente, è possibile impostare le autorizzazioni **Lettura definizione** ed **Elaborazione** per i singoli oggetti dimensione, a condizione che tali autorizzazioni non siano già impostate a livello di database. Vedere [Concedere le autorizzazioni di elaborazione &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md) e [Concedere le autorizzazioni di lettura definizione per i metadati degli oggetti &#40;Analysis Services&#41;](grant-read-definition-permissions-on-object-metadata-analysis-services.md) per informazioni dettagliate.  
  
## <a name="set-permissions-on-a-cube-dimension"></a>Impostare le autorizzazioni su una dimensione del cubo  
 Le dimensioni del cubo sono dimensioni del database che sono state aggiunte a un cubo. Di conseguenza, sono strutturalmente dipendenti dai gruppi di misure associati. Sebbene sia possibile elaborare questi oggetti in modo atomico, in relazione all'autorizzazione è consigliabile gestire il cubo e le dimensioni del cubo come una sola entità.  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]connettersi all'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], espandere il nodo **Ruoli** relativo al database appropriato in Esplora oggetti, quindi fare clic su un ruolo del database o creare un nuovo ruolo del database.  
  
2.  Nel **quote** riquadro modificare la dimensione del set \<nome-cubo > **dimensioni cubo**.  
  
     Per impostazione predefinita, le autorizzazioni vengono ereditate da una dimensione del database corrispondente. Deselezionare la casella di controllo **Eredita** per modificare le autorizzazioni da **Lettura** a **Lettura/Scrittura**. Prima di usare l'autorizzazione **Lettura/Scrittura**, leggere la nota nella sezione precedente.  
  
> [!IMPORTANT]  
>  Se per configurare le autorizzazioni del ruolo del database si usa la libreria AMO (Analysis Management Objects), qualsiasi riferimento a una dimensione del cubo nell'attributo DimensionPermission di un cubo impedisce l'ereditarietà delle autorizzazioni dall'attributo DimensionPermission del database. Per altre informazioni su AMO, vedere [Sviluppo con AMO &#40;Analysis Management Objects&#41;](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo).  
  
## <a name="see-also"></a>Vedere anche  
 [Ruoli e autorizzazioni &#40;Analysis Services&#41;](roles-and-permissions-analysis-services.md)   
 [Concedere le autorizzazioni per un cubo o un modello &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)   
 [Concedere le autorizzazioni per le strutture e i modelli di data mining &#40;Analysis Services&#41;](grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [Concedere l'accesso personalizzato ai dati della dimensione &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md)   
 [Concedere l'accesso personalizzato ai dati delle celle &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md)  
  
  
