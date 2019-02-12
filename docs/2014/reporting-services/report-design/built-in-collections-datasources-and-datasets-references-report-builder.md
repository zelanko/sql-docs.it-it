---
title: DataSources and DataSets Collection References (Report Builder and SSRS) (Riferimenti a raccolte DataSources e DataSets (Generatore report e SSRS)) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f951a4aa-da55-4e43-8579-4a5d4480d11f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b3663c9cdb9fd83dc0caa4298a81f73adcae87cd
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56039272"
---
# <a name="datasources-and-datasets-collection-references-report-builder-and-ssrs"></a>Riferimenti a raccolte DataSources e DataSets (Generatore report e SSRS)
  La raccolta `DataSources` rappresenta tutte le origini dati utilizzate in un report. Analogamente, la raccolta `DataSets` rappresenta tutti i set di dati per tutte le origini dati disponibili in un report. Usare il riquadro **Dati report** per ottenere una visualizzazione gerarchica dei set di dati del report organizzati sotto l'origine dati cui fanno riferimento. Se si includono riferimenti a queste raccolte, durante l'anteprima del report questi valori non verranno visualizzati. Le raccolte sono disponibili solo dopo la pubblicazione del report in un server di report.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="datasources"></a>DataSources  
 La raccolta `DataSources` rappresenta le origini dati a cui si fa riferimento nella definizione del report pubblicato. È possibile scegliere di includere queste informazioni nel report per documentare l'origine dei relativi dati, Questa raccolta non è disponibile in modalità **Anteprima** . Nella tabella seguente vengono descritte le variabili della raccolta `DataSources`.  
  
|**Variabile**|`Type`|**Descrizione**|  
|------------------|--------------|---------------------|  
|`DataSourceReference`|`String`|Percorso completo della definizione dell'origine dati nel server di report. Ad esempio, è possibile includere un elenco di tutte le origini dati utilizzate da un report come parte di una cronologia di report. Nell'esempio seguente è illustrato il percorso completo per l'origine dati denominata AdventureWorks2012:<br /><br /> `/DataSources/AdventureWorks2012` (Indici per tabelle con ottimizzazione per la memoria).|  
|`Type`|`String`|Tipo di provider di dati per l'origine dati. Ad esempio, `SQL`.|  
  
## <a name="datasets"></a>DataSets  
 La raccolta `DataSets` rappresenta i set di dati a cui si fa riferimento nella definizione del report. È possibile scegliere di includere la query nel report in una casella di testo, in modo che un utente interessato ai dati effettivi contenuti nel report possa vedere il testo del comando originale. Questa raccolta non è disponibile in modalità **Anteprima** . Nella tabella seguente vengono descritti i membri della raccolta `DataSets`.  
  
|**Membro**|`Type`|**Descrizione**|  
|----------------|--------------|---------------------|  
|`CommandText`|`String`|Per le origini dei dati database, si tratta della query utilizzata per recuperare dati dall'origine dei dati. Se la query è un'espressione, si tratta dell'espressione valutata.|  
|`RewrittenCommandText`|`String`|Valore CommandText espanso del provider di dati. Viene in genere utilizzato per i report con parametri query su cui viene eseguito il mapping a parametri report. Il provider di dati imposta questa proprietà quando espande i riferimenti ai parametri di testo di comando nei valori costanti selezionati per i parametri report su cui viene eseguito il mapping.|  
  
### <a name="using-query-expressions"></a>Utilizzo di espressioni di query  
 È possibile utilizzare le espressioni per definire la query contenuta in un set di dati. È possibile utilizzare questa funzionalità per progettare report in cui la query viene modificata in base all'input dell'utente, ai dati di altri set di dati o ad altre variabili. Per altre informazioni sulle query, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni &#40;Generatore report e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
  
