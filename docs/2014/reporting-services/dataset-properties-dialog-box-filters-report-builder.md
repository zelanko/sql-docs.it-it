---
title: Finestra di dialogo Proprietà set di dati, filtri (Generatore Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10025"
ms.assetid: 933a6f44-4eb7-4e73-9c40-ac0fd17b23d3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 01d9c5b6ae0e69febd45008bf0aa7b6c3b5a83d4
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109374"
---
# <a name="dataset-properties-dialog-box-filters-report-builder"></a>Finestra di dialogo Proprietà set di dati, Filtri (Generatore report)
  Selezionare **Filtri** nella finestra di dialogo **Proprietà set di dati** per creare filtri per il set di dati.  
  
 I filtri che sono parte di una definizione del set di dati condiviso sul server di report vengono applicati a tutti i report che utilizzano il set di dati condiviso. È possibile specificare filtri aggiuntivi per il set di dati condiviso una volta aggiunto a un report. Questi filtri vengono applicati solo al report nel quale sono definiti.  
  
 I filtri per un set di dati incorporato vengono applicati solo al report nel quale sono definiti.  
  
 Per altre informazioni, vedere [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opzioni  
 **Aggiungi**  
 Consente di aggiungere all'elenco una nuova clausola di filtro.  
  
 **Elimina**  
 Consente di eliminare la clausola di filtro dall'elenco.  
  
 **Freccia in su**  
 Sposta il filtro selezionato di una posizione verso l'alto nell'elenco.  
  
 **Freccia GIÙ**  
 Sposta il filtro selezionato di una posizione verso il basso nell'elenco.  
  
 **Espressione**  
 Digitare o scegliere l'espressione alla quale si desidera applicare un filtro. Fare clic sul pulsante Espressione (**fx**) per modificare l'espressione.  
  
 **Data type**  
 Scegliere il tipo di dati per **Valore**. Se possibile, scegliere un tipo di dati che corrisponda al tipo di dati per **Espressione**.  
  
 I valori specificati in **Espressione** e **Valore** devono restituire lo stesso tipo di dati. Ad esempio, se **Espressione** è impostato su un campo a cui è associato il tipo di dati System.Int32 e **Valore** è impostato su 7, nell'elenco a discesa selezionare **Integer**.  
  
 Se l'opzione relativa al tipo di dati necessario non è presente nell'elenco a discesa, scrivere un'espressione per convertire il valore nel tipo di dati corretto. Per altre informazioni, vedere [Esempi di equazioni di filtro &#40;Generatore report e SSRS&#41;](report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
 **Operatore**  
 Scegliere l'operatore da utilizzare per confrontare l'espressione e il valore.  
  
 **Valore**  
 Digitare l'espressione o il valore da usare durante la valutazione dell'espressione specificata nella casella **Espressione** . Fare clic sul pulsante Espressione (**fx**) per modificare l'espressione.  
  
## <a name="see-also"></a>Vedere anche  
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Parametri report &#40;Generatore report e Progettazione report&#41;](report-design/report-parameters-report-builder-and-report-designer.md)   
 [Aggiungere un filtro a un set di dati &#40;Report e SSRS&#41;](report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)   
 [Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](report-design/expression-uses-in-reports-report-builder-and-ssrs.md)  
  
  
