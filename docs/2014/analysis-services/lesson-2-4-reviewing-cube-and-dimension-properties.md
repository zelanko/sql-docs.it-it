---
title: Esame delle proprietà di dimensione e del cubo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: dda922b8-6d75-4662-b09e-8a317c6a1c70
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b4db6133a486e77369630dc717fab02b3be7f8e2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729297"
---
# <a name="reviewing-cube-and-dimension-properties"></a>Esame delle proprietà del cubo e delle dimensioni
  Dopo avere definito un cubo, è possibile verificare i risultati tramite Progettazione cubi. Nell'attività seguente si esaminerà la struttura del cubo nel progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial.  
  
### <a name="to-review-cube-and-dimension-properties-in-cube-designer"></a>Per verificare le proprietà del cubo e delle dimensioni in Progettazione cubi  
  
1.  Per aprire Progettazione cubi, fare doppio clic sul cubo **Analysis Services Tutorial** nel nodo **Cubi** di Esplora soluzioni.  
  
2.  Nel riquadro **Misure** della scheda **Struttura cubo** di Progettazione cubi espandere il gruppo di misure **Internet Sales** per visualizzare le misure definite.  
  
     È possibile modificare l'ordine trascinando le misure per disporle nel modo desiderato. L'ordine creato influisce sull'ordinamento di queste stesse misure da parte di alcune applicazioni client. Il gruppo di misure e ogni misura in esso contenuta presentano proprietà modificabili nella finestra Proprietà.  
  
3.  Nel riquadro **Dimensioni** della scheda **Struttura cubo** di Progettazione cubi verificare le dimensioni del cubo di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial.  
  
     Si noti che anche sa a livello di database sono state create solo tre dimensioni, visualizzate in Esplora soluzioni, nel cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial vi sono cinque dimensioni. Il cubo contiene più dimensioni del database poiché la dimensione Date del database viene usata come base per tre dimensioni separate del cubo relative alla data, basate su fatti relativi alla data diversi nella tabella dei fatti. Queste dimensioni relative alla data vengono anche denominate *dimensioni con ruoli multipli*. Le tre dimensioni relative alla data del cubo consentono agli utenti di dimensionare il cubo in base a tre fatti separati correlati alla vendita di ogni prodotto: la data di ordine del prodotto, la data di scadenza dell'evasione dell'ordine e la data di invio dell'ordine. Riutilizzando una sola dimensione del database per più dimensioni del cubo, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] semplifica la gestione delle dimensioni, utilizza meno spazio su disco e riduce il tempo di elaborazione totale.  
  
4.  Nel riquadro **Dimensioni** della scheda **Struttura cubo** espandere **Customer**, quindi fare clic su **Modifica Customer** per aprire la dimensione in Progettazione dimensioni.  
  
     Progettazione dimensioni contiene le schede: **Struttura dimensione**, **relazioni tra attributi**, **traduzioni**, e **Browser**. Si noti che il **struttura dimensione** scheda include tre riquadri: **Gli attributi**, **gerarchie**, e **vista origine dati**. Gli attributi contenuti nella dimensione vengono visualizzati nel riquadro **Attributi** . Per altre informazioni, vedere [Dimension Attribute Properties Reference](multidimensional-models/dimension-attribute-properties-reference.md), [gerarchie definite dall'utente](multidimensional-models/user-defined-hierarchies-create.md).  
  
5.  Per passare a Progettazione cubi, fare clic con il pulsante destro del mouse sul cubo **Analysis Services Tutorial** nel nodo **Cubi** in Esplora soluzioni e fare clic su **Progettazione viste**.  
  
6.  In Progettazione cubi fare clic sulla scheda **Utilizzo dimensioni** .  
  
     In questa vista del cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial è possibile vedere le dimensioni del cubo utilizzate dal gruppo di misure Internet Sales. È inoltre possibile definire il tipo di relazione tra ogni dimensione e ogni gruppo di misure in cui essa viene utilizzata.  
  
7.  Fare clic sulla scheda **Partizioni** .  
  
     Tramite la Creazione guidata cubo viene definita una singola partizione per il cubo utilizzando la modalità di archiviazione MOLAP (Multidimensional OnLine Analytical Processing, elaborazione analitica in linea multidimensionale) senza aggregazioni. Con la modalità MOLAP, la memorizzazione di tutti i dati a livello foglia e di tutte le aggregazioni avviene all'interno del cubo per ottenere prestazioni ottimali. Le aggregazioni sono riepiloghi precalcolati dei dati che consentono di migliorare il tempo di risposta alle query predisponendo le risposte prima che vengano formulate le domande. Nella scheda **Partizioni** è possibile definire ulteriori partizioni, impostazioni di archiviazione e impostazioni writeback. Per altre informazioni, vedere [Partizioni &#40;Analysis Services - Dati multidimensionali&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md), [Aggregazioni e progettazione di aggregazioni](multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md).  
  
8.  Fare clic sulla scheda **Esplorazione** .  
  
     Si noti che non è possibile esplorare il cubo poiché non è stato ancora distribuito in un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. A questo punto, il cubo del progetto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial è solo una definizione di cubo, che sarà possibile distribuire a qualunque istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Quando un cubo viene distribuito ed elaborato, gli oggetti definiti vengono creati in un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e quindi vengono popolati con i dati delle origini dati sottostanti.  
  
9. In Esplora soluzioni fare clic con il pulsante destro del mouse su **Analysis Services Tutorial** nel nodo **Cubi** e fare clic su **Visualizza codice**. Potrebbe essere necessario attendere alcuni istanti.  
  
     Il codice XML per il cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial viene visualizzato nella scheda **[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial.cube [XML]** . Si tratta del codice effettivo utilizzato per creare il cubo in un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] durante la distribuzione. Per altre informazioni, vedere [Visualizzare il codice XML per un progetto di Analysis Services &#40;SSDT&#41;](multidimensional-models/view-the-xml-for-an-analysis-services-project-ssdt.md).  
  
10. Chiudere la scheda del codice XML.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Distribuzione di un progetto di Analysis Services](lesson-2-5-deploying-an-analysis-services-project.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esplorare i dati di una dimensione in Progettazione dimensioni](multidimensional-models/database-dimensions-browse-dimension-data-in-dimension-designer.md)  
  
  
