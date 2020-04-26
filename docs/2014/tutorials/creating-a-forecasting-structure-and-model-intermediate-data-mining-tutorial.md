---
title: Creazione di una struttura e di un modello di previsione (Esercitazione intermedia sul data mining) | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63204806"
---
# <a name="creating-a-forecasting-structure-and-model-intermediate-data-mining-tutorial"></a>Creazione di una struttura e di un modello di previsione (Esercitazione intermedia sul data mining)
  Verrà ora utilizzata la Creazione guidata modello di data mining per creare una nuova struttura di data mining e un nuovo modello di data mining basati sulla vista origine dati appena creata. In questa attività si specificherà che il modello di data mining deve utilizzare l'algoritmo [!INCLUDE[msCoName](../includes/msconame-md.md)] Time Series.  
  
### <a name="to-create-a-forecasting-mining-structure"></a>Per creare una struttura di data mining per la previsione  
  
1.  In Esplora soluzioni in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]fare clic con il pulsante destro del mouse su **strutture di data mining** e scegliere **nuova struttura di data mining**  
  
2.  Nella pagina iniziale **Creazione guidata modello di data mining** fare clic su **Avanti**.  
  
3.  Nella pagina **Selezione metodo di definizione** verificare che sia selezionato **da database relazionale o data warehouse esistente** e quindi fare clic su **Avanti**.  
  
4.  Nella pagina **Crea la struttura di data mining** in **cui data mining tecnica si desidera utilizzare?** selezionare **Microsoft Time Series**, quindi fare clic su **Avanti**.  
  
5.  Nella pagina **Selezione vista origine dati** , in **viste origine dati disponibili**, selezionare **SalesByRegion**.  
  
6.  Fare clic su **Avanti**.  
  
7.  Nella pagina **impostazione tipi di tabelle** assicurarsi che la casella di controllo nella colonna **case** per la tabella vTimeSeries sia selezionata, quindi fare clic su **Avanti**.  
  
8.  Nella pagina **impostazione dati di training** selezionare le caselle di controllo nella colonna **chiave** per le colonne ModelRegion e ReportingDate.  
  
     La colonna ReportingDate dovrebbe essere selezionata per impostazione predefinita, poiché è stata specificata come chiave primaria logica quando è stata creata la vista origine dati. Aggiungendo ModelRegion come seconda chiave, si indica all'algoritmo di creare una serie temporale distinta per ogni combinazione di modello e area geografica elencata in questo campo.  
  
9. Selezionare le caselle di controllo nelle colonne **input** e **stimabile** per la quantità, colonna, quindi fare clic su **Avanti**.  
  
     Selezionando **stimabile**, si indica che si desidera creare previsioni sui dati in questa colonna. Tuttavia, poiché si desidera basare le previsioni sui dati passati, è inoltre necessario aggiungere la colonna come input.  
  
10. Nella pagina **specificare il tipo di dati e il contenuto delle colonne**, rivedere le selezioni.  
  
     La colonna ModelRegion viene designata come colonna **chiave** e la colonna ReportingDate viene automaticamente designata come colonna **chiave temporale** . È consentito un solo tipo per ogni tipo di chiave.  
  
11. Fare clic su **Avanti**.  
  
12. Nella pagina **Completamento procedura guidata** Digitare `Forecasting`per **Nome struttura di data mining**.  
  
    > [!NOTE]  
    >  L'opzione di drill-through non è disponibile per i modelli Time Series.  
  
13. In **nome modello di data mining**Digitare `Forecasting`, quindi fare clic su **fine**.  
  
     Progettazione modelli di data mining viene aperto `Forecasting` per visualizzare la struttura di data mining appena creata.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Modifica della struttura di previsione &#40;esercitazione intermedia sul data mining&#41;](../../2014/tutorials/modifying-the-forecasting-structure-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Progettazione modelli di data mining](../../2014/analysis-services/data-mining/data-mining-designer.md)   
 [Algoritmo Microsoft Time Series](../../2014/analysis-services/data-mining/microsoft-time-series-algorithm.md)  
  
  
