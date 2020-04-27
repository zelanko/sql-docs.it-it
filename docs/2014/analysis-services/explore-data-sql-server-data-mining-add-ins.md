---
title: Esplorazione dei dati (SQL Server componenti aggiuntivi Data mining) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data preparation
- histogram [data mining]
- data visualization
ms.assetid: 714845a9-4c27-461a-9ba3-149e1e818386
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0bad2a2e65a65bbafa8218a3e0afbedd4b9f13b6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081312"
---
# <a name="explore-data-sql-server-data-mining-add-ins"></a>Esplorazione dati (componenti aggiuntivi Data mining di SQL Server)
  ![Procedura guidata Esplorazione dati](media/dmc-explore.gif "Procedura guidata Esplorazione dati")  
  
 La procedura guidata **Esplora dati** consente di comprendere il tipo e la quantità di dati nella tabella dati. La procedura guidata consente di creare un grafico della distribuzione e dei valori delle colonne selezionate, una alla volta. È quindi possibile provare a modificare il modo in cui i dati vengono raggruppati o copiare il grafico del contenuto in una cartella di lavoro di Excel per esaminarlo.  
  
 Se nei dati sono contenuti dati numerici continui, è possibile passare tra queste due viste:  
  
-   **Grafico a linee.** Questo grafico a linee riporta i valori dei dati sull'asse X e il numero di case sull'asse Y.  
  
-   **Grafico a barre.** Questo grafico a barre raggruppa i valori in base al numero di case per ogni valore.  
  
 Quando tramite la procedura guidata vengono trovati gruppi nei dati, si utilizza la distribuzione effettiva dei valori dei dati. Pertanto, il grafico a barre non visualizza i valori numerici in base a indicatori numerici tipici dell'asse costituiti da numeri interi, ad esempio 10 o 100. Gli intervalli visualizzati nel grafico a barre possono invece essere simili al seguente: 43521-55603 (per la colonna Income).  
  
 Se si desidera raggruppare i dati in altri intervalli, è necessario eseguire questa operazione in Excel prima di analizzare i dati. In alternativa, è possibile rietichettare i dati tramite la procedura guidata modifica [etichette](relabel-sql-server-data-mining-add-ins.md) .  
  
## <a name="using-the-explore-data-wizard"></a>Utilizzo della procedura guidata Esplorazione dati  
  
1.  Sulla barra multifunzione **data mining** fare clic su **Esplora dati**.  
  
2.  Nella finestra di dialogo **Seleziona origine** selezionare la tabella o l'intervallo di celle contenente i dati.  
  
3.  Nella finestra di dialogo **Seleziona colonna** scegliere la colonna da analizzare, dai dati di esempio visualizzati nel riquadro.  
  
4.  Nella finestra di dialogo **Esplora dati** scegliere i tipi di grafico per la visualizzazione della distribuzione dei dati.  
  
5.  È possibile aggiungere nuove colonne ai dati, cambiare il modo in cui i dati sono segmentati o copiare il grafico in Excel.  
  
### <a name="requirements"></a>Requisiti  
 Per utilizzare la procedura guidata **esplorazione dati** , è necessario che i dati si trovino in una tabella dati di Excel.   
  
## <a name="see-also"></a>Vedi anche  
 [Elenco di controllo per la preparazione di data mining](checklist-of-preparation-for-data-mining.md)  
  
  
