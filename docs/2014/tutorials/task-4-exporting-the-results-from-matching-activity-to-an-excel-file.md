---
title: "Attività 4: Esportazione dei risultati dell'attività di corrispondenza in un File di Excel | Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 644454c4-3c5a-469a-90ec-e51dc7fb99fc
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c9424f2ba21fb4b93e359c8662974a82c62b4895
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020442"
---
# <a name="task-4-exporting-the-results-from-matching-activity-to-an-excel-file"></a>Attività 4: Esportazione dei risultati dell'attività di corrispondenza in un file di Excel
  In questa attività vengono esportati i risultati dell'attività di corrispondenza in un file di Excel.  
  
1.  Nel **esportare** pagina, selezionare **File di Excel** per il **tipo di destinazione**.  
  
2.  Selezionare **risultati sopravvivenza** opzione. Nel processo di sopravvivenza, DQS viene determinato un record superstite per ogni cluster basato sul **regola di sopravvivenza** è stato selezionato.  
  
3.  Fare clic su **esplorare** e passare alla cartella in cui si desidera archiviare il file di output.  
  
4.  Tipo di **Cleansed and Matched Suppliers. xls** per il nome e fare clic su **Open**.  
  
5.  Verificare che **Record Pivot** sia selezionata per il **regola di sopravvivenza**. Quando si seleziona questa opzione, come output da un cluster viene selezionato il record pivot per ogni cluster. Di seguito sono riportate le altre opzioni per la regola di sopravvivenza:  
  
    1.  **Record più completo:** il record superstite è quello con il maggior numero di campi popolati.  
  
    2.  **Record più lungo:** il record superstite è quello con il maggior numero di termini nei campi di origine.  
  
    3.  **Record più completo e più lungo:** il record superstite è quello con il maggior numero di campi popolati e di termini in ogni campo.  
  
     ![Esportare i risultati dalla pagina corrispondenza](../../2014/tutorials/media/et-exportingtheresultsfrommatoanexcelfile.jpg "esportare i risultati dalla pagina corrispondenza")  
  
6.  Fare clic su **esportare** per esportare i risultati in un file di Excel.  
  
7.  Fare clic su **chiudere** per chiudere la **esportazione corrispondenze** nella finestra di dialogo.  
  
8.  Fare clic su **fine** per completare l'attività di corrispondenza.  
  
9. Aprire il **Cleansed and Matched Suppliers. xlsx** file e verificare che non viene visualizzato alcun duplicato (SupplierID).  
  
 A questo punto, si dispone di dati fornitore puliti e di cui è stata effettuata la corrispondenza per rimuovere i duplicati.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Lezione 4: Archiviazione dei dati fornitore in MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)  
  
  
