---
title: Aggiungere un misuratore a un report (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 45da4fef-2b02-40e1-977c-f8f80d87155e
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f779bd7cbec18583dcd0c9f30ea8b90750f506ff
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56287929"
---
# <a name="add-a-gauge-to-a-report-report-builder-and-ssrs"></a>Aggiungere un misuratore a un report (Generatore report e SSRS)
  Se si desidera riepilogare i dati in formato visivo, è possibile utilizzare un'area dati Misuratore. Dopo aver aggiunto tale area dati all'area di progettazione, è possibile trascinare i campi del set di dati del report in un riquadro dei dati nel misuratore.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-gauge-to-your-report"></a>Per aggiungere un misuratore al report  
  
1.  Creare un report o aprirne uno esistente.  
  
2.  Nella scheda Inserisci fare doppio clic su misuratore. Verrà visualizzata la finestra di dialogo **Seleziona tipo di misuratore** .  
  
3.  Selezionare il tipo di misuratore da aggiungere. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  A differenza del grafico, il misuratore è solo di due tipi: lineare e radiale. I misuratori disponibili nella finestra di dialogo **Seleziona tipo di misuratore** rappresentano i modelli per questi due tipi di misuratore. Per questo motivo, dopo aver aggiunto il misuratore al report non è possibile modificarne il tipo. Per farlo, è necessario eliminare il misuratore e aggiungerlo di nuovo.  
  
     Se al report non sono associati un'origine dati e un set di dati, viene visualizzata la finestra di dialogo **Proprietà origine dati** che consente di eseguire in modo guidato la procedura per creare entrambi. Per altre informazioni, vedere [aggiungere e verificare una connessione dati o un'origine dati &#40;Generatore Report e SSRS&#41;](../report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
     Se il report ha un'origine dati, ma non un set di dati, viene visualizzata la finestra di dialogo **Proprietà origine dati** in cui sono descritti i passaggi necessari per la creazione. Per altre informazioni, vedere [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](../report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
4.  Fare clic sul misuratore per visualizzare il riquadro dei dati. Per impostazione predefinita, un misuratore dispone di un solo indicatore di misura corrispondente a un unico valore. È tuttavia possibile aggiungere altri indicatori di misura.  
  
5.  Aggiungere un campo del set di dati all'area di rilascio del campo dati. È possibile aggiungere un campo soltanto. Se si desidera visualizzare più campi, è necessario aggiungere indicatori di misura aggiuntivi, uno per ogni campo.  
  
     Fare clic con il pulsante destro del mouse sulla scala del misuratore e scegliere **Proprietà scala**. Digitare un valore per le opzioni **Minimo** e **Massimo** della scala. Per altre informazioni, vedere [Impostare un valore minimo o massimo su un misuratore &#40;Generatore report e SSRS&#41;](set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Aree dati annidate &#40;Generatore report e SSRS&#41;](nested-data-regions-report-builder-and-ssrs.md)   
 [Misuratori &#40;Generatore report e SSRS&#41;](gauges-report-builder-and-ssrs.md)  
  
  
