---
title: Partizioni abilitate per la scrittura | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- storage [Analysis Services], partitions
- write-enabled partitions [Analysis Services]
- partitions [Analysis Services], write-enabled
- partitions [Analysis Services], storage
- writeback [Analysis Services], partitions
- storing data [Analysis Services], partitions
ms.assetid: 46e7683f-03ce-4af2-bd99-a5203733d723
author: minewiskan
ms.author: owend
ms.openlocfilehash: bd4bd012847c3aee231767e94bead86a507ecc53
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545223"
---
# <a name="write-enabled-partitions"></a>Partizioni abilitate per la scrittura
  I dati di un cubo sono in genere di sola lettura. In determinati scenari, tuttavia, può rivelarsi utile abilitare una partizione per la scrittura. Le partizioni abilitate per la scrittura vengono utilizzate per consentire agli utenti aziendali di sperimentare vari scenari modificando i valori delle celle e analizzando gli effetti delle modifiche sui dati del cubo. Quando si abilita per la scrittura una partizione, le applicazioni client potranno registrare modifiche ai dati nella partizione. Tali modifiche, note come dati writeback, vengono archiviate in una tabella separata e non sovrascrivono i dati esistenti in un gruppo di misure. Vengono però incorporate nei risultati delle query come se facessero parte dei dati del cubo.  
  
 È possibile abilitare per la scrittura un intero cubo o soltanto determinate partizioni nel cubo. Le dimensioni abilitate per la scrittura sono diverse ma complementari. Una partizione abilitata per la scrittura consente agli utenti di aggiornare le celle della partizione, mentre una dimensione abilitata per la scrittura consente agli utenti di aggiornare i membri della dimensione. È inoltre possibile utilizzare queste due caratteristiche in combinazione. Una partizione o un cubo abilitato per la scrittura, ad esempio, non deve necessariamente includere dimensioni abilitate per la scrittura. **Argomento correlato:**[dimensioni abilitate](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)per la scrittura.  
  
> [!NOTE]  
>  Se si desidera abilitare per la scrittura un cubo con un database Microsoft Access come origine dati, non utilizzare il provider Microsoft OLE DB per driver ODBC nelle definizioni dell'origine dati del cubo, delle partizioni o delle dimensioni. Utilizzare invece il provider Microsoft OLE DB per Jet versione 4.0 o qualsiasi versione del Service Pack di Jet che include OLE per Jet 4.0. Per ulteriori informazioni, vedere l'articolo della Microsoft Knowledge base [come ottenere la Service Pack più recente per Microsoft Jet 4,0 motore di database](https://support.microsoft.com/?kbid=239114).  
  
 Un cubo può essere abilitato per la scrittura solo se tutte le misure utilizzano la funzione di aggregazione `Sum`. I gruppi di misure collegati e i cubi locali non possono essere abilitati per la scrittura.  
  
## <a name="writeback-storage"></a>Archiviazione writeback  
 Qualsiasi modifica apportata dall'utente aziendale viene archiviata nella tabella writeback come differenza rispetto al valore attualmente visualizzato. Se, ad esempio, un utente finale modifica il valore di una cella da 90 a 100, nella tabella writeback verrà archiviato il valore `+10`, insieme all'ora della modifica e alle informazioni sull'utente aziendale che l'ha apportata. Alle applicazioni client viene visualizzato il risultato finale delle modifiche cumulative. In questo modo, il valore originale del cubo viene mantenuto e nella tabella writeback viene memorizzata un itinerario di controllo delle modifiche.  
  
 Le modifiche apportate a celle foglia e non foglia vengono gestite in modo diverso. Una cella foglia rappresenta un'intersezione di una misura e un membro foglia di ogni dimensione a cui fa riferimento il gruppo di misure. Il valore di una cella foglia viene recuperato direttamente dalla tabella dei fatti e non può essere suddiviso ulteriormente tramite il drill-down. Se qualsiasi partizione o un cubo è abilitato per la scrittura, possono essere apportate modifiche alle celle foglia. Le celle non foglia possono essere modificate solo se l'applicazione client consente di distribuire le modifiche tra le celle foglia che compongono la cella non foglia. Questo processo, denominato allocazione, viene gestito tramite l'utilizzo dell'istruzione UPDATE CUBE in espressioni MDX (MultiDimensional Expression). Gli sviluppatori di applicazioni di Business Intelligence possono utilizzare l'istruzione UPDATE CUBE per includere funzionalità di allocazione. Per ulteriori informazioni, vedere [istruzione UPDATE CUBE &#40;&#41;MDX ](/sql/mdx/mdx-data-manipulation-update-cube).  
  
> [!IMPORTANT]  
>  Quando celle aggiornate non si sovrappongono, la proprietà della stringa di connessione `Update Isolation Level` può essere utilizzata per migliorare le prestazioni di UPDATE CUBE. Per altre informazioni, vedere <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>.  
  
 Indipendentemente dal fatto che un'applicazione client distribuisca le modifiche apportate alle celle non foglia, durante la valutazione delle query le modifiche nella tabella writeback vengono applicate sia alle celle foglia che alle celle non foglia. Gli utenti aziendali possono pertanto verificare gli effetti delle modifiche nell'intero cubo.  
  
 Le modifiche apportate dall'utente aziendale vengono mantenute in una tabella writeback separata che può essere utilizzata come segue:  
  
-   Convertita in una partizione per incorporare le modifiche nel cubo in modo definitivo. Il gruppo di misure verrà impostato automaticamente come di sola lettura. È possibile specificare un'espressione filtro per selezionare le modifiche da convertire.  
  
-   Ignorata in modo da ripristinare lo stato originale della partizione. La partizione verrà impostata automaticamente come di sola lettura.  
  
## <a name="security"></a>Sicurezza  
 Un utente aziendale è autorizzato a registrare modifiche nella tabella writeback di un cubo solo se appartiene a un ruolo con autorizzazione in lettura/scrittura per le celle del cubo. È possibile determinare le singole celle del cubo aggiornabili per ogni ruolo. Per ulteriori informazioni, vedere [Grant Cube or Model permissions &#40;Analysis Services&#41;](../multidimensional-models/grant-cube-or-model-permissions-analysis-services.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Dimensioni abilitate per la scrittura](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)   
 [Aggregazioni e progettazioni delle aggregazioni](../multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)   
 [Partizioni &#40;Analysis Services Dati multidimensionali&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Dimensioni abilitate per la scrittura](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  
