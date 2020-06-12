---
title: Traduzioni nei modelli multidimensionali | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.deletelanguagefirm.f1
ms.assetid: 5521f8ef-b10a-4861-9df7-1e43e0a1fb3f
author: minewiskan
ms.author: owend
ms.openlocfilehash: d01aeb00c7cf96bf993867388d6a2cbbede82d90
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547313"
---
# <a name="translations-in-multidimensional-models"></a>Traduzioni nei modelli multidimensionali
  Il supporto multilingue in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene eseguito tramite le traduzioni. Ogni traduzione include un identificatore di lingua e le associazioni per le proprietà degli oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che possono essere visualizzati in più lingue. Ad esempio, è possibile definire una traduzione per un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] al fine di visualizzare la didascalia e la descrizione di tale database nella lingua specificata. Per ulteriori informazioni sulle traduzioni, vedere la pagina relativa alle [traduzioni dei cubi](../multidimensional-models-olap-logical-cube-objects/cube-translations.md).  
  
## <a name="defining-translations"></a>Definizione di traduzioni  
 È possibile definire le traduzioni in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] mediante la finestra di progettazione appropriata per l'oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da tradurre. Mediante la definizione di una traduzione viene creato un oggetto `Translation` associato all'oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] appropriato con i valori letterali espliciti specificati, nella lingua indicata, per le proprietà dell'oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] correlato.  
  
 Agli oggetti e alle proprietà seguenti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] possono essere associate le traduzioni corrispondenti:  
  
|Oggetto|Proprietà|Designer|  
|------------|----------------|--------------|  
|Database|`Caption`, `Description`|[&#40;generale di progettazione database&#41; &#40;Analysis Services Dati multidimensionali&#41;](../general-database-designer-analysis-services-multidimensional-data.md)|  
|Cube|`Caption`, `Description`|[Traduzioni &#40;Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Gruppo di misure|`Caption`|[Traduzioni &#40;Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Measure|`Caption`, `DisplayFolder`|[Traduzioni &#40;Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Dimensione del cubo|`Caption`|[Traduzioni &#40;Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Prospettiva|`Caption`|[Traduzioni &#40;Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Indicatore di prestazioni chiave|`Caption`, `Description`, `DisplayFolder`|[Traduzioni &#40;Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Azione|`Caption`|[Traduzioni &#40;Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Set denominato|`Caption`|[Traduzioni &#40;Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|membro calcolato|`Caption`|[Traduzioni &#40;Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](../translations-cube-designer-analysis-services-multidimensional-data.md)|  
|Dimensione del database|`Caption`, `AttributeAllMember`|[Traduzioni &#40;Progettazione dimensioni&#41; &#40;Analysis Services Dati multidimensionali&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|Attributo|`Caption`, `CaptionColumn` <sup>1</sup>, `AttributeHierarchyDisplayFolder` , `NamingTemplate` ,`MembersWithDataCaption`|[Traduzioni &#40;Progettazione dimensioni&#41; &#40;Analysis Services Dati multidimensionali&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|Gerarchia|`Caption`, `AllMemberName`|[Traduzioni &#40;Progettazione dimensioni&#41; &#40;Analysis Services Dati multidimensionali&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
|Level|`Caption`|[Traduzioni &#40;Progettazione dimensioni&#41; &#40;Analysis Services Dati multidimensionali&#41;](../translations-dimension-designer-analysis-services-multidimensional-data.md)|  
  
 <sup>1</sup> la `CaptionColumn` proprietà di un attributo può essere associata a una colonna in una vista origine dati e può utilizzare regole di confronto di Windows diverse da quelle specificate per l'istanza, a differenza di altre traduzioni.  
  
### <a name="defining-attribute-translations"></a>Definizione di traduzioni degli attributi  
 Le traduzioni associate agli attributi nelle dimensioni del database vengono gestite in modo diverso rispetto alle altre traduzioni, come illustrato di seguito:  
  
-   È possibile associare una colonna, anziché un valore letterale esplicito, alla proprietà `CaptionColumn` in modo da consentire la traduzione dei nomi dei membri dell'attributo.  
  
-   È possibile utilizzare regole di confronto di Windows diverse da quelle specificate per l'istanza in modo che i membri dell'attributo vengano ordinati correttamente per la lingua specificata nella traduzione.  
  
 È possibile utilizzare la finestra di dialogo **Traduzione dati attributo** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] per definire le traduzioni per gli attributi nelle dimensioni del database. Per ulteriori informazioni sulla finestra di dialogo **Traduzione dati attributo** , vedere la finestra di [dialogo traduzione dati attributi &#40;Analysis Services-&#41;dati multidimensionali ](../attribute-data-translation-dialog-box-analysis-services-multidimensional-data.md).  
  
## <a name="resolving-translations"></a>Risoluzione di traduzioni  
 Se un'applicazione client richiede informazioni corrispondenti all'identificatore di lingua specificato, l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta di risolvere i dati e i metadati per gli oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] approssimandoli all'identificatore di lingua più vicino. Se l'applicazione client non specifica una lingua predefinita oppure specifica l'identificatore delle impostazioni locali neutro (0) o l'identificatore della lingua predefinita (1024), [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce i dati e i metadati per l'oggetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nella lingua predefinita.  
  
 Se l'applicazione client specifica un identificatore di lingua diverso da quello della lingua predefinita, l'istanza scorre tutte le traduzioni disponibili per tutti gli oggetti disponibili. Se l'identificatore di lingua specificato corrisponde all'identificatore di lingua di una traduzione, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] restituisce tale traduzione. Nel caso in cui non sia possibile trovare una corrispondenza, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta di utilizzare uno dei metodi seguenti per restituire l'identificatore di lingua più vicino a quello specificato.  
  
-   Per gli identificatori di lingua seguenti, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta di utilizzare un identificatore di lingua alternativo se non è stata definita una traduzione per l'identificatore di lingua specificato:  
  
    |Identificatore di lingua specificato|Identificatore di lingua alternativo|  
    |-----------------------------------|-----------------------------------|  
    |3076 - Cinese (Hong Kong SAR, RPC)|1028 - Cinese (Taiwan)|  
    |5124 - Cinese (RAS di Macao)|1028 - Cinese (Taiwan)|  
    |1028 - Cinese (Taiwan)|Lingua predefinita|  
    |4100 - Cinese (Singapore)|2052 - Cinese (RPC)|  
    |2074 - Croato|Lingua predefinita|  
    |3098 - Croato (alfabeto cirillico)|Lingua predefinita|  
  
-   Per tutti gli altri identificatori di lingua specificati, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] estrae la lingua principale dell'identificatore specificato e recupera l'identificatore indicato da Windows come corrispondenza più appropriata per la lingua principale. Se non è possibile trovare una traduzione per l'identificatore di lingua che rappresenta la corrispondenza più appropriata o se l'identificatore specificato è la corrispondenza più appropriata per la lingua principale, viene utilizzata la lingua predefinita.  
  
## <a name="deleting-translation-objects"></a>Eliminazione di oggetti Translation  
 È possibile fare clic con il pulsante destro del mouse su un oggetto di questo tipo in Progettazione dimensioni o Progettazione cubi per rimuoverlo definitivamente. Non è possibile ripristinare o riciclare un oggetto eliminato, quindi è opportuno accertarsi di controllare l'elenco degli oggetti interessati prima di continuare.  
  
## <a name="see-also"></a>Vedere anche  
 [Scenari di globalizzazione per Analysis Services multidimensionale](../globalization-scenarios-for-analysis-services-multiidimensional.md)   
 [Lingue e regole di confronto &#40;Analysis Services&#41;](../languages-and-collations-analysis-services.md)  
  
  
