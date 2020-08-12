---
title: Aggiungere un riferimento a un assembly in un report | Microsoft Docs
description: Informazioni su come fornire un riferimento a un assembly in un report in modo che il componente Elaborazione report possa risolvere i nomi in Generatore report.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- code [Reporting Services]
- custom assemblies [Reporting Services], referencing
- custom code [Reporting Services]
- adding assembly references
- assemblies [Reporting Services], references
ms.assetid: 0a03939e-48ce-4c30-b227-98533f2e0ccb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8bbad43a5aa0339ccc13002073facf54de729a58
ms.sourcegitcommit: 02b22274da4a103760a376c4ddf26c4829018454
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/11/2020
ms.locfileid: "84681210"
---
# <a name="add-an-assembly-reference-to-a-report-ssrs"></a>Aggiungere un riferimento a un assembly in un report (SSRS)
  Quando si incorpora codice personalizzato contenente riferimenti alle classi [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] che non sono in <xref:System.Math> o <xref:System.Convert>, è necessario fornire un riferimento all'assembly nel report in modo che il componente Elaborazione report possa risolvere i nomi. Per altre informazioni, vedere [Aggiungere codice a un report &#40;SSRS&#41;](../../reporting-services/report-design/add-code-to-a-report-ssrs.md).  
  
### <a name="to-add-an-assembly-reference-to-a-report"></a>Per aggiungere un riferimento a un assembly in un report  
  
1.  Nella visualizzazione **Progettazione** fare clic con il pulsante destro del mouse nell'area di progettazione all'esterno del bordo del report e scegliere **Proprietà report**.  
  
2.  Fare clic su **Riferimenti**.  
  
3.  In **Aggiungi o rimuovi assembly**fare clic su **Aggiungi** e quindi fare clic sul pulsante con i puntini di sospensione per passare all'assembly.  
  
4.  In **Aggiungi o rimuovi assembly**fare clic su **Aggiungi** e quindi digitare il nome della classe e specificare un nome di istanza da usare nel report.  
  
    > [!NOTE]  
    >  Specificare il nome di una classe e il nome di un'istanza solo per i membri basati sulle istanze. Non specificare membri statici nell'elenco **Classi** . Per altre informazioni, vedere [Riferimenti a codice personalizzato e ad assembly in espressioni in Progettazione report &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)sottostante.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di assembly personalizzati con i report](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Finestra di dialogo Proprietà report, Riferimenti](https://msdn.microsoft.com/library/4639d368-9918-4bb1-9953-7a724ca78dea)  
  
  
