---
title: Esplorazione del cubo | Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: da01dbb0f8e67d885382a3fa125a0fb37596d553
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2019
ms.locfileid: "65403973"
---
# <a name="lesson-2-6---browsing-the-cube"></a>Lezione 2-6: esplorazione del cubo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Dopo aver distribuito un cubo, è possibile visualizzarne i dati nella scheda **Esplorazione** di Progettazione cubi, mentre i dati della dimensione possono essere visualizzati nella scheda **Esplorazione** di Progettazione dimensioni. L'esplorazione dei dati del cubo e delle dimensioni consente di controllare il lavoro in modo incrementale. È possibile verificare che le piccole modifiche a proprietà, relazioni e altri oggetti abbiano l'effetto desiderato dopo l'elaborazione dell'oggetto. Sebbene la scheda Esplorazione venga utilizzata per visualizzare sia i dati del cubo che quelli delle dimensioni, le funzionalità da essa fornite variano a seconda dell'oggetto visualizzato.  
  
Per le dimensioni la scheda Esplorazione consente di visualizzare i membri o di spostarsi nella gerarchia fino al nodo foglia. È possibile esplorare i dati della dimensione in diverse lingue, a condizione che siano state aggiunte le traduzioni al modello.  
  
Per i cubi la scheda Esplorazione fornisce due approcci per l'esplorazione dei dati. È possibile utilizzare la progettazione query MDX incorporata per compilare query che restituiscono un set di righe bidimensionale da un database multidimensionale. In alternativa, è possibile utilizzare un collegamento Excel. Quando si avvia Excel dall'interno di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], Excel viene aperto con una tabella pivot già presente nel foglio di lavoro e una connessione predefinita al database dell'area di lavoro del modello.  
  
Excel offre in genere un'esperienza di esplorazione migliore poiché è possibile esplorare i dati del cubo in modo interattivo, utilizzando gli assi orizzontale e verticale per analizzare le relazioni nei dati. Al contrario, la progettazione query MDX è limitata a un solo asse. Inoltre, poiché il set di righe è bidimensionale, non si ottiene il drill-down fornito da una tabella pivot di Excel. Man mano che si aggiungono più dimensioni e gerarchie al cubo, operazione che verrà eseguita nelle lezioni successive, Excel sarà la soluzione preferita per l'esplorazione dei dati.  
  
### <a name="to-browse-the-deployed-cube"></a>Per esplorare il cubo distribuito  
  
1.  Passare a **Progettazione dimensioni** per la dimensione Product in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. A tale scopo, fare doppio clic sulla dimensione **Product** nel nodo **Dimensioni** di Esplora soluzioni.  
  
2.  Fare clic sulla scheda **Esplorazione** per visualizzare il membro **Tutto** della gerarchia dell'attributo **Product Key** . Nella lezione 3 verrà definita una gerarchia utente per la dimensione Product che consentirà di esplorare la dimensione.  
  
3.  Passare a **Progettazione cubi** in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. A tale scopo, fare doppio clic sul cubo **Analysis Services Tutorial** nel nodo **Cubi** di Esplora soluzioni.  
  
4.  Selezionare la scheda **Esplorazione** e fare clic sull'icona **Riconnetti** sulla barra degli strumenti della finestra di progettazione.  
  
    Nel riquadro sinistro della finestra di progettazione vengono visualizzati gli oggetti del cubo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Tutorial. A destra della scheda **Esplorazione** sono disponibili due riquadri: quello superiore è il riquadro **Filtro** , mentre quello inferiore è il riquadro **Dati** . In una lezione successiva si utilizzerà il visualizzatore cubi per eseguire analisi.  
  
## <a name="next-lesson"></a>Lezione successiva  
[Lezione 3: Modifica le misure, attributi e gerarchie](lesson-3-modifying-measures-attributes-and-hierarchies.md)  
  
## <a name="see-also"></a>Vedere anche  
[Editor di query MDX &#40;Analysis Services - Dati multidimensionali&#41;](http://msdn.microsoft.com/library/777f2c23-1c1c-4b72-9d19-48a4866551f8)  
  
  
  
