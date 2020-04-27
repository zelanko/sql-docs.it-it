---
title: Specificare un intervallo dell'asse (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ae46712d-a5bf-44c0-9929-e30ccc1e7e33
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9d862ac509af3936a9f09cadd01667cbe81a679c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66104852"
---
# <a name="specify-an-axis-interval-report-builder-and-ssrs"></a>Specificare un intervallo dell'asse (Generatore report e SSRS)
  L'intervallo dell'asse definisce il numero di etichette e dei segni di graduazione associati su un asse. Sull'asse dei valori gli intervalli forniscono una misura coerente dei punti dati del grafico. Sull'asse delle categorie è tuttavia possibile che tale funzionalità provochi la visualizzazione delle categorie senza etichette. È possibile specificare il numero di intervalli desiderato nella proprietà intervallo dell'asse. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] il numero degli intervalli viene calcolato in fase di esecuzione, in base ai dati nel set di risultati. Per altre informazioni su come vengono calcolati gli intervalli degli assi, vedere [Formattazione delle etichette degli assi in un grafico &#40;Generatore report e SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md).  
  
 Questo argomento non è applicabile per i valori di data o ora sull'asse delle categorie. Per impostazione predefinita, i valori `DateTime` vengono visualizzati come giorni. Per specificare un intervallo di data o ora diverso, ad esempio un mese o un intervallo orario, è necessario formattare le etichette dell'asse e impostare l'asse in modo da visualizzare istanze di tipi `DateTime` anziché di tipi `String`. È inoltre necessario impostare la proprietà intervallo. Per altre informazioni, vedere [Formattazione delle etichette degli assi come date o valute &#40;Generatore report e SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md).  
  
 Questo argomento non è applicabile ai grafici a torta, ad anello, a imbuto o a piramide che non includono assi.  
  
> [!NOTE]  
>  L'asse delle categorie è in genere l'asse orizzontale, ovvero l'asse X. Tuttavia, per i grafici a barre, l'asse delle categorie è l'asse verticale, ovvero l'asse y.  
  
 Un esempio di un grafico che specifica intervalli dell'asse diversi è disponibile come report di esempio. Per altre informazioni sul download di questo e di altri report di esempio, vedere la pagina relativa ai [report di esempio per Generatore report e Progettazione report](https://go.microsoft.com/fwlink/?LinkId=198283) di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-show-all-category-labels-on-the-x-axis"></a>Per visualizzare tutte le etichette delle categorie sull'asse X  
  
1.  Fare clic con il pulsante destro del mouse sull'asse delle categorie, quindi scegliere **Proprietà asse**. Verrà visualizzata la finestra di dialogo **Proprietà asse** .  
  
2.  In **Opzioni asse**impostare `Interval` su **1**. Verranno visualizzate tutte le etichette dei gruppi di categorie. Se si desidera visualizzare tutte le etichette dei gruppi di categorie sull'asse X, digitare **2**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Quando viene impostato un intervallo dell'asse, tutte le funzionalità di assegnazione automatica di etichette vengono disabilitate. Se si specifica un valore per l'intervallo dell'asse, è possibile che si verifichi un comportamento imprevisto delle etichette, a seconda del numero di categorie presenti sull'asse delle categorie.  
  
### <a name="to-enable-a-variable-interval-calculation-on-an-axis"></a>Per abilitare il calcolo di intervalli variabili su un asse  
  
1.  Fare clic con il pulsante destro del mouse sull'asse da modificare, quindi scegliere **Proprietà asse**. Verrà visualizzata la finestra di dialogo **Proprietà asse** .  
  
2.  In **Opzioni asse**impostare `Interval` su **auto**. Il grafico visualizzerà il numero ottimale di etichette di categorie che possono adattarsi lungo l'asse.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedi anche  
 [Formattazione di un grafico &#40;Generatore report e SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Formattazione dei punti dati in un grafico &#40;Generatore report e SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Ordinare i dati in un'area dati &#40;Generatore report e SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Finestra di dialogo Proprietà asse, opzioni asse &#40;Generatore report e SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)   
 [Specificare una scala logaritmica &#40;Generatore report e SSRS&#41;](specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [Traccia di dati su un asse secondario &#40;Generatore report e SSRS&#41;](plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)  
  
  
