---
title: Impostazione conteggi oggetti (Progettazione guidata aggregazioni) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 7d616997d3764aad42691d9ef3c213d553b5f311
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66068312"
---
# <a name="specify-object-counts-aggregation-design-wizard"></a>Impostazione conteggi oggetti (Progettazione guidata aggregazioni)
  Utilizzare la pagina **Impostazione conteggi oggetti** per eseguire automaticamente il conteggio degli oggetti nel cubo o per digitare manualmente conteggi stimati. La Progettazione guidata aggregazioni utilizza i conteggi degli oggetti per stimare i requisiti di archiviazione.  
  
## <a name="options"></a>Opzioni  
 **Oggetti Cube**  
 Consente di valutare le dimensioni e gli attributi nel cubo. Solo gli attributi che non hanno loro `AggregationUsage` proprietà impostata su `None` nel **controlla utilizzo aggregazioni** pagina della procedura guidata vengono visualizzati, perché questi sono gli unici attributi che è possibile specificare i conteggi.  
  
 **Conteggio stimato**  
 Viene visualizzato il numero stimato di righe nel gruppo di misure e il numero di membri di attributi stimato nelle dimensioni del database. È possibile digitare un valore da utilizzare come conteggio stimato o è possibile calcolare i totali stimati. Per calcolare il totale, digitare `0` nel campo e quindi fare clic su **conteggio**. I campi che presentano già un conteggio non vengono aggiornati.  
  
 **Numero di partizioni**  
 (Facoltativo) Digitare il numero stimato di righe nel gruppo di misure e il numero di membri di attributi stimato nelle dimensioni del database.  
  
 **Count**  
 Consente di calcolare e di ripopolare i valori nella colonna **Conteggio stimato** per tutti i campi vuoti. I campi che presentano già un conteggio non vengono aggiornati.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida F1 guidata di progettazione delle aggregazioni](aggregation-design-wizard-f1-help.md)   
 [Procedure guidate di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
