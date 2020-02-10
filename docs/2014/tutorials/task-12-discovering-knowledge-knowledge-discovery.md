---
title: 'Attività 12: individuazione delle informazioni (individuazione informazioni) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: dd80a8e6-1e41-4c49-9898-02b1d2505a10
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 6dd54475ee63b2f6ef5e1b56b94c11aafd5996ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484678"
---
# <a name="task-12-discovering-knowledge-knowledge-discovery"></a>Attività 12: Individuazione delle informazioni (Individuazione informazioni)
  In questa attività viene eseguita l'attività di **individuazione delle informazioni** sui domini **Supplier ID** e **Supplier Name** . In questo scenario, tramite il processo di individuazione delle informazioni vengono importati principalmente i valori per questi due domini.  
  
 In questa esercitazione viene avviata la compilazione di una Knowledge Base nuova. Inoltre, è possibile avviare la creazione di una Knowledge Base eseguendo un'attività di individuazione delle informazioni. Quando si fa clic su **Crea una Knowledge base** nella pagina principale, il client DQS porta a una pagina con l'attività di **gestione del dominio** selezionata per l'attività. È possibile modificare l' **attività** in **Individuazione informazioni** , quindi nella pagina successiva è possibile creare domini come parte del processo di individuazione delle informazioni. Per ulteriori informazioni, vedere [eseguire l'individuazione delle informazioni](https://msdn.microsoft.com/library/hh510398.aspx) .  
  
1.  Nella sezione **Knowledge Base recente** della pagina principale del client DQS fare clic sulla freccia a **destra** accanto alla Knowledge base **Suppliers** e scegliere **Individuazione informazioni**. In alternativa, è possibile fare clic su **Apri Knowledge base**, selezionare **Suppliers** dall' **elenco di Knowledge**base, selezionare **Individuazione informazioni** come **attività** e fare clic su **Avanti**.  
  
     ![Menu Individuazione informazioni nella pagina principale](../../2014/tutorials/media/et-discoveringknowledge-01.jpg "Menu Individuazione informazioni nella pagina principale")  
  
2.  Selezionare il **file di Excel** per **origine dati**.  
  
3.  Fare clic su **Sfoglia**, spostarsi e selezionare **Suppliers. xls**, quindi fare clic su **Apri**.  
  
4.  Selezionare **Suppliers for Discovery** for **Worksheet**.  
  
5.  Nella sezione **mapping** , eseguire il mapping della colonna **SupplierID** dal file di **Excel** alla colonna Supplier **ID** Domain e **Supplier** Name al dominio **Supplier Name** usando gli **elenchi a discesa**. Il file di Excel contiene dati di esempio per i domini **Supplier ID** e **Supplier Name** . Durante il processo di individuazione, è possibile selezionare i domini di cui si desidera individuare i valori. È possibile creare i domini in questa pagina e, successivamente, eseguire il mapping delle colonne di origine ai domini in questione. In genere i domini vengono creati durante l'attività di individuazione delle informazioni e non durante l'attività di gestione dei domini.  
  
     ![Pagina Mappa del processo di individuazione](../../2014/tutorials/media/et-discoveringknowledge-02.jpg "Pagina Mappa del processo di individuazione")  
  
6.  Fare clic su **Avanti** per passare alla pagina **individua** .  
  
7.  Nella pagina **individua** fare clic su **Avvia** per avviare il processo di individuazione. L'individuazione viene eseguita sulle colonne **SupplierID** e **Supplier Name** nel file **Suppliers. xls** . I domini **Supplier ID** e **Supplier Name** devono essere popolati con le informazioni ricavate dall'individuazione.  
  
     ![Pagina Individua del processo di individuazione](../../2014/tutorials/media/et-discoveringknowledge-03.jpg "Pagina Individua del processo di individuazione")  
  
8.  Al termine dell'analisi, esaminare le **statistiche di origine** nella **scheda Profiler** nella parte inferiore della pagina. Si noti che sono stati individuati 10 nuovi record con 20 valori totali (valori**SupplierID** e **Supplier Name** del foglio di lavoro di **Excel**). Sarà possibile anche visualizzare quanti valori sono nuovi, univoci, nuovi e univoci, nonché validi. Nella casella di riepilogo a destra è possibile visualizzare ulteriori dettagli per ogni dominio coinvolto nel processo di individuazione. Se si posiziona il mouse sulla barra di stato nella colonna Completezza è possibile verificare l'eventuale mancanza di valori nelle colonne dell'origine.  
  
     ![Risultati dell'individuazione delle informazioni](../../2014/tutorials/media/et-discoveringknowledge-04.jpg "Risultati dell'individuazione delle informazioni")  
  
9. Fare clic su **Avanti** per passare alla pagina **Gestisci valori di dominio** .  
  
10. Nella pagina **Gestisci valori di dominio** fare clic su **Fornitore nome** dominio nell'elenco di domini.  
  
11. Nel riquadro destro fare clic con il pulsante destro del mouse su **Lazy Country Storex** (avviso ' x ' alla fine) e selezionare **Lazy Country Store**. In DQS questa modifica viene suggerita dopo l'esecuzione del correttore ortografico nel dominio. Per impostazione predefinita, il correttore ortografico è abilitato nei domini creati.  
  
     ![Correzione nome fornitore - Archivio paesi differito](../../2014/tutorials/media/et-discoveringknowledge-05.jpg "Correzione nome fornitore - Archivio paesi differito")  
  
12. Nell'elenco dei valori di dominio verificare che il valore **Lazy Country Storex** sia impostato come errore (contrassegno **X** rosso) con **Lazy Country Store** come correzione e anche l' **Archivio Lazy Country** venga aggiunto come valore valido.  
  
     ![Valori di dominio e di correzione](../../2014/tutorials/media/et-discoveringknowledge-06.jpg "Valori di dominio e di correzione")  
  
13. Fare clic su **Fine**.  
  
14. Nella finestra di dialogo **SQL Server Data Quality Services** fare clic su **pubblica**.  
  
15. Fare clic su **OK** nella finestra di messaggio operazione riuscita.  
  
     È stata completata la prima lezione dell'esercitazione.  
  
## <a name="next-step"></a>passaggio successivo  
 [Lezione 2: Pulizia dei dati fornitore mediante la Knowledge Base Suppliers](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)  
  
  
