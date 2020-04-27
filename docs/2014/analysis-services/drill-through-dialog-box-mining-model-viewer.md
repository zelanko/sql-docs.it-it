---
title: Finestra di dialogo Drill-through (Visualizzatore modello di data mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.drillthrough.f1
ms.assetid: 42b78399-143d-4f44-90e0-b545ffb79e10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c065e36dd20646312d04379ea61b96d37a47a262
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081489"
---
# <a name="drill-through-dialog-box-mining-model-viewer"></a>Finestra di dialogo Drill-through (Visualizzatore modello di data mining)
  Quando si visualizza un modello di data mining tramite la scheda **Visualizzatore modello di data mining** di Progettazione modelli di data mining, è possibile eseguire il drill through ai dettagli dei dati del case, purché nel modello sia abilitato il drill-through. Inoltre se nella struttura di data mining sottostante è abilitato il drill-through, è anche possibile visualizzare colonne non incluse nel modello di data mining. Nell'elenco delle colonne, le colonne della struttura sono precedute dall'etichetta "Structure." etichetta.  
  
> [!NOTE]  
>  Non è possibile abilitare il drill-through in una struttura di data mining esistente. È invece necessario ricreare la struttura di data mining e abilitare il drill-through durante il processo di creazione.  
  
 Per informazioni sull'accesso ai dati del case da ogni visualizzatore del modello di data mining che supporta il drill-through, **vedere** [Eseguire il drill-through sui dati del case da un modello di data mining](data-mining/drill-through-to-case-data-from-a-mining-model.md).  
  
## <a name="options"></a>Opzioni  
 **Case classificati in**  
 Viene visualizzata la definizione della regola, del set di elementi e del cluster contenuti nel nodo selezionato.  
  
 **Elenco colonne**  
 Visualizza le colonne contenute nel modello, seguite dalle colonne della struttura.  
  
 **Nota** Le colonne della struttura sono visualizzate solo se nella struttura di data mining è abilitato il drill-through e viene selezionata l'opzione **Colonne struttura e modello**. Per visualizzare le colonne è inoltre necessario disporre delle autorizzazioni drill-through per il modello di data mining e per la struttura di data mining.  
  
 Le colonne della struttura non incluse nel modello vengono visualizzate come **strutture.\< nome della colonna>**.  
  
> [!NOTE]  
>  È possibile fare clic con il pulsante destro del mouse in un punto della griglia di colonne e selezionare **Copia tutto** per copiare negli Appunti i dati drill-through in formato delimitato da tabulazione. Nei dati copiati sono inclusi solo i dati dei case, non la definizione del nodo.  
  
 **Play**  
 Fare clic sul pulsante con la freccia verde per aggiornare i dati.  
  
## <a name="see-also"></a>Vedi anche  
 [Query drill-through &#40;&#41;di data mining](data-mining/drillthrough-queries-data-mining.md)   
 [Visualizzatori modello di data mining &#40;Progettazione modelli di data mining&#41;](mining-model-viewers-data-mining-model-designer.md)   
 [Attività e procedure relative al visualizzatore modello di data mining](data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
  
