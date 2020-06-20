---
title: 'Attività 13: aggiunta della destinazione OLE DB per la scrittura dei dati nella tabella di staging MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e6c67fa9-bb52-44a9-82f6-d86551cf12b2
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: bb39e9d50d135adfedcf307cda2ad703e302eda5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061142"
---
# <a name="task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table"></a>Attività 13: Aggiunta di Destinazione OLE DB a Scrivi dati fornitore nella tabella di gestione temporanea MDS
  Ora che sono stati aggiunti i valori **ImportType** e **BatchTag** a tutti i record, si è pronti per inviarli a MDS per la gestione temporanea. In questa attività si utilizza la destinazione OLE DB per scrivere i dati in **STG. supplier_Leaf** tabella di staging.  
  
1.  Trascinare **OLE DB destinazione** dalla sezione **altre destinazioni** nella **casella degli strumenti SSIS** nella scheda **flusso di dati** e rilasciarla in **Aggiungi colonne richieste da MDS**.  
  
2.  Fare clic con il pulsante destro del mouse su **OLE DB destinazione** nella scheda **flusso di dati** e quindi scegliere **Rinomina**. Digitare **Scrivi dati fornitore nella tabella di staging di MDS** e premere **invio**.  
  
3.  Connettere l' **aggiunta di colonne richieste da MDS** per **scrivere i dati fornitore nella tabella di staging MDS** usando il connettore blu.  
  
4.  Fare doppio clic su **Scrivi dati fornitore nella tabella di staging di MDS** nella scheda **flusso di dati** .  
  
5.  Nella finestra di dialogo **Editor destinazione OLE DB** verificare che **(locale). MDS** (o **localhost). MDS**) è selezionato per il campo **gestione connessione OLE DB** .  
  
6.  Selezionare **STG. Supplier_Leaf** tabella dall'elenco di **nome della tabella o della vista**.  
  
     ![Editor destinazione OLEDB](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-01.jpg "Editor destinazione OLEDB")  
  
7.  Passare alla pagina **mapping** facendo clic su **mapping** nel menu a sinistra.  
  
8.  Eseguire il mapping delle colonne di **input** e di **destinazione** , come illustrato nella tabella seguente.  
  
     ![Editor destinazione ODBC - Mapping](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-02.jpg "Editor destinazione ODBC - Mapping")  
  
9. Verificare che vengano utilizzate colonne **_Output** per le colonne di input, non le colonne **_Status** o **_source** . **_Output** colonne contengono i valori di output della pulizia DQS.  
  
10. Fare clic su **OK** per chiudere la finestra di dialogo **Editor destinazione OLE DB** .  
  
11. Il flusso di dati deve essere simile alla figura seguente.  
  
     ![Flusso di dati completato](../../2014/tutorials/media/et-addingoledbdestinationtowdtomdsst-03.jpg "Flusso di dati completato")  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 14: Attività dell'attività Esegui SQL al flusso di controllo per eseguire la stored procedure per MDS](../../2014/tutorials/task-14-add-execute-to-control-flow-run-mds-stored-procedure.md)  
  
  
