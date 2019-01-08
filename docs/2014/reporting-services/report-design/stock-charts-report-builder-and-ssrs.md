---
title: Grafici azionari (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f75ca11e-b7f5-4ac0-ba17-fe6f82742dad
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 6e7b05abcff2b5f7eae6fabb936447dd37ee6306
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377408"
---
# <a name="stock-charts-report-builder-and-ssrs"></a>Grafici azionari (Generatore report e SSRS)
  I grafici azionari sono progettati appositamente per i dati finanziari o scientifici in cui si usano fino a quattro valori per ogni punto dati. Questi valori si allineano ai valori massimo, minimo, di apertura e di chiusura usati per tracciare dati azionari finanziari. In questo tipo di grafico i valori di apertura o di chiusura vengono visualizzati tramite i marcatori, solitamente linee o triangoli. Nell'esempio seguente i valori di apertura sono rappresentati dai marcatori a sinistra, mentre quelli di chiusura dai marcatori a destra.  
  
 ![Grafico azionario](../media/rs-stockchart.gif "Grafico azionario")  
  
 Un esempio di questo grafico azionario è disponibile come report di Generatore report di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] di esempio. Per altre informazioni sul download di questo e di altri report di esempio, vedere la pagina relativa ai [report di esempio per Generatore report e Progettazione report](https://go.microsoft.com/fwlink/?LinkId=198283) di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="variations"></a>Variazioni  
  
-   **Candela**. Il grafico a candela è un tipo speciale di grafico azionario in cui si usano caselle per indicare l'intervallo tra i valori di apertura e di chiusura. Analogamente al grafico azionario, il grafico a candela consente di visualizzare fino a quattro valori per ogni punto dati.  
  
## <a name="data-considerations-for-stock-charts"></a>Considerazioni sui dati per i grafici azionari  
  
-   Quando si presentano molti punti dati azionari, ad esempio la tendenza annua dei prezzi azionari, risulta difficile distinguere ogni valore di apertura, di chiusura, massimo e minimo di ogni punto dati. In questo scenario è consigliabile usare un grafico a linee anziché un grafico azionario.  
  
-   Quando vengono generate le etichette degli assi, la numerazione inizia solitamente da zero.  In generale, i prezzi azionari non presentano lo stesso grado di fluttuazione di altri set di dati. Per questo motivo, è possibile evitare che le etichette dell'asse inizino da zero, in modo da ottenere una visuale migliore dei dati. A tale scopo, impostare **IncludeZero** su **false** nella finestra di dialogo **Proprietà asse** o nella finestra Proprietà. Per altre informazioni sulla generazione delle etichette dell'asse da parte del grafico, vedere [Formattazione delle etichette degli assi in un grafico &#40;Generatore report e SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md).  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sono disponibili molte formule calcolate da usare con i grafici azionari, tra cui Indicatori prezzo, Indice di forza relativa, MACD e così via.  
  
## <a name="see-also"></a>Vedere anche  
 [Grafici a intervalli &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Formattazione di un grafico &#40;Generatore report e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Finestra di dialogo Proprietà asse, Opzioni asse &#40;Generatore report e SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)  
  
  
