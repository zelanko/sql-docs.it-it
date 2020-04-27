---
title: Selezione dimensione cubo di origine (creazione guidata modello di data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.selectsourcecube.f1
ms.assetid: 556e216b-5e21-4160-967d-4c57591fbab4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bdb61763a49bad7eae1a49a01633ec8f45e27642
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66069224"
---
# <a name="select-the-source-cube-dimension-data-mining-wizard"></a>Selezione dimensione cubo di origine (Creazione guidata modello di data mining)
  Usare la pagina **Selezione dimensione cubo di origine** per selezionare la dimensione del cubo contenente i case da analizzare. Se, ad esempio, si compila un modello che analizza il comportamento di acquisto dei clienti in base ai dati demografici, è necessario selezionare la dimensione Customer che in genere contiene un record univoco per ogni cliente e vari attributi che rappresentano i dati demografici, ad esempio sesso, ubicazione o reddito. Più avanti nella procedura guidata si potrà aggiungere una tabella correlata a questa tabella del case, ad esempio una tabella nidificata in cui sono elencati i prodotti acquistati dal cliente.  
  
> [!NOTE]  
>  Questa pagina viene visualizzata solo se è stata selezionata l'opzione **Da cubo esistente** nella pagina **Selezione metodo di definizione** della procedura guidata.  
  
## <a name="options"></a>Opzioni  
 **Selezionare una dimensione del cubo di origine**  
 Consente di selezionare la dimensione del cubo da cui verranno recuperati i dati dell'origine per la struttura di data mining.  
  
## <a name="choosing-a-dimension"></a>Scelta di una dimensione  
 Poiché è possibile selezionare una sola dimensione da utilizzare nel modello, è importante comprendere la struttura del cubo e selezionare la dimensione che fornisce le informazioni più appropriate per il modello. In caso di dubbi sulla dimensione da utilizzare, potrebbe essere utile esplorare il cubo ed esaminare i campi e i dati delle dimensioni utilizzando Progettazione dimensioni. Per altre informazioni, vedere [Esplorare i dati di una dimensione in Progettazione dimensioni](multidimensional-models/database-dimensions-browse-dimension-data-in-dimension-designer.md).  
  
 Se non si ha familiarità con le dimensioni in generale, vedere [Introduzione alle dimensioni &#40;Analysis Services - Dati multidimensionali&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md).  
  
 Per altre informazioni sul tipo di informazioni generalmente contenute in una singola dimensione, inclusi gli attributi e le misure che potrebbero essere utili per il data mining, vedere [Relazioni tra dimensioni](multidimensional-models-olap-logical-cube-objects/dimension-relationships.md).  
  
 Se la dimensione scelta non contiene tutti gli attributi correlati richiesti per la compilazione del modello di data mining, potrebbe essere necessario modificarla. Per altre informazioni, vedere [Definire le dimensioni del database](multidimensional-models/define-database-dimensions.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Guida sensibile al contesto della creazione guidata modello di data mining &#40;Analysis Services-&#41;di data mining](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Creazione della struttura di data mining &#40;creazione guidata modello di data mining&#41;](create-the-data-mining-structure-data-mining-wizard.md)   
 [Selezionare la chiave del case &#40;creazione guidata modello di data mining&#41;](select-the-case-key-data-mining-wizard.md)  
  
  
