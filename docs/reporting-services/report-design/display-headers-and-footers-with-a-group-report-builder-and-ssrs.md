---
title: Visualizzare intestazioni e piè di pagina con un gruppo (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 8eb7d648-4df2-491a-96cb-99e55629d617
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a9033e39b58e70131ca7c361f89cebed9f12c1d0
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65580853"
---
# <a name="display-headers-and-footers-with-a-group-report-builder-and-ssrs"></a>Visualizzare intestazioni e piè di pagina con un gruppo (Generatore report e SSRS)
  È possibile stabilire se di una riga statica, ad esempio l'intestazione o il piè di pagina di un gruppo, viene eseguito il rendering con righe dinamiche associate a un gruppo in un'area dati Tablix.  
  
 Per ripetere tutte le intestazioni di colonna o di riga su più pagine, è possibile impostare proprietà per l'area dati Tablix. Per altre informazioni, vedere [Visualizzazione delle intestazioni di riga e colonna in più pagine Generatore report e SSRS](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md).  
  
 Per controllare il comportamento di rendering per righe e colonne dinamiche associate a gruppi nidificati oppure per righe e colonne statiche associate a etichette o subtotali, è necessario impostare proprietà per il membro Tablix. Un membro Tablix rappresenta una riga o una colonna statica o dinamica. Un membro statico si ripete una sola volta. Ad esempio, la riga di un totale complessivo è una riga statica. Un membro dinamico si ripete una sola volta per ogni istanza di un gruppo. Ad esempio, una riga associata a un gruppo che include l'espressione di raggruppamento [Territory] si ripete una sola volta per ogni valore univoco relativo al territorio. Per altre informazioni sui membri Tablix, vedere [Celle, righe e colonne dell'area dati Tablix &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
 È possibile selezionare un membro Tablix nel riquadro di raggruppamento e impostare le proprietà **KeepWithGroup**, **KeepTogether**e **RepeatOnNewPage** nel riquadro Proprietà. Usare **KeepWithGroup** per visualizzare intestazioni e piè di pagina di gruppo nella stessa pagina del gruppo. Usa **KeepTogether** per visualizzare membri statici con le righe o colonne di un gruppo. Usare **RepeatOnNewPage** per ripetere l'intestazione di gruppo o il piè di pagina in ogni pagina che visualizza almeno un'istanza completa del membro del gruppo di righe definito dal valore **KeepWithGroup** . La proprietà**RepeatOnNewPage** non è supportata per i membri del gruppo di colonne.  
  
> [!NOTE]  
>  **KeepWithGroup**, **KeepTogether** e **RepeatOnNewPage** sono proprietà dei membri del gruppo che è possibile impostare usando l'opzione **Modalità avanzata** del riquadro di raggruppamento. Per altre informazioni, vedere [Riquadro di raggruppamento &#40;Generatore report&#41;](../../reporting-services/report-design/grouping-pane-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-a-static-row-with-a-set-of-dynamic-rows-associated-with-a-row-group"></a>Per mantenere una riga statica con un set di righe dinamiche associato a un gruppo di righe  
  
1.  Nell'area di progettazione fare clic in un punto qualsiasi nell'area dati Tablix per selezionarla. Nel riquadro di raggruppamento verranno visualizzati i gruppi di righe e di colonne per l'area dati.  
  
2.  Sul lato destro del riquadro di raggruppamento fare clic sulla freccia rivolta verso il basso, quindi fare clic su **Modalità avanzata**. Nel riquadro Gruppi di righe verranno visualizzati i membri statici e dinamici gerarchici della gerarchia dei gruppi di righe.  
  
3.  Fare clic sul membro statico che corrisponde all'intestazione o al piè di pagina della riga che si desidera mantenere con le righe di gruppo. Nel riquadro Proprietà verranno visualizzate le proprietà dei **membri Tablix** .  
  
4.  Nel riquadro Proprietà fare clic su **KeepWithGroup**e quindi scegliere uno dei valori seguenti nell'elenco a discesa:  
  
    -   **Nessuno** Selezionare questa opzione per non indicare preferenze relative al mantenimento del membro con i membri del gruppo di righe selezionato.  
  
    -   **Prima** Selezionare questa opzione per mantenere il membro con i membri del gruppo precedente. È possibile utilizzare questa opzione per le righe di piè di pagina del gruppo.  
  
    -   **Dopo** Selezionare questa opzione per mantenere il membro con i membri del gruppo successivo. È possibile utilizzare questa opzione per le righe di intestazione del gruppo.  
  
5.  (Facoltativo) Visualizzare l'anteprima del report. Se possibile, il renderer del report mantiene il membro con i membri del gruppo di righe specificato.  
  
### <a name="to-keep-a-static-column-with-a-set-of-dynamic-columns-associated-with-a-column-group"></a>Per mantenere una colonna statica con un set di colonne dinamiche associato a un gruppo di colonne  
  
1.  Nell'area di progettazione fare clic in un punto qualsiasi nell'area dati Tablix per selezionarla. Nel riquadro di raggruppamento verranno visualizzati i gruppi di righe e di colonne per l'area dati.  
  
2.  Sul lato destro del riquadro di raggruppamento fare clic sulla freccia rivolta verso il basso, quindi fare clic su **Modalità avanzata**. Nel riquadro Gruppi di colonne verranno visualizzati i membri statici e dinamici gerarchici della gerarchia dei gruppi di colonne.  
  
3.  Fare clic sul membro statico che corrisponde alla colonna statica che si desidera mantenere con le colonne di gruppo. Nel riquadro Proprietà verranno visualizzate le proprietà dei **membri Tablix** .  
  
4.  Nel riquadro Proprietà fare clic su **KeepWithGroup**e quindi scegliere uno dei valori seguenti nell'elenco a discesa:  
  
    -   **Nessuno** Selezionare questa opzione per non indicare preferenze relative al mantenimento del membro con i membri del gruppo di colonne selezionato.  
  
    -   **Prima** Selezionare questa opzione per mantenere il membro con i membri del gruppo precedente. È possibile utilizzare questa opzione per le etichette di colonna che vengono visualizzate prima dei membri del gruppo di colonne specificati.  
  
    -   **Dopo** Selezionare questa opzione per mantenere il membro con i membri del gruppo successivo. È possibile utilizzare questa opzione per i totali delle colonne che vengono visualizzati dopo i membri del gruppo di colonne specificati.  
  
5.  (Facoltativo) Visualizzare l'anteprima del report. Laddove possibile, il renderer del report mantiene il membro con i membri del gruppo di colonne specificati.  
  
## <a name="see-also"></a>Vedere anche  
 [Celle, righe e colonne dell'area dati Tablix (Generatore report e SSRS)](tablix-data-region-report-builder-and-ssrs.md)   
 
  
  
