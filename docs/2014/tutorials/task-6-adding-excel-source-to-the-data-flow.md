---
title: "Attività 6: aggiunta dell'origine Excel al flusso di dati | Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0209055e-cb6b-4a07-909e-836596727a2c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: eff79fb144c2bbc4d31a21b2dc263c4ccb087104
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177239"
---
# <a name="task-6-adding-excel-source-to-the-data-flow"></a>Attività 6: Aggiunta dell'origine Excel al flusso di dati
  In questa attività viene aggiunta un'origine Excel al flusso di dati per leggere i dati del fornitore dal file di Excel di origine. Tramite l'origine Excel vengono estratti dati da fogli di lavoro o intervalli in cartelle di lavoro di Microsoft Excel. Per ulteriori informazioni, vedere l'argomento [origine Excel](../integration-services/data-flow/excel-source.md) .

1.  Trascinare **origine Excel** da **altre origini** nella **casella degli strumenti SSIS** alla scheda **flusso di dati** .

2.  Fare clic con il pulsante destro del mouse su **origine Excel** nella scheda **flusso di dati** e quindi scegliere **Rinomina**.

3.  Digitare **Leggi dati fornitore dal file di Excel** e premere **invio**.

4.  Fare doppio clic su **Leggi dati fornitore dal file di Excel** per aprire la finestra di dialogo **Editor origine Excel** .

5.  Nella finestra di dialogo **Editor origine Excel** fare clic su **nuovo** per creare una connessione Excel.

6.  Nella finestra di dialogo **gestione connessione Excel** fare clic su **Sfoglia**, quindi selezionare il file **Suppliers. xls** nella cartella **EIM tutorial** . Verificare che **Microsoft excel 97-2003** sia selezionato nella casella **versione di Excel** , quindi fare clic su **OK**.

     ![Finestra di dialogo Gestione connessioni di Excel](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-01.jpg "Finestra di dialogo Gestione connessioni di Excel")

7.  Nella finestra di dialogo **Editor origine Excel** selezionare **IncomingSuppliers $** nella casella **di riepilogo nome del foglio di Excel** .

     ![Nome del foglio di Excel - Fornitori$ in entrata](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-02.jpg "Nome del foglio di Excel - Fornitori$ in entrata")

8.  Fare clic su **Anteprima** per visualizzare in anteprima i dati nel file di Excel.

9. Scegliere **OK** per chiudere la finestra di dialogo.

10. Trascinare la trasformazione **pulizia DQS** in **altre trasformazioni** nella **casella degli strumenti SSIS** nella scheda **flusso di dati** in **Leggi dati fornitore dal file di Excel**. Nella trasformazione DQS Cleansing viene utilizzato Data Quality Services (DQS) per correggere i dati applicando le regole approvate nella Knowledge Base. In fase di esecuzione, tramite questa trasformazione viene creato un progetto DQS Cleansing nel server DQS. Per ulteriori informazioni, vedere l'argomento [trasformazione della pulizia DQS](https://msdn.microsoft.com/library/ee677619.aspx) .

## <a name="next-step"></a>passaggio successivo

[Attività 7: Aggiunta della trasformazione DQS Cleansing al flusso di dati](task-7-adding-dqs-cleansing-transform-to-the-data-flow.md)

### <a name="see-also"></a>Vedere anche

[Flusso di dati](../integration-services/data-flow/data-flow.md)
