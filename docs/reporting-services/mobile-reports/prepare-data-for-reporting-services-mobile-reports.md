---
title: Preparare i dati per report di Reporting Services per dispositivi mobili | Microsoft Docs
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 8adce9ad-6a08-4d20-b1cf-d3c45544d8de
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9ded496c3509420d54325dc054e018048ede0732
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62499925"
---
# <a name="prepare-data-for-reporting-services-mobile-reports"></a>Preparare i dati per report di Reporting Services per dispositivi mobili
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)] supporta svariate operazioni sui dati complesse, tra le quali l'applicazione di filtri, l'aggregazione e l'assegnazione di intervalli di tempo per l'esecuzione. Questo articolo descrive alcuni degli aspetti di cui tenere conto durante la preparazione dei dati. La preaggregazione dei dati può essere utile per ottimizzare sia la creazione che l'uso dei report per dispositivi mobili ed è un requisito per alcune progettazioni di report per dispositivi mobili.   
  
## <a name="date-and-time-formats"></a>Formati di data e ora 
Durante la definizione degli intervalli di data e ora da usare in un report per dispositivi mobili, in particolare con lo strumento di spostamento temporale, è importante formattare correttamente la colonna di data/ora in modo che possa essere identificata come tale da [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] . Ecco alcuni esempi di formati di data/ora validi:  
  
    05/01/2009    
    2009-05-01    
    05/01/2009 14:57:32.8    
    2009-05-01 14:57:32.8    
    2009-05-01T14:57:32.8375298-04:00    
    5/01/2008 14:57:32.80 -07:00    
    1 May 2008 2:57:32.8 PM    
    Fri, 15 May 2009 20:10:57 GMT    
  
I set di dati basati su data e ora possono essere descritti, nella maggior parte dei casi, da uno o più intervalli di data/ora, ad esempio orario, giornaliero, mensile, trimestrale e annuale. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] consente di combinare più tabelle con livelli di granularità diversi e visualizzarli in un singolo report per dispositivi mobili. Tenere conto, tuttavia, degli intervalli rilevanti dai set di dati originali, perché possono essere utili per decidere quale opzioni di filtro di data/ora presentare all'utente nel report per dispositivi mobili finale.  

I campi di data in modelli di [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] multidimensionali e tabulari possono perdere la formattazione della data nei set di dati condivisi. Per una soluzione che ne preservi la formattazione, vedere [Retain date formatting for Analysis Services in mobile reports](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md) (Mantenere la formattazione della data per i dati di Analysis Services nei report per dispositivi mobili).
  
## <a name="preparing-filter-data"></a>Preparazione dei dati di filtro ##  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] consente di filtrare i dati sia in base ai campi di data/ora che ai campi chiave. Anche se i campi chiave possono essere numerici, nella maggior parte dei casi si tratta di un ID o un valore stringa. Per preparare un campo di filtro da usare con un elemento di navigazione, come l'elenco di selezione, la chiave del filtro deve essere una singola colonna nella tabella dati. In questo modo, è possibile raggruppare le righe della tabella in base al valore nella colonna di filtro. La disponibilità di più colonne con diverse chiavi di filtro, o criteri di filtro, consente di usare i report per dispositivi mobili insieme a più strumenti di navigazione di filtro, in modo gerarchico o singolarmente.  
  
| Settore  | Country   | Region    |  
| ------------- | ------------- | ------------- |  
| Banche     | AFGHANISTAN   | ASIA      |  
| Servizi commerciali e professionali | AFGHANISTAN | ASIA |  
| Alimentari, bevande e tabacco | AFGHANISTAN | ASIA |  
| Supporti | AFGHANISTAN | ASIA |  
| Prodotti farmaceutici | AFGHANISTAN | ASIA |  
| Commercio al dettaglio di alimentari e beni di consumo | ALBANIA | EUROPA |  
  
  
I filtri basati su chiave potrebbero anche essere strutturati in modo gerarchico per l'uso con un elenco di selezione in una struttura ad albero. Per preparare i dati per l'uso in questo tipo di scenario, creare una tabella di ricerca che descrive la struttura gerarchica. Usare una struttura di tabella che include una colonna chiave e una colonna chiave padre per indicare la posizione di appartenenza di un nodo nella gerarchia globale.  
  
In questa tabella, gli elementi ChiavePadre vengono prima elencati nella colonna ChiaveElemento e poi nella colonna ChiaveElementoPadre accanto agli elementi figlio corrispondenti.   
  
|ChiaveElemento    | ChiaveElementoPadre |  
| ------------- | ------------- |  
| Finanza    |   |  
| Industria   |   |  
| Beni di consumo |    |  
| Beni voluttuari |  |     
| Sanità   |   |  
| Tecnologia informatica |  |  
| Banche | Finanza |  
| Beni immobili | Finanza |  
| Finanza diversificata |  Finanza |   
| Assicurazioni |   Finanza |  
| Servizi commerciali e professionali |  Industria |  
| Beni strumentali |   Industria |  
| Trasporti |  Industria |  
| Alimentari, bevande e tabacco |    Beni di consumo |  
| Commercio al dettaglio di alimentari e beni di consumo |    Beni di consumo |  
| Prodotti per la casa e per la persona | Beni di consumo |  
| Supporti | Beni voluttuari |  
| Automobili e componentistica |  Beni voluttuari |  
| Beni durevoli e abbigliamento |Beni voluttuari |  
| Servizi al consumo |   Beni voluttuari |  
| Commercio | Beni voluttuari |  
| Prodotti farmaceutici   | Sanità |  
| Attrezzature e servizi sanitari |    Sanità |  
| Software e servizi | Tecnologia informatica |  
| Tecnologia - Attrezzature e hardware   | Tecnologia informatica |  
| Servizi di telecomunicazione |Tecnologia informatica |  
  
### <a name="see-also"></a>Vedere anche  
- [Preparare i dati di Excel per i report per dispositivi mobili di Reporting Services](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md)  
- [Retain date formatting for Analysis Services in mobile reports](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md)
- [Creare report per dispositivi mobili con SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
  
  
  

