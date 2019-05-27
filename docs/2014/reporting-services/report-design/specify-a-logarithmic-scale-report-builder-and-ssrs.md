---
title: Specificare una scala logaritmica (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f3092c1c-b128-433d-9a95-983508b2a8d4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0910888603528d899f0180bf96c66cfbea045aa4
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66104940"
---
# <a name="specify-a-logarithmic-scale-report-builder-and-ssrs"></a>Specificare una scala logaritmica (Generatore report e SSRS)
  Se i dati sono proporzionali in modo logaritmico, è opportuno utilizzare nel grafico una scala logaritmica per migliorare l'aspetto del grafico e agevolare la gestione dei dati. Con la maggior parte delle scale logaritmiche viene utilizzata la base 10.  
  
 Questa caratteristica è disponibile solo sull'asse dei valori. L'asse dei valori è in genere l'asse verticale, ovvero l'asse Y. Sui grafici a barre, tuttavia, è l'asse orizzontale, ovvero l'asse x.  
  
 Se l'asse è logaritmico, tutte le altre proprietà correlate all'asse verranno scalate in modo logaritmico. Se ad esempio si specifica una scala logaritmica in base 10 sull'asse e si imposta per l'asse un intervallo di 2, verranno generati intervalli con ordine di grandezza pari a 10 alla potenza di 2 o 100. Ciò significa che i valori dell'asse indicheranno 1, 100, 10000, anziché il risultato predefinito 1, 10, 100, 1000, 10000.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-a-logarithmic-scale"></a>Per specificare una scala logaritmica  
  
1.  Fare clic con il pulsante destro del mouse sull'asse Y del grafico e scegliere **Proprietà asse verticale**. Viene visualizzata la finestra di dialogo **Proprietà asse verticale** .  
  
2.  In **Opzioni asse**selezionare **Usa scala logaritmica**.  
  
3.  Nella casella di testo **Base logaritmo** digitare un valore positivo per la base logaritmica. Se non si specifica alcun valore, il valore predefinito della base logaritmica sarà 10.  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione delle etichette degli assi in un grafico &#40;Generatore report e SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Formattazione di un grafico &#40;Generatore report e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Formattazione delle etichette degli assi come date o valute &#40;Generatore report e SSRSSSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
