---
title: 'Attività 11: aggiunta della trasformazione Suddivisione condizionale per filtrare i duplicati | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 3094bd57-5cf4-4860-bf51-fadd1b309f94
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ad925c543cefaf7aed5a0ef355029312b3de7140
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064798"
---
# <a name="task-11-adding-conditional-split-transform-to-filter-duplicates"></a>Attività 11: Aggiunta della trasformazione Suddivisione condizionale a Filtra duplicati
  In questa attività viene aggiunta la trasformazione Suddivisione condizionale al flusso di dati. Tramite questa trasformazione è possibile filtrare i duplicati del set di record in ingresso. Tramite la trasformazione Raggruppamento fuzzy vengono raggruppati i record corrispondenti e uno dei record viene selezionato come record pivot. A tutti i record di un gruppo è assegnato lo stesso valore _key_out. I valori _key_in e _key_out del record pivot nel gruppo sono uguali. Agli altri record del gruppo sono associati valori diversi per _key_in e _key_out. Pertanto, quando si applicano filtri utilizzando la condizione _key_in==_key_out, viene visualizzata solo la riga pivot nel gruppo.  
  
1.  Trascinare la trasformazione **Suddivisione condizionale** dalla sezione **comune** nella **casella degli strumenti SSIS** alla scheda flusso di **dati** .  
  
2.  Fare clic con il pulsante destro del mouse su **trasformazione Suddivisione condizionale** nella scheda **flusso di dati** e quindi scegliere **Rinomina**. Digitare **filtro duplicati** e premere **invio**.  
  
3.  Connettere i **fornitori del gruppo con ID corrispondenti** per **filtrare i duplicati**.  
  
4.  Fare doppio clic su **Filtra duplicati** per avviare la finestra di dialogo **Editor trasformazione Suddivisione condizionale** .  
  
5.  Espandere **colonne** nel riquadro superiore sinistro.  
  
6.  Trascinare **_key_in** nella colonna **condizione** .  
  
7.  Digitare = = (uguale a) accanto a **_key_in** e trascinamento della selezione **_key_out**.  
  
8.  Fare clic su **case 1** nella colonna **Nome output** , digitare **record univoci**e premere **invio**.  
  
     ![Editor trasformazione Suddivisione condizionale](../../2014/tutorials/media/et-addingconditionalsplittransformtofilterduplicates.jpg "Editor trasformazione Suddivisione condizionale")  
  
9. Fare clic su **OK** per chiudere la finestra di dialogo **Editor trasformazione Suddivisione condizionale** .  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 12: Aggiunta della trasformazione Colonna derivata ad Aggiungi colonne richieste da MDS](../../2014/tutorials/task-12-adding-derived-column-transform-to-add-columns-required-by-mds.md)  
  
  
