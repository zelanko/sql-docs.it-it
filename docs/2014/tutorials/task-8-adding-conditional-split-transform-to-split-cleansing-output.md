---
title: "Attività 8: Aggiunta di Conditional Split trasformazione per suddividere l'Output di pulizia | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d4ebe420-a4a9-4076-89d3-41abe726fc5c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d5a55f0694094e6fe88a42946bcff34f420210f4
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65489675"
---
# <a name="task-8-adding-conditional-split-transform-to-split-cleansing-output"></a>Attività 8: Aggiunta della trasformazione Suddivisione condizionale all'output di pulizia della suddivisione
  In questa trasformazione viene aggiunta la trasformazione Suddivisione condizionale al flusso di dati. La trasformazione Suddivisione condizionale consente di indirizzare le righe verso output diversi in base al contenuto dei dati. Per questa esercitazione, si utilizza il **stato Record** colonna di output dalla trasformazione DQS Cleansing. In questa esercitazione verranno caricati solo i record corretti o con correzione nel server MDS. Pertanto, controllare se il **stato Record** viene **correggere** oppure **con correzione**e combinare i record prima di caricarli in MDS.  
  
1.  Trascinare **trasformazione Suddivisione condizionale** dalla **comuni** sezione la **casella degli strumenti SSIS** per il **del flusso di dati** scheda in **Pulisci dati fornitore**.  
  
2.  Fare doppio clic su **suddivisione condizionale**, fare clic su **rinominare**. Tipo di **Seleziona record corretti e** , quindi premere **invio**.  
  
3.  Connettere **Pulisci dati fornitore** e **Seleziona record corretti e** usando il collegamento blu.  
  
     ![CLEANSE Supplier Data -> scegliere corretti con correzione](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-01.jpg "Cleanse Supplier Data -> scegliere corretti con correzione")  
  
4.  Fare doppio clic su **Seleziona record corretti e** nel **flusso di dati** scheda.  
  
5.  Modifica il **nome Output predefinito** nella parte inferiore della schermata per **correggere**.  
  
6.  Espandere **colonne** nel **riquadro superiore sinistro**.  
  
     ![Editor trasformazione Suddivisione condizionale](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-02.jpg "Editor trasformazione Suddivisione condizionale")  
  
7.  Funzionalità di trascinamento **stato Record** per il **condizione** colonna.  
  
8.  Tipo di **= = "Corrected"** accanto a **[Record Status]** per il **condizione** colonna.  
  
9. Fare clic su **caso 1** nel **colonna nome Output**e denominarlo **con correzione**.  
  
10. Fare clic su **OK** per chiudere la **Editor trasformazione Suddivisione condizionale** nella finestra di dialogo.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 9: Aggiunta della Union trasformazione multipli a combina record corretti e con correzione](../../2014/tutorials/task-9-adding-union-all-transform-to-combine-correct-and-corrected-records.md)  
  
  
