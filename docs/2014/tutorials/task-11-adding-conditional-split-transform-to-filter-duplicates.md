---
title: 'Attività 11: Aggiunta Conditional Split trasformazione per filtrare i duplicati | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 71b050e49440764d355d4658607600c135741f50
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65476746"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>Attività 11: Aggiunta della trasformazione Suddivisione condizionale a Filtra duplicati
  In questa attività viene aggiunta la trasformazione Suddivisione condizionale al flusso di dati. Tramite questa trasformazione è possibile filtrare i duplicati del set di record in ingresso. Tramite la trasformazione Raggruppamento fuzzy vengono raggruppati i record corrispondenti e uno dei record viene selezionato come record pivot. A tutti i record di un gruppo è assegnato lo stesso valore _key_out. I valori _key_in e _key_out del record pivot nel gruppo sono uguali. Agli altri record del gruppo sono associati valori diversi per _key_in e _key_out. Pertanto, quando si applicano filtri utilizzando la condizione _key_in==_key_out, viene visualizzata solo la riga pivot nel gruppo.  
  
1.  Funzionalità di trascinamento **suddivisione condizionale** trasformare dalla **comuni** sezione la **casella degli strumenti SSIS** per il **del flusso di dati** scheda.  
  
2.  Fare doppio clic su **trasformazione Suddivisione condizionale** nel **flusso di dati** scheda, quindi scegliere **rinominare**. Tipo di **Filtra duplicati** , quindi premere **invio**.  
  
3.  Connettere **raggruppare fornitori con ID corrispondenti** al **Filtra duplicati**.  
  
4.  Fare doppio clic su **Filtra duplicati** per avviare la **Editor trasformazione Suddivisione condizionale** nella finestra di dialogo.  
  
5.  Espandere **colonne** nel riquadro superiore sinistro.  
  
6.  Funzionalità di trascinamento **key_in** per il **condizione** colonna.  
  
7.  Tipo = = (uguale a) accanto a **key_in** e trascinare **key_out**.  
  
8.  Fare clic su **caso 1** nel **nome Output** colonna, digitare **record univoci**, premere **invio**.  
  
     ![Editor trasformazione Suddivisione condizionale](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "Editor trasformazione Suddivisione condizionale")  
  
9. Fare clic su **OK** per chiudere la **Editor trasformazione Suddivisione condizionale** nella finestra di dialogo.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 12: Aggiunta di trasformazione colonna derivata ad Aggiungi colonne richieste da MDS](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  
