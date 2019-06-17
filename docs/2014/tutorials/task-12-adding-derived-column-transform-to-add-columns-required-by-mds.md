---
title: 'Attività 12: Aggiunta di trasformazione colonna derivata ad Aggiungi colonne richieste da MDS | Microsoft Docs'
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65485245"
---
# <a name="task-12-adding-derived-column-transform-to-add-columns-required-by-mds"></a>Attività 12: Aggiunta della trasformazione Colonna derivata ad Aggiungi colonne richieste da MDS
  In questa attività viene aggiunta la trasformazione Colonna derivata al flusso di dati. Si aggiungono due colonne derivate, **ImportType** e **BatchTag**a record passati a questa trasformazione. È consigliabile aggiungere queste colonne prima di caricare i dati nelle tabelle di staging in MDS. Queste due colonne sono necessarie per le tabelle di staging in MDS. Visualizzare [tabelle di gestione temporanea di membri foglia](../master-data-services/leaf-member-staging-table-master-data-services.md) per altri dettagli.  
  
1.  Trascinare **trasformazione colonna derivata** dalla **comuni** sezione la **casella degli strumenti SSIS** per il **del flusso di dati** scheda.  
  
2.  Fare doppio clic su **colonna derivata** trasformare nel **flusso di dati** scheda, quindi scegliere **rinominare**. Tipo di **Aggiungi colonne richieste da MDS** , quindi premere **invio**.  
  
3.  Connettere **Filtra duplicati** al **Aggiungi colonne richieste da MDS** usando il collegamento blu. Dovrebbero vedere le **selezione Input e Output** nella finestra di dialogo.  
  
4.  Nel **selezione Input e Output** finestra di dialogo **record univoci**, fare clic su **OK**.  
  
     ![Finestra di dialogo di selezione di Output di input](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-01.jpg "Output finestra di dialogo di selezione di Input")  
  
5.  Fare clic su **SSIS** nella barra dei menu e fare clic su **variabili**.  
  
6.  Nel **variabili** finestra, fare clic su **Aggiungi variabile** pulsante sulla barra degli strumenti.  
  
     ![Finestra variabili SSIS](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-02.jpg "finestra variabili SSIS")  
  
7.  Tipo di **ImportType** per il **Name** e **2** per il **valore**. Specificare il valore 2 dal momento che si desidera aggiungere nuovi membri a un'entità in MDS. Per informazioni dettagliate su questo parametro, vedere [tabella di Staging dei membri foglia](../master-data-services/leaf-member-staging-table-master-data-services.md).  
  
8.  Fare clic su **Aggiungi variabile** nuovo clic sul pulsante della barra degli strumenti.  
  
9. Tipo **BatchTag** per il **Name**, selezionare **stringa** per il **tipo di dati**, e **EIMBatch** per il **Valore**. **BatchTag** è semplicemente un nome univoco per il batch sarà inviata a MDS.  
  
10. Nel **flusso di dati** scheda, fare doppio clic su **Aggiungi colonne richieste da MDS**.  
  
11. Nel **Editor trasformazione colonna derivata** nella finestra di dialogo il **casella di riepilogo nel riquadro inferiore**, digitare **ImportType** per il **nome colonna derivata**.  
  
12. Espandere **variabili e parametri** nel riquadro superiore sinistro, trascinare **User:: importtype** per il **espressione** colonna.  
  
     ![Editor trasformazione colonna derivata](../../2014/tutorials/media/et-addingdcttoaddcolumnsrequiredbymds-03.jpg "Editor trasformazione colonna derivata")  
  
13. Tipo di **BatchTag** nella riga successiva per il **nome colonna derivata**.  
  
14. Funzionalità di trascinamento **User:: batchtag** dalla **variabili e parametri** per il **espressione** colonna.  
  
15. Fare clic su **OK** per chiudere la **trasformazione colonna derivata** nella finestra di dialogo.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 13: Aggiunta di destinazione OLE DB per scrivere dati nella tabella di gestione temporanea MDS](../../2014/tutorials/task-13-adding-ole-db-destination-to-write-data-to-mds-staging-table.md)  
  
  
