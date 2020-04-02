---
title: Lavorare con dati simulati nei report di Reporting Services per dispositivi mobili | Microsoft Docs
description: Quando si inserisce un elemento della raccolta nell'area di progettazione, Mobile Report Publisher genera dati simulati per quell'elemento. Progettare i prototipi con i dati simulati.
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 6baabc36-58fb-4a98-bb9c-c42bafb16d0f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 39640b3ce6e8d3c8760e3c1a1153949426eba80c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "79448363"
---
# <a name="work-with-simulated-data-in-reporting-services-mobile-reports"></a>Lavorare con dati simulati nei report di Reporting Services per dispositivi mobili
Quando si inserisce un elemento della raccolta nell'area di progettazione, [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] genera immediatamente dati simulati per quell'elemento. Questi dati assolvono a molti scopi utili durante la creazione di report per dispositivi mobili.   
  
![SS_MRP_SimDataTreeMapProps](../../reporting-services/mobile-reports/media/ss-mrp-simdatatreemapprops.png)  
  
I dati simulati risultano utili quando si adotta un approccio di tipo progettuale alla creazione di report per dispositivi mobili. Il popolamento iniziale degli elementi con dati simulati consente di creare prototipi di report per dispositivi mobili in modo rapido, senza doversi preoccupare di specifici requisiti dei dati. Questi report per dispositivi mobili possono quindi essere valutati in termini generali di estetica ed efficienza.  
  
## <a name="create-an-excel-file-with-simulated-data-as-a-template"></a>Creare un file di Excel con dati simulati come modello  
  
I dati simulati forniscono anche un modello che rappresenta in modo accurato i requisiti dei dati di un determinato progetto di report per dispositivi mobili.   
  
-  Click **Esporta tutti i dati** nell'angolo in alto a destra della Vista dati.   
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] genera un documento di Excel contenente dati simulati, che possono essere sostituiti rapidamente con dati reali, pronto per l'importazione.   
  
## <a name="how-simulated-data-behaves"></a>Comportamento dei dati simulati  
  
I dati simulati generati sono personalizzati in modo specifico per il report per dispositivi mobili che si sta creando. Man mano che si posizionano altri elementi nell'area di progettazione, i dati simulati associati aumentano e cambiano per fornire la migliore esperienza possibile in assenza di dati reali. Questa evoluzione assicura la possibilità di disporre di altri campi e filtri nel caso in cui si aggiungano serie supplementari nelle visualizzazioni grafico o si espanda altrimenti l'ambito di uno o più elementi dei report per dispositivi mobili.  
  
Come accennato in precedenza, è possibile esportare dati simulati in un file di Excel, creando un modello di dati ideale per il report per dispositivi mobili associato. È possibile scambiare i dati con i dati reali nel file di Excel e reimportarli in [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)].   
  
Dopo avere associato tutti i controlli a dati reali, le tabelle simulate non più in uso vengono rimosse automaticamente dal report per dispositivi mobili. Non è possibile rimuovere tabelle simulate a cui fanno ancora riferimento elementi nell'area di progettazione.  
  
>**Nota**: i dati simulati non contribuiscono al footprint complessivo del report per dispositivi mobili perché non sono serializzati con tale report, ma vengono generati in fase di esecuzione.  
  
### <a name="see-also"></a>Vedere anche  
- [Creare e pubblicare report per dispositivi mobili con SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-  Vedere [Visualizzare report per dispositivi mobili e indicatori KPI di SQL Server nell'app iPad](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-ipad-kpis-mobile-reports)  (Power BI per iOS)  
-  [Visualizzare report per dispositivi mobili e indicatori KPI di SQL Server nell'app iPhone](https://pbiwebprod-docs.azurewebsites.net/documentation/powerbi-mobile-iphone-kpis-mobile-reports) (Power BI per iOS)  
  
  
  
  
  

