---
title: Creazione di una struttura di previsione e un modello (esercitazione intermedia di Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5f55cbf6-0db4-4cb4-a0f5-e27441873d4f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6e631a8983705d4f58e4b193823c9a255284f346
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56015252"
---
# <a name="creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial"></a>Creazione di una struttura e di un modello di previsione (Esercitazione intermedia sul data mining)
  Verrà ora utilizzata la Creazione guidata modello di data mining per creare una nuova struttura di data mining e un nuovo modello di data mining basati sulla vista origine dati appena creata. In questa attività si specificherà che il modello di data mining deve utilizzare l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series.  
  
### <a name="to-create-a-forecasting-mining-structure"></a>Per creare una struttura di data mining per la previsione  
  
1.  In Esplora soluzioni in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], fare doppio clic su **strutture di Data Mining** e selezionare **nuova struttura di Data Mining**.  
  
2.  Nella pagina iniziale **Creazione guidata modello di data mining** fare clic su **Avanti**.  
  
3.  Nel **Selezione metodo di definizione** verificare che **da esistenti database relazionale o data warehouse** sia selezionata e quindi fare clic su **Next**.  
  
4.  Nel **creare la struttura di Data Mining** nella pagina **tecnica di data mining si desidera utilizzare?**, selezionare **Microsoft Time Series**e quindi fare clic su  **Avanti**.  
  
5.  Nel **selezione vista origine dati** nella pagina **viste origine dati disponibili**, selezionare **SalesByRegion**.  
  
6.  Scegliere **Avanti**.  
  
7.  Nel **specificare i tipi di tabella** pagina, assicurarsi che la casella di controllo la **Case** colonna per la tabella vTimeSeries sia selezionata e quindi fare clic su **Avanti**.  
  
8.  Nel **specificare i dati di Training** pagina, selezionare le caselle di controllo nel **chiave** colonna per le colonne ModelRegion e ReportingDate.  
  
     La colonna ReportingDate dovrebbe essere selezionata per impostazione predefinita, poiché è stata specificata come chiave primaria logica quando è stata creata la vista origine dati. Aggiungendo ModelRegion come seconda chiave, si indica all'algoritmo di creare una serie temporale distinta per ogni combinazione di modello e area geografica elencata in questo campo.  
  
9. Selezionare le caselle di controllo di **Input** e **stimabile** colonne per la quantità di colonna e quindi fare clic su **Avanti**.  
  
     Selezionando **stimabile**, si indica che si desidera creare previsioni sui dati in questa colonna. Tuttavia, poiché si desidera basare le previsioni sui dati passati, è inoltre necessario aggiungere la colonna come input.  
  
10. Nella pagina **contenuto e tipo di dati specificare colonne**, rivedere le selezioni.  
  
     La colonna ModelRegion viene definita come una **Key** colonna e la colonna ReportingDate viene definita automaticamente come un **Key Time** colonna. È consentito un solo tipo per ogni tipo di chiave.  
  
11. Scegliere **Avanti**.  
  
12. Nel **Completamento procedura guidata** pagina, per **nome struttura di Data Mining**, tipo `Forecasting`.  
  
    > [!NOTE]  
    >  L'opzione di drill-through non è disponibile per i modelli Time Series.  
  
13. In **nome del modello di Data Mining**, digitare `Forecasting`, quindi fare clic su **fine**.  
  
     Verrà aperto Progettazione modelli di Data Mining per visualizzare il `Forecasting` struttura di data mining appena creato.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Modifica della struttura di previsione &#40;esercitazione intermedia sul Data Mining&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Progettazione modelli di data mining](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
