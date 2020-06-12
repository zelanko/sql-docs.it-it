---
title: Definire le assegnazioni e altri comandi script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- empty scripts [Analysis Services]
- calculations [Analysis Services], scripts
- MDX [Analysis Services], scripts
- scripts [Analysis Services], calculations
ms.assetid: f28b9b22-3dc7-4a45-b4eb-2d023f2c94b8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 184c998bb4bd27d077cca78e792a7e7712f87666
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547053"
---
# <a name="define-assignments-and-other-script-commands"></a>Definire le assegnazioni e altri comandi script
  Per creare uno script vuoto, nella scheda **Calcoli** di Progettazione cubi fare clic sull'icona **Nuovo comando script** sulla barra degli strumenti. Quando si crea un nuovo script, questo viene inizialmente visualizzato con un titolo vuoto nel riquadro **Libreria script** della scheda calcoli. I caratteri digitati nel riquadro Espressioni di calcolo saranno visibili come nome dell'elemento in **Libreria script**. Nella prima riga è pertanto opportuno digitare un nome con commenti, in modo da identificare più agevolmente lo script nel riquadro **Libreria script** . Per altre informazioni, vedere [Introduction to MDX Scripting in Microsoft SQL Server 2005](https://go.microsoft.com/fwlink/?LinkId=81892)(Introduzione alla creazione di script MDX in Microsoft SQL Server 2005). Per ulteriori informazioni sui problemi di prestazioni relativi a query e calcoli MDX, vedere la sezione relativa alla scrittura di espressioni MDX efficienti nella [Guida alle prestazioni SQL Server 2005 Analysis Services](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide).  
  
> [!IMPORTANT]  
>  Quando si passa inizialmente alla scheda **Calcoli** di Progettazione cubi, nel riquadro **Libreria script** è presente un unico script con un comando CALCULATE. Il comando CALCULATE controlla l'aggregazione delle celle del cubo ed è consigliabile modificarlo solo se si desidera specificare manualmente la modalità di aggregazione delle celle del cubo.  
  
 È possibile utilizzare il riquadro Espressioni calcoli per compilare un'espressione nella sintassi MDX (Multidimensional Expression). Durante il processo di compilazione dell'espressione, è possibile trascinare o copiare componenti, funzioni e modelli del cubo dal riquadro **Strumenti di calcolo** nel riquadro Espressioni di calcolo. In questo modo lo script per l'elemento viene aggiunto al riquadro Espressioni di calcolo nella posizione in cui si rilascia o incolla l'elemento. Sostituire gli argomenti e i rispettivi delimitatori (« e ») con i valori appropriati.  
  
> [!IMPORTANT]  
>  Quando si scrive un'espressione contenente più istruzioni utilizzando il riquadro Espressioni di calcolo, verificare che tutte le righe dello script MDX ad eccezione dell'ultima terminino con un punto e virgola (;). I calcoli vengono concatenati in un singolo script MDX e ad ogni script viene aggiunto un punto e virgola in modo da garantire la corretta compilazione dello script MDX. Se si aggiunge un punto e virgola all'ultima riga dello script nel riquadro Espressioni di calcoli, il cubo verrà compilato e distribuito in modo corretto, ma non sarà possibile eseguirvi query.  
  
## <a name="see-also"></a>Vedere anche  
 [Calcoli nei modelli multidimensionali](calculations-in-multidimensional-models.md)  
  
  
