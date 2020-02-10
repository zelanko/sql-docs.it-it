---
title: 'Attività 3: creazione ed esecuzione di un progetto Data Quality per la corrispondenza | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6260e911-ea8b-4c69-a39d-d1bccd565a32
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ca7c735f00f4fa5c7baf102b26edb6634f57b90f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65489239"
---
# <a name="task-3-creating-and-running-a-data-quality-project-for-matching"></a>Attività 3: Creazione ed esecuzione di un progetto Data Quality per la corrispondenza
  In questa attività viene creato un progetto Data Quality per l'attività di corrispondenza e viene eseguito il processo di corrispondenza nei dati puliti del fornitore per rimuovere tutti i duplicati nei dati.  
  
1.  Nella pagina principale del **client DQS**fare clic su **nuovo progetto Data Quality**.  
  
2.  Digitare **Remove Supplier Duplicates** dal **nome del progetto**.  
  
3.  Selezionare **Suppliers** nell'elenco di KB per il campo **Usa Knowledge base** . Sono stati creati i criteri di corrispondenza in questa Knowledge Base nella lezione precedente.  
  
4.  Selezionare **corrispondente** nell' **elenco di attività** nel riquadro in basso a destra.  
  
     ![Nuovo progetto Data Quality - Corrispondenza selezionata](../../2014/tutorials/media/et-creatingandrunningadqpformatching.jpg "Nuovo progetto Data Quality - Corrispondenza selezionata")  
  
5.  Fare clic su **Avanti**.  
  
6.  Nella pagina **Mappa** selezionare **File di Excel** per **Origine dati**.  
  
7.  Fare clic su **Sfoglia** e selezionare **cleaned Supplier List. xls**, ovvero il file di output dell'attività di pulizia.  
  
8.  Eseguire il mapping della colonna di origine **SupplierID** al dominio **Supplier ID** , della colonna **Supplier** Name al dominio **Supplier Name** e della colonna **ContactEmailAddress** al dominio **Contact email** .  
  
9. Fare clic su **Avanti** per passare alla pagina **corrispondente** .  
  
10. Fare clic su **Avvia** per avviare il processo di corrispondenza. Verranno visualizzati risultati simili a quelli dell'attività precedente poiché è stato utilizzato lo stesso file di input per la definizione dei criteri di corrispondenza.  
  
11. Controllare tutti i record corrispondenti e il punteggio di corrispondenza nella casella di riepilogo. I risultati devono essere uguali a quelli visualizzati nell'attività precedente. Vedere i passaggi dell'attività precedente per analizzare i risultati di questa attività di corrispondenza.  
  
12. Fare clic su **Avanti** per passare alla pagina **Esporta** .  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 4: Esportazione dei risultati dell'attività di corrispondenza in un file di Excel](../../2014/tutorials/task-4-exporting-the-results-from-matching-activity-to-an-excel-file.md)  
  
  
