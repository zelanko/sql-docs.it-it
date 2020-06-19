---
title: Impostazione conteggi oggetti (progettazione guidata aggregazioni) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.storagedesignwizard.calculatingobjectcounts.f1
ms.assetid: 305d9d79-d1ab-4704-a7b5-3283842b3996
author: minewiskan
ms.author: owend
ms.openlocfilehash: c66b972395f86746b2d08df234db8aa0c71d03fd
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940322"
---
# <a name="specify-object-counts-aggregation-design-wizard"></a>Impostazione conteggi oggetti (Progettazione guidata aggregazioni)
  Utilizzare la pagina **Impostazione conteggi oggetti** per eseguire automaticamente il conteggio degli oggetti nel cubo o per digitare manualmente conteggi stimati. La Progettazione guidata aggregazioni utilizza i conteggi degli oggetti per stimare i requisiti di archiviazione.  
  
## <a name="options"></a>Opzioni  
 **Oggetti cubo**  
 Consente di valutare le dimensioni e gli attributi nel cubo. Vengono visualizzati solo gli attributi che non hanno la `AggregationUsage` proprietà impostata su `None` nella pagina **verifica utilizzo aggregazioni** della procedura guidata, perché questi sono gli unici attributi che richiedono la specifica dei conteggi.  
  
 **Conteggio stimato**  
 Viene visualizzato il numero stimato di righe nel gruppo di misure e il numero di membri di attributi stimato nelle dimensioni del database. È possibile digitare un valore da utilizzare come conteggio stimato o è possibile calcolare i totali stimati. Per calcolare i valori di conteggio, digitare `0` nel campo e quindi fare clic su **conteggio**. I campi che presentano già un conteggio non vengono aggiornati.  
  
 **Numero di partizioni**  
 (Facoltativo) Digitare il numero stimato di righe nel gruppo di misure e il numero di membri di attributi stimato nelle dimensioni del database.  
  
 **Numero**  
 Consente di calcolare e di ripopolare i valori nella colonna **Conteggio stimato** per tutti i campi vuoti. I campi che presentano già un conteggio non vengono aggiornati.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto della progettazione guidata aggregazioni](aggregation-design-wizard-f1-help.md)   
 [Procedure guidate di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
