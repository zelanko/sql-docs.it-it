---
title: Drill-through sulle strutture di Data Mining | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a0b00a3b-f9db-4289-a8cb-ddf600cd64ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9eb585f756c03388bfe5b280a75b85f57d35394d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722417"
---
# <a name="drillthrough-on-mining-structures"></a>Drill-through sulle strutture di data mining
  Il termine*drill-through* indica la possibilità di eseguire query su un modello o una struttura di data mining e di ottenere dati dettagliati non esposti nel modello.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] offre due diverse opzioni per il drill-through dei dati del case. È possibile eseguire il drill-through dei dati utilizzati per compilare il modello di data mining o dei dati di origine nella struttura di data mining.  
  
## <a name="drillthrough-to-model-cases-vs-drillthrough-to-structure"></a>Drill-through nei case del modello e drill-through nella struttura  
 Il drill-through nei **case del modello** è utile per trovare dettagli aggiuntivi su regole, schemi o cluster in un modello.  
  
 Al contrario, il **drill-through dei dati della struttura** consente l'accesso a informazioni non disponibili nel modello. Ad esempio, se si dispone delle autorizzazioni appropriate, è possibile risalire alle righe di dati utilizzate per il training del modello e a quelle utilizzate per il test.  
  
 È possibile visualizzare gli attributi dei dati non utilizzati nell'analisi, a condizione che siano stati inclusi nella definizione della struttura. Ad esempio, le strutture di data mining supportano spesso molti tipi diversi di modelli ed è possibile che alcune colonne della struttura siano state escluse da un modello perché il tipo di dati era incompatibile o i dati non erano utili per l'analisi. Non è ad esempio consigliabile utilizzare le informazioni di contatto del cliente in un modello di clustering, anche se i dati sono stati inclusi nella struttura, tuttavia abilitando il drill-through è possibile accedere a queste informazioni senza eseguire query separate sull'origine dati.  
  
## <a name="enabling-drillthrough-to-structure-data"></a>Abilitazione del drill-through per i dati della struttura  
 Per utilizzare il drill-through per la struttura di data mining, è necessario soddisfare le condizioni seguenti:  
  
-   È anche necessario abilitare il drill-through per il modello. Per impostazione predefinita, entrambi i tipi di drill-through sono disabilitati. Per abilitare il drill-through nella Creazione guidata modello di data mining, selezionare l'opzione per abilitare il drill-through per i case del modello nell'ultima pagina della procedura guidata. È anche possibile abilitare in seguito il drill-through per un modello modificando la proprietà `AllowDrillthrough`.  
  
-   Se si crea la struttura di data mining utilizzando DMX, utilizzare la clausola WITH DRILLTHROUGH. Per altre informazioni, vedere [CREATE MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx).  
  
-   Il drill-through consiste nel recupero delle informazioni sui case di training memorizzati nella cache durante l'elaborazione della struttura di data mining. Pertanto, se i dati memorizzati nella cache vengono cancellati dopo l'elaborazione della struttura impostando la proprietà <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> su `ClearAfterProcessing`, il drill-through non funziona. Per abilitare il drill-through per le colonne della struttura, è necessario impostare la proprietà <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> su `KeepTrainingCases` e rielaborare la struttura.  
  
-   Verificare che la struttura di data mining sia nel modello di data mining sia la [AllowDrillThrough](https://docs.microsoft.com/bi-reference/assl/properties/allowdrillthrough-element-assl) impostata su `True`. È inoltre necessario essere membro di un ruolo che disponga delle autorizzazioni di drill-through sia per la struttura sia per il modello.  
  
## <a name="security-issues-for-drillthrough"></a>Problemi di sicurezza correlati al drill-through  
 Le autorizzazioni di drill-through vengono impostate separatamente per la struttura e per il modello. L'autorizzazione del modello consente di eseguire il drill-through dal modello, anche se non si dispone di autorizzazioni sulla struttura. Le autorizzazioni di drill-through per la struttura consentono di includere colonne della struttura nelle query di drill-through dal modello usando la funzione [StructureColumn &#40;DMX&#41;](/sql/dmx/structurecolumn-dmx).  
  
 Per altre informazioni su come creare ruoli e assegnare autorizzazioni in Analysis Services, vedere [Progettazione ruoli &#40;Analysis Services - Dati multidimensionali&#41;](https://msdn.microsoft.com/library/ms189696(v=sql.120).aspx).  
  
> [!NOTE]  
>  Se si abilita il drill-through per la struttura e per il modello di data mining, qualsiasi utente che sia un membro di un ruolo che dispone delle autorizzazioni di drill-through per il modello di data mining può anche visualizzare le colonne della struttura di data mining, anche se tali colonne non sono incluse nel modello di data mining. Pertanto, per proteggere i dati sensibili, è necessario configurare la vista origine dati per mascherare le informazioni personali e consentire l'accesso drill-through alla struttura di data mining solo quando necessario.  
  
## <a name="related-tasks"></a>Attività correlate  
 Per ulteriori informazioni su come utilizzare il drill-through con i modelli di data mining, vedere gli argomenti seguenti:  
  
|||  
|-|-|  
|Utilizzo del drill-through per la struttura dai visualizzatori del modello di data mining|[Usare il drill-through dai visualizzatori modello](use-drillthrough-from-the-model-viewers.md)|  
|Per tipi di modelli specifici, vedere gli esempi di query drill-through.|[Query di data mining](data-mining-queries.md)|  
|Ottenere informazioni sulle autorizzazioni applicabili a strutture e modelli di data mining specifici.|[Concedere le autorizzazioni per le strutture e i modelli di data mining &#40;Analysis Services&#41;](../multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Drill-through sui modelli di data mining](drillthrough-on-mining-models.md)  
  
  
