---
title: 'Attività 12: aggiunta della trasformazione colonna derivata per aggiungere le colonne richieste da MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 98ccb271-04da-4126-9729-67e9a479aaef
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 18789f5bc1d97e1531588d50e2430829f95912b8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65485245"
---
# <a name="task-12-adding-derived-column-transform-to-add-columns-required-by-mds"></a>Attività 12: Aggiunta della trasformazione Colonna derivata ad Aggiungi colonne richieste da MDS
  In questa attività viene aggiunta la trasformazione Colonna derivata al flusso di dati. Si aggiungono due colonne derivate, **ImportType** e **BatchTag**, ai record passati a questa trasformazione. È consigliabile aggiungere queste colonne prima di caricare i dati nelle tabelle di staging in MDS. Queste due colonne sono necessarie per le tabelle di staging in MDS. Per altri dettagli, vedere [tabelle di staging dei membri foglia](../master-data-services/leaf-member-staging-table-master-data-services.md) .  
  
1.  Trascinare la **trasformazione colonna derivata** dalla sezione **comune** nella **casella degli strumenti SSIS** alla scheda **flusso di dati** .  
  
2.  Fare clic con il pulsante destro del mouse su trasformazione **colonna derivata** nella scheda **flusso di dati** e quindi scegliere **Rinomina**. Digitare **Aggiungi colonne richieste da MDS** e premere **invio**.  
  
3.  Connettere i **duplicati del filtro** per **aggiungere le colonne richieste da MDS** usando il connettore blu. Verrà visualizzata la finestra di dialogo **Selezione output input** .  
  
4.  Nella finestra di dialogo **Selezione output input** selezionare **record univoci**, quindi fare clic su **OK**.  
  
     ![Finestra di dialogo Selezione input e output](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-01.jpg "Finestra di dialogo Selezione input e output")  
  
5.  Fare clic su **SSIS** sulla barra dei menu e fare clic su **variabili**.  
  
6.  Nella finestra **variabili** fare clic sul pulsante **Aggiungi variabile** sulla barra degli strumenti.  
  
     ![Finestra Variabili SSIS](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-02.jpg "Finestra Variabili SSIS")  
  
7.  Digitare **ImportType** per **nome** e **2** per il **valore**. Specificare il valore 2 dal momento che si desidera aggiungere nuovi membri a un'entità in MDS. Per informazioni dettagliate su questo parametro, vedere [tabella di staging dei membri foglia](../master-data-services/leaf-member-staging-table-master-data-services.md).  
  
8.  Fare nuovamente clic sul pulsante **Aggiungi variabile** della barra degli strumenti.  
  
9. Digitare **BatchTag** per **nome**, selezionare **stringa** per il **tipo di dati**e **EIMBatch** per il **valore**. **BatchTag** è semplicemente un nome univoco per il batch che verrà inviato a MDS.  
  
10. Nella scheda **flusso di dati** fare doppio clic su **Aggiungi colonne richieste da MDS**.  
  
11. Nella **casella di riepilogo nel riquadro inferiore**della finestra di dialogo **Editor trasformazione colonna derivata** digitare **ImportType** per **nome colonna derivata**.  
  
12. Espandere **variabili e parametri** nel riquadro in alto a sinistra e trascinare **User:: ImportType** nella colonna **espressione** .  
  
     ![Editor trasformazione Colonna derivata](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-03.jpg "Editor trasformazione Colonna derivata")  
  
13. Digitare **BatchTag** nella riga successiva per il **nome della colonna derivata**.  
  
14. Trascinare **User:: BatchTag** da **variabili e parametri** nella colonna **espressione** .  
  
15. Fare clic su **OK** per chiudere la finestra di dialogo **trasformazione colonna derivata** .  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 13: Aggiunta di Destinazione OLE DB a Scrivi dati fornitore nella tabella di gestione temporanea MDS](../../2014/tutorials/task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table.md)  
  
  
