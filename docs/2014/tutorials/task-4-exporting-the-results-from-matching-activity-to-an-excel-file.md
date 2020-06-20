---
title: "Attività 4: esportazione dei risultati dall'attività di corrispondenza in un file di Excel | Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 644454c4-3c5a-469a-90ec-e51dc7fb99fc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: fd85a523804232deff14f2e1da5485229f943dd2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "84999663"
---
# <a name="task-4-exporting-the-results-from-matching-activity-to-an-excel-file"></a>Attività 4: Esportazione dei risultati dell'attività di corrispondenza in un file di Excel
  In questa attività vengono esportati i risultati dell'attività di corrispondenza in un file di Excel.

1.  Nella pagina **Esporta** selezionare il **file di Excel** per il **tipo di destinazione**.

2.  Selezionare l'opzione **risultati sopravvivenza** . Nel processo di sopravvivenza, DQS determina un record superstite per ogni cluster in base alla **regola di sopravvivenza** selezionata.

3.  Fare clic su **Sfoglia** e passare alla cartella in cui si desidera archiviare il file di output.

4.  Digitare **Cleansed and matched Suppliers.xls** per il nome e fare clic su **Apri**.

5.  Verificare che il **record pivot** sia selezionato per la **regola di sopravvivenza**. Quando si seleziona questa opzione, come output da un cluster viene selezionato il record pivot per ogni cluster. Di seguito sono riportate le altre opzioni per la regola di sopravvivenza:

    1.  **Record più completo:** Il record superstite è quello con il maggior numero di campi popolati.

    2.  **Record più lungo:** Il record superstite è quello con il maggior numero di termini nei campi di origine.

    3.  Il **record più completo e più lungo:** Il record superstite è quello con il maggior numero di campi popolati e presenta il maggior numero di termini in ogni campo.

     ![Esporta risultati dalla pagina Corrispondenza](../../2014/tutorials/media/et-exportingtheresultsfrommatoanexcelfile.jpg "Esporta risultati dalla pagina Corrispondenza")

6.  Fare clic su **Esporta** per esportare i risultati in un file di Excel.

7.  Fare clic su **Chiudi** per chiudere la finestra di dialogo **esportazione corrispondente** .

8.  Fare clic su **fine** per completare l'attività di corrispondenza.

9. Aprire il file di **Suppliers.xlsxpulito e corrispondente** e verificare che non vengano visualizzati duplicati (SupplierID).

 A questo punto, si dispone di dati fornitore puliti e di cui è stata effettuata la corrispondenza per rimuovere i duplicati.

## <a name="next-step"></a>passaggio successivo
 [Lezione 4: Archiviazione dei dati fornitore in MDS](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)


