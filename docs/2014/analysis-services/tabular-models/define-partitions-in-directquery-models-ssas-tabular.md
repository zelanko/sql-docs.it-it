---
title: Partizioni e modalità DirectQuery (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 5f179ba9-6efb-46ae-90e5-945bbfddb719
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f445b32e0c580cde10f38a22b3d26270d927c5a1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62757316"
---
# <a name="partitions-and-directquery-mode-ssas-tabular"></a>Partizioni e modalità DirectQuery (SSAS tabulare)
  In questa sezione viene illustrato come utilizzare le partizioni nei modelli DirectQuery. Per informazioni più generali sulle partizioni nei modelli tabulari, vedere [Partizioni &#40;SSAS tabulare&#41;](partitions-ssas-tabular.md).  
  
 Per istruzioni su come modificare la partizione utilizzata o visualizzare le informazioni sulla partizione, vedere [modificare la partizione DirectQuery &#40;modello tabulare di SSAS&#41;](../change-the-directquery-partition-ssas-tabular.md).  
  
## <a name="using-partitions-in-directquery-mode"></a>Utilizzo di partizioni in modalità DirectQuery  
 Per ogni tabella, è necessario specificare una sola partizione da utilizzare come origine dati DirectQuery.  In presenza di più partizioni, quando si abilita la modalità DirectQuery per il modello, per impostazione predefinita la prima partizione creata nella tabella viene contrassegnata come partizione DirectQuery. Questa impostazione potrà essere modificata in seguito tramite Gestione partizioni in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Perché consentire una sola partizione nella modalità DirectQuery?  
  
 Nei modelli tabulari, come nei modelli OLAP, le partizioni di una tabella sono definite tramite query SQL. È responsabilità dello sviluppatore che crea la definizione della partizione assicurarsi che le partizioni non si sovrappongano. In Analysis Services non viene controllato se i record fanno parte di una o più partizioni.  
  
 Le partizioni in un modello tabulare memorizzato nella cache si comportano allo stesso modo. Se si utilizza un modello in memoria, durante l'accesso alla cache, le formule DAX vengono valutate per ogni partizione e i risultati vengono combinati. Tuttavia, quando un modello tabulare utilizza la modalità DirectQuery, sarebbe impossibile valutare più partizioni, combinare i risultati e convertirli in un'istruzione SQL per l'invio all'archivio dati relazionale. Questa operazione potrebbe causare una calo inaccettabile delle prestazioni, nonché imprecisioni potenziali durante l'aggregazione dei dati.  
  
 Quindi, per query risposte in modalità DirectQuery, il server usa una sola partizione contrassegnata come partizione primaria per l'accesso DirectQuery, denominata *partizione DirectQuery*.  La query SQL specificata nella definizione di questa partizione definisce il set completo di dati che possono essere usati per rispondere alle query in modalità DirectQuery.  
  
 Se non si definisce in modo esplicito una partizione, il motore emette una query SQL sull'intera origine dati relazionale, esegue eventuali operazioni basate su set imposte dalla formula DAX e restituisce i risultati della query.  
  
 Se sono state create più partizioni in una tabella e si seleziona una partizione come DirectQuery, per impostazione predefinita tutte le altre partizioni vengono contrassegnate automaticamente per il solo utilizzo in memoria.  
  
## <a name="partitions-in-cached-models-and-in-directquery-models"></a>Partizioni nei modelli memorizzati nella cache e nei modelli DirectQuery  
 Quando si configura una partizione DirectQuery, è necessario specificare le opzioni di elaborazione per la partizione.  
  
 Sono disponibili due opzioni di elaborazione per la partizione DirectQuery: Per impostare questa proprietà, utilizzare **Gestore partizioni** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e selezionare la proprietà **Opzione di elaborazione** . Nella tabella seguente vengono elencati i valori di questa proprietà e vengono illustrati gli effetti di ciascun valore combinato alla proprietà DirectQueryUsage nella stringa di connessione:  
  
|**DirectQueryUsage** property|Proprietà**Opzione di elaborazione** |Note|  
|-----------------------------------|------------------------------------|-----------|  
|DirectQuery|Non elaborare mai questa partizione|Se il modello utilizza solo DirectQuery, l'elaborazione non è mai necessaria.<br /><br /> Nei modelli ibridi è possibile configurare la partizione DirectQuery in modo che non venga mai elaborata. Ad esempio, se si lavora su un set di dati di grandi dimensioni e non si desidera che i risultati completi vengano aggiunti alla cache, è possibile specificare che la partizione DirectQuery includa l'unione dei risultati di tutte le altre partizioni nella tabella e quindi non elaborare mai l'unione. Le query dirette all'origine relazionale non saranno interessate, mentre le query sui dati memorizzati nella cache combineranno i dati delle altre partizioni.|  
|In-Memory con DirectQuery|Consenti l'elaborazione della partizione|Se il modello utilizza la modalità ibrida, è necessario utilizzare la stessa partizione per le query su In-Memory e sull'origine dati DirectQuery.|  
  
## <a name="see-also"></a>Vedere anche  
 [Partizioni &#40;SSAS tabulare&#41;](partitions-ssas-tabular.md)  
  
  
