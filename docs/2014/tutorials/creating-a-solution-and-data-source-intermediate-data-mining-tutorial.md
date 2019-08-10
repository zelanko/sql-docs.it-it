---
title: Creazione di una soluzione e di un'origine dati (Esercitazione intermedia sul data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0488b231-1045-4169-aabb-c1005d86ca30
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 21bedc825f5890e3eb6551818dc5dc10724d2bf8
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891435"
---
# <a name="creating-a-solution-and-data-source-intermediate-data-mining-tutorial"></a>Creazione di una soluzione e di un'origine dati (Esercitazione intermedia sul data mining)
  Per usare il data mining, è necessario prima creare un progetto in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] usando il modello **Progetto multidimensionale e di data mining di Analysis Services**. Quando si apre il modello, nella finestra di progettazione vengono caricati tutti gli schemi che potrebbero essere necessari per il data mining: origini dati, strutture di data mining, modelli di data mining e persino cubi nel caso in cui nella struttura di data mining vengano usati dati multidimensionali.  
  
 Quando si crea il progetto, la soluzione viene archiviata come file locale finché non viene distribuita. Quando si distribuisce la soluzione, in [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] viene eseguita la ricerca del server [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] specificato nelle proprietà del progetto e viene creato un nuovo database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] con lo stesso nome del progetto. Per impostazione predefinita, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] usa l'istanza **localhost** per i nuovi progetti. Se si usa un'istanza denominata o si specifica un nome diverso per l'istanza predefinita, è necessario impostare la proprietà del database di distribuzione del progetto sul percorso in cui creare gli oggetti di data mining.  
  
 Per ulteriori informazioni sui [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] progetti, vedere [creare un Analysis Services progetto &#40;SSDT&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt).  
  
### <a name="to-create-a-new-analysis-services-project-for-this-tutorial"></a>Per creare un nuovo progetto di Analysis Services per questa esercitazione  
  
1.  Aprire [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.  
  
3.  Selezionare **Progetto multidimensionale e di data mining di Analysis Services** nel riquadro **Modelli installati** .  
  
4.  Nella casella **Nome** assegnare al nuovo progetto il nome **DM Intermediate**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-instance-where-data-mining-objects-are-stored-optional"></a>Per modificare l'istanza in cui sono archiviati gli oggetti di data mining (facoltativo)  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]scegliere **Proprietà** dal menu **Progetto**.  
  
2.  Fare clic su **Distribuzione** sul lato sinistro del riquadro **Pagine delle proprietà**.  
  
3.  Verificare che il nome di **Server** sia **localhost**. Se si usa un'altra istanza, digitarne il nome. Se si usa un'istanza denominata di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], digitare il nome del computer, quindi il nome dell'istanza. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-deployment-properties-for-a-project-optional"></a>Per modificare le proprietà di distribuzione di un progetto (facoltativo)  
  
1.  In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Proprietà**.  
  
     -oppure-  
  
     In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]scegliere **Proprietà** dal menu **Progetto**.  
  
2.  Fare clic su **Distribuzione** sul lato sinistro del riquadro **Pagine delle proprietà**.  
  
     Nel riquadro **Opzioni** selezionare **Modalità di distribuzione**e impostare le opzioni su **Distribuisci tutto** per sovrascrivere o su **Distribuisci solo modifiche** per aggiornare gli oggetti esistenti o aggiungere altri oggetti.  
  
## <a name="creating-a-data-source"></a>Creazione di un'origine dati  
 Nell'esercitazione di base sul data mining è stata creata un' *origine dati* in cui vengono archiviate le informazioni di connessione per il database [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] . Eseguire gli stessi passaggi per creare l'origine dati [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] in questa soluzione.  
  
#### <a name="to-create-a-data-source"></a>Per creare un'origine dati  
  
-   [Esercitazione sulla creazione di &#40;un'origine dati di base sul data mining&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
 Un'unica origine dati può supportare più viste origine dati, ognuna delle quali può includere più tabelle. Tuttavia, poiché l'origine dati e la vista origine dati vengono distribuite nel database di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] insieme ai modelli di data mining creati dall'utente, è consigliabile includere in ogni vista origine dati solo le tabelle necessarie per ogni modello di data mining o gruppo di modelli.  
  
 Nelle lezioni successive verranno aggiunte alcune viste origine dati per supportare ognuno dei nuovi scenari. Solo nelle lezioni relative alle analisi degli acquisti e al clustering delle sequenze viene usata la stessa vista origine dati; diversamente, in ogni scenario viene usata una vista origine dati diversa. Le lezioni sono pertanto indipendenti l'una dall'altra e possono essere completate separatamente.  
  
|Scenario|Dati inclusi nella vista origine dati|  
|--------------|-------------------------------------------|  
|[Lezione 2: Creazione di un'esercitazione intermedia &#40;sul data mining di uno scenario di previsione&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)|Report mensili sulle vendite per i modelli di bicicletta nelle diverse aree geografiche, raccolti come singola vista.|  
|[Lezione 3: Creazione di uno scenario &#40;Market basket esercitazione intermedia sul data mining&#41;](../../2014/tutorials/lesson-3-building-a-market-basket-scenario-intermediate-data-mining-tutorial.md)|Tabella contenente un elenco di ordini cliente e tabella annidata che mostra i singoli acquisti per ciascun cliente.|  
|[Lezione 4: Esercitazione sulla creazione di uno scenario &#40;di clustering delle sequenze intermedio di data mining&#41;](../../2014/tutorials/lesson-4-build-sequence-clustering-scenario-intermediate-data-mining.md)|Gli stessi dati usati per il Market basket analysis, con l'aggiunta di un identificatore che mostra l'ordine in cui sono stati acquistati gli articoli.|  
|[Lezione 5: Creazione di modelli &#40;di data mining di rete neurale e di regressione logistica intermedia&#41;](../../2014/tutorials/lesson-5-build-models-intermediate-data-mining-tutorial.md)|Singola tabella contenente i dati preliminari sul monitoraggio delle prestazioni provenienti da un call center.|  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 2: Creazione di un'esercitazione intermedia &#40;sul data mining di uno scenario di previsione&#41;](../../2014/tutorials/lesson-2-building-a-forecasting-scenario-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Progetti di data mining](../../2014/analysis-services/data-mining/data-mining-projects.md)   
 [Viste origine dati in modelli multidimensionali](https://docs.microsoft.com/analysis-services/multidimensional-models/data-source-views-in-multidimensional-models)  
  
  
