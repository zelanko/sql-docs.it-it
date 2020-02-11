---
title: Formattazione delle etichette degli assi come date o valute (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e9a01a74-2f51-4b35-be3a-a6138568f6cf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d328f58da2be026046fc2688a4959b37f5ff7d65
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105876"
---
# <a name="format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs"></a>Formattazione delle etichette degli assi come date o valute (Generatore report e SSRS)
  Quando i valori DateTime sono formattati correttamente su un asse, vengono visualizzati automaticamente in un grafico come giorni. Per specificare un intervallo di data o ora per l'asse X, ad esempio un intervallo di mesi o di ore, è necessario formattare le etichette dell'asse e impostare il tipo di intervallo dell'asse su un intervallo di data o ora valido.  
  
> [!NOTE]  
>  Nei grafici a dispersione e negli istogrammi, l'asse orizzontale, o asse x, è l'asse delle categorie. Nei grafici a barre l'asse delle categorie è l'asse verticale, ovvero l'asse y.  
  
 Per formattare correttamente gli intervalli di tempo, i valori visualizzati sull'asse X devono restituire un tipo di dati <xref:System.DateTime> . Se il campo dispone di un tipo di dati <xref:System.String>, il grafico non calcolerà gli intervalli come date o ore. Per altre informazioni, vedere [Grafici &#40;Generatore report e SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
 Quando un valore numerico viene aggiunto all'asse Y, per impostazione predefinita il grafico non formatta il numero prima di visualizzarlo. Se il campo numerico è una cifra relativa alle vendite, è possibile formattare i numeri come valute per migliorare la leggibilità del grafico.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-format-x-axis-labels-as-monthly-intervals"></a>Per formattare le etichette dell'asse X come intervalli mensili  
  
1.  Fare clic con il pulsante destro del mouse sull'asse orizzontale o asse X, del grafico e scegliere **Proprietà asse orizzontale**.  
  
2.  Nella finestra di dialogo **Proprietà asse orizzontale** selezionare l'opzione **Numero**.  
  
3.  Nell'elenco **Categoria** selezionare **Data**. Nell'elenco **Tipo** selezionare un formato di data da applicare alle etichette dell'asse X.  
  
4.  Selezionare **Opzioni asse**.  
  
5.  In **Intervallo**digitare **1**. Nella proprietà **Tipo intervallo** selezionare **Mesi**.  
  
    > [!NOTE]  
    >  Se non si specifica un tipo di intervallo, il grafico calcolerà gli intervalli in termini di giorni.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-format-y-axis-labels-using-a-currency-format"></a>Per formattare le etichette dell'asse Y utilizzando un formato di valuta  
  
1.  Fare clic con il pulsante destro del mouse sull'asse verticale o asse Y, del grafico e scegliere **Proprietà asse verticale**.  
  
2.  Nella finestra di dialogo **Proprietà asse verticale** selezionare l'opzione **Numero**.  
  
3.  Nell'elenco **Categoria** selezionare **Valuta**. Nell'elenco **Simbolo** selezionare un formato di valuta da applicare alle etichette dell'asse Y.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione delle etichette degli assi in un grafico &#40;Generatore report e SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Formattazione di un grafico &#40;Generatore report e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Specificare una scala logaritmica &#40;Generatore report e SSRS&#41;](specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [Specificare un intervallo dell'asse &#40;Generatore report e SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md)  
  
  
