---
title: Aggiungere un misuratore a un report (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 45da4fef-2b02-40e1-977c-f8f80d87155e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9b5c1a9989831e6c28cd2aecd58a3e9f8640465c
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65575014"
---
# <a name="add-a-gauge-to-a-report-report-builder-and-ssrs"></a>Aggiungere un misuratore a un report (Generatore report e SSRS)
  In un report impaginato di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , per riepilogare i dati in formato visivo è possibile usare un'area dati Misuratore. Dopo aver aggiunto tale area dati all'area di progettazione, è possibile trascinare i campi del set di dati del report in un riquadro dei dati nel misuratore.  
  
## <a name="to-add-a-gauge-to-your-report"></a>Per aggiungere un misuratore al report  
  
1.  Creare un report o aprirne uno esistente.  
  
2.  Nella scheda Inserisci fare doppio clic su misuratore. Verrà visualizzata la finestra di dialogo **Seleziona tipo di misuratore** .  
  
3.  Selezionare il tipo di misuratore da aggiungere. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Diversamente dai grafici, esistono solo due tipi di misuratore: lineare e radiale. I misuratori disponibili nella finestra di dialogo **Seleziona tipo di misuratore** rappresentano i modelli per questi due tipi di misuratore. Per questo motivo, dopo aver aggiunto il misuratore al report non è possibile modificarne il tipo. Per farlo, è necessario eliminare il misuratore e aggiungerlo di nuovo.  
  
     Se al report non sono associati un'origine dati e un set di dati, viene visualizzata la finestra di dialogo **Proprietà origine dati** che consente di eseguire in modo guidato la procedura per creare entrambi. Per altre informazioni, vedere [Aggiungere e verificare una connessione dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
     Se il report ha un'origine dati, ma non un set di dati, viene visualizzata la finestra di dialogo **Proprietà origine dati** in cui sono descritti i passaggi necessari per la creazione. Per altre informazioni, vedere [Creare un set di dati condiviso o un set di dati incorporato &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
4.  Fare clic sul misuratore per visualizzare il riquadro dei dati. Per impostazione predefinita, un misuratore dispone di un solo indicatore di misura corrispondente a un unico valore. È tuttavia possibile aggiungere altri indicatori di misura.  
  
5.  Aggiungere un campo del set di dati all'area di rilascio del campo dati. È possibile aggiungere un campo soltanto. Se si desidera visualizzare più campi, è necessario aggiungere indicatori di misura aggiuntivi, uno per ogni campo.  
  
     Fare clic con il pulsante destro del mouse sulla scala del misuratore e scegliere **Proprietà scala**. Digitare un valore per le opzioni **Minimo** e **Massimo** della scala. Per altre informazioni, vedere [Impostare un valore minimo o massimo su un misuratore &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/set-a-minimum-or-maximum-on-a-gauge-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Aree dati annidate &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md)   
 [Misuratori &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md)  
  
  
