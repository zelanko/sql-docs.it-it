---
title: 'Attività 12: Individuazione delle informazioni (individuazione informazioni) | Microsoft Docs'
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484678"
---
# <a name="task-12-discovering-knowledge-knowledge-discovery"></a>Attività 12: Individuazione delle informazioni (Individuazione informazioni)
  In questa attività viene eseguita la **individuazione informazioni** attività nei **Supplier ID** e **Supplier Name** domini. In questo scenario, tramite il processo di individuazione delle informazioni vengono importati principalmente i valori per questi due domini.  
  
 In questa esercitazione viene avviata la compilazione di una Knowledge Base nuova. Inoltre, è possibile avviare la creazione di una Knowledge Base eseguendo un'attività di individuazione delle informazioni. Quando fa clic su **creare una Knowledge Base** nella pagina principale, il client DQS consente di visualizzare una pagina con **Domain Management** attività selezionata per l'attività. È possibile modificare il **attività** al **Knowledge Discovery** e quindi nella pagina successiva è possibile creare domini come parte del processo di individuazione della Knowledge Base. Visualizzare [Perform Knowledge Discovery](https://msdn.microsoft.com/library/hh510398.aspx) per altri dettagli.  
  
1.  Nella pagina principale del Client DQS, nelle **Knowledge Base recente** fare clic su **freccia destra** accanto al **Suppliers** knowledge base e fare clic su **della Knowledge Base Individuazione**. In alternativa, è possibile fare clic su **Apri Knowledge Base**, selezionare **Suppliers** dal **elenco di knowledge base**, selezionare **Knowledge Discovery**come **impegno** e fare clic su **successiva**.  
  
     ![Menu individuazione informazioni su Main pagina](../../2014/tutorials/media/et-discoveringknowledge-01.jpg "Menu individuazione informazioni su Main pagina")  
  
2.  Selezionare **File di Excel** per **Zdroj dat**.  
  
3.  Fare clic su **esplorare**, individuare e selezionare **Suppliers. xls**, fare clic su **Open**.  
  
4.  Selezionare **Suppliers for Discovery** per **foglio di lavoro**.  
  
5.  Nel **mapping** sezione, eseguire il mapping **SupplierID** colonna dal **Excel** file per il **Supplier ID** dominio e  **Supplier Name** colonna per il **Supplier Name** dominio utilizzando **elenchi a discesa**. Il file di Excel contiene dati di esempio per la **Supplier ID** e **Supplier Name** domini. Durante il processo di individuazione, è possibile selezionare i domini di cui si desidera individuare i valori. È possibile creare i domini in questa pagina e, successivamente, eseguire il mapping delle colonne di origine ai domini in questione. In genere i domini vengono creati durante l'attività di individuazione delle informazioni e non durante l'attività di gestione dei domini.  
  
     ![Eseguire il mapping di pagina del processo di individuazione](../../2014/tutorials/media/et-discoveringknowledge-02.jpg "eseguire il mapping di pagina del processo di individuazione")  
  
6.  Fare clic su **successivo** per passare alle **Discover** pagina.  
  
7.  Nel **Discover** pagina, fare clic su **avviare** per avviare il processo di individuazione. L'individuazione viene eseguita sulle colonne **SupplierID** e **Supplier Name** nel **Suppliers. xls** file. Il **Supplier ID** e **Supplier Name** domini devono essere popolati con le informazioni ricavate dall'individuazione.  
  
     ![Pagina del processo di individuazione individua](../../2014/tutorials/media/et-discoveringknowledge-03.jpg "pagina del processo di individuazione individua")  
  
8.  Una volta completata l'analisi, esaminare i **statistiche origine** nel **scheda Profiler** nella parte inferiore della pagina. Si noti che 10 nuovi record con 20 valori totali (**SupplierID** e **Supplier Name** i valori di **foglio di lavoro di Excel**) sono stati individuati. Sarà possibile anche visualizzare quanti valori sono nuovi, univoci, nuovi e univoci, nonché validi. Nella casella di riepilogo a destra è possibile visualizzare ulteriori dettagli per ogni dominio coinvolto nel processo di individuazione. Se si posiziona il mouse sulla barra di stato nella colonna Completezza è possibile verificare l'eventuale mancanza di valori nelle colonne dell'origine.  
  
     ![I risultati dell'individuazione Knowledge](../../2014/tutorials/media/et-discoveringknowledge-04.jpg "i risultati dell'individuazione della Knowledge Base")  
  
9. Fare clic su **successivo** per passare alle **Gestisci valori di dominio** pagina.  
  
10. Nel **Gestisci valori di dominio** pagina, fare clic su **Supplier Name** dominio dall'elenco di domini.  
  
11. Nel riquadro di destra, fare doppio clic su **Lazy Country Storex** (si noti che "x" alla fine) e selezionare **Lazy Country Store**. In DQS questa modifica viene suggerita dopo l'esecuzione del correttore ortografico nel dominio. Per impostazione predefinita, il correttore ortografico è abilitato nei domini creati.  
  
     ![Correzione nome fornitore - Lazy Country Store](../../2014/tutorials/media/et-discoveringknowledge-05.jpg "correzione nome fornitore - Lazy Country Store")  
  
12. Nell'elenco dei valori di dominio, verificare che il valore **Lazy Country Storex** viene impostato come un errore (rosso **X** contrassegnare) con **Lazy Country Store** come la correzione e anche il **Lazy Country Store** viene inoltre aggiunto come un valore valido.  
  
     ![Dominio valore e di correzione](../../2014/tutorials/media/et-discoveringknowledge-06.jpg "dominio valore e di correzione")  
  
13. Scegliere **Fine**.  
  
14. Sul **SQL Server Data Quality Services** finestra di dialogo, fare clic su **Publish**.  
  
15. Fare clic su **OK** nella finestra di messaggio di esito positivo.  
  
     È stata completata la prima lezione dell'esercitazione.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Lezione 2: Pulizia dei dati fornitore mediante la Knowledge Base Suppliers](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)  
  
  
