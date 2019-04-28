---
title: 'Attività 7: Aggiunta di trasformazione DQS Cleansing al flusso di dati | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0b749c71-dfb6-493a-804f-600290d46eef
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a43ac39754a5f5e83e664a2e21be904c2525bd53
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62866373"
---
# <a name="task-7-adding-dqs-cleansing-transform-to-the-data-flow"></a>Attività 7: Trasformazione Aggiunta DQS Cleansing al flusso di dati
  In questa attività viene aggiunta una trasformazione DQS Cleansing al flusso di dati per pulire i dati di input del fornitore tramite DQS. Visualizzare **[trasformazione DQS Cleansing](https://msdn.microsoft.com/library/ee677619.aspx)** per altri dettagli sulla trasformazione.  
  
1.  Fare doppio clic su **DQS Cleansing** nel **flusso di dati** scheda, quindi scegliere **rinominare**. Tipo di **Pulisci dati fornitore**, quindi premere **invio**.  
  
2.  Selezionare **Leggi dati fornitore dal File di Excel**; trascinare il collegamento blu al **Pulisci dati fornitore**. I componenti sono ora collegati.  
  
     ![Leggi dati fornitore -> Pulisci dati fornitore](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-01.jpg "Leggi dati fornitore -> Pulisci dati fornitore")  
  
3.  Fare doppio clic su **Pulisci dati fornitore**.  
  
4.  Nel **Editor trasformazione DQS Cleansing**, fare clic su **New** accanto al **gestione connessione Data Quality riepilogo**.  
  
5.  Nel **gestione connessione DQS Cleansing** finestra di dialogo, digitare **(locale)** oppure **periodo** (.) per connettersi al server locale. In questa lezione si presuppone che in un server locale sia installato DQS.  
  
6.  Fare clic su **Test connessione** per testare la connessione al server DQS.  
  
7.  Scegliere **OK** per chiudere la finestra di dialogo.  
  
8.  Selezionare **Suppliers** per il **Data Quality Knowledge Base**.  
  
     ![Editor di trasformazione - KB fornitori DQS Cleansing](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-02.jpg "Editor di trasformazione - KB fornitori DQS Cleansing")  
  
9. Passare al **Mapping** scheda nella parte superiore.  
  
10. Dal **colonne di Input disponibili**, selezionare **Supplier Name**, **ContactEmailAddress**, **Address Line**, **Città**, **Stato**, **paese**, e **CAP** selezionando le caselle di controllo.  
  
     ![Editor di trasformazione - mapping di DQS Cleansing](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-03.jpg "Editor di trasformazione - mapping di DQS Cleansing")  
  
11. Nel riquadro inferiore, eseguire il mapping di queste colonne usando elenchi a discesa nel **dominio** colonna:  
  
    |colonna|Dominio|  
    |------------|------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|Contact Email|  
    |Riga indirizzo|Riga indirizzo|  
    |Città|Città|  
    |State|State|  
    |Country|Country|  
    |Zip Code|CAP|  
  
12. Fare clic su **OK** per chiudere la **Editor trasformazione DQS Cleansing** nella finestra di dialogo.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 8: Aggiunta della trasformazione Suddivisione condizionale per l'Output di pulizia della suddivisione](../../2014/tutorials/task-8-adding-conditional-split-transform-to-split-cleansing-output.md)  
  
  
