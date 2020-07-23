---
title: 'Passaggio 7: Aggiungere e configurare la destinazione OLE DB | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 442c841d-d528-4bf0-8724-7156f909ee50
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c72ac0393733511f63844ae50b20a40e4c12ea4a
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917340"
---
# <a name="lesson-1-7-add-and-configure-the-ole-db-destination"></a>Lezione 1-7: Aggiungere e configurare la destinazione OLE DB

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Il pacchetto ora consente di estrarre i dati dall'origine file flat e trasformarli in un formato compatibile con la destinazione. L'attività successiva consiste nel caricare i dati trasformati nella destinazione. Per caricare i dati si aggiunge una destinazione OLE DB al flusso di dati. La destinazione OLE DB può usare una tabella di database, una vista o un comando SQL per caricare i dati in diversi database compatibili con OLE DB.  
  
In questa attività verrà aggiunta e configurata una destinazione OLE DB in modo da usare la gestione connessione OLE DB creata precedentemente.  
  
## <a name="add-and-configure-the-sample-ole-db-destination"></a>Aggiungere e configurare la destinazione OLE DB di esempio  
  
1.  Nella **Casella degli strumenti SSIS**espandere **Altre destinazioni**e trascinare **Destinazione OLE DB** nell'area di progettazione della scheda **Flusso di dati** . Posizionare la **destinazione OLE DB** esattamente sotto la trasformazione **Lookup Date Key**.  
  
2.  Selezionare la trasformazione **Lookup Date Key** e trascinare la freccia azzurra corrispondente sulla nuova **destinazione OLE DB** per collegare i due componenti.  
  
3.  Nella casella di riepilogo **Output** della finestra di dialogo **Selezione input e output** selezionare **Output corrispondenza ricerca** e quindi selezionare **OK**.  
  
4.  Nell'area di progettazione **Flusso di dati** selezionare il nome **Destinazione OLE DB** nel nuovo componente **Destinazione OLE DB** e cambiare il nome in **Sample OLE DB Destination**.  
  
5.  Fare doppio clic su **Sample OLE DB Destination**.  
  
6.  Nella finestra di dialogo **Editor destinazione OLE DB** verificare che **localhost.AdventureWorksDW2012** sia selezionato nella casella **Gestione connessione OLE DB**.  
  
7.  Nella casella **Nome tabella o vista** immettere o selezionare **[dbo].[FactCurrencyRate]** .  
  
8.  Selezionare il pulsante **Nuova** per creare una nuova tabella.  Cambiare il nome della tabella nello script da **Sample OLE DB Destination** a **NewFactCurrencyRate**.  Selezionare **OK**.  
  
9. Quando si seleziona **OK**, la finestra di dialogo si chiude e la casella **Nome tabella o vista** viene impostata automaticamente su **NewFactCurrencyRate**.  
  
10. Selezionare **Mapping**.  
  
11. Verificare che le colonne di input **AverageRate**, **CurrencyKey**, **EndOfDayRate**e **DateKey** siano assegnate correttamente alle colonne di destinazione. Il mapping è corretto se include colonne con nomi corrispondenti.  
  
12. Selezionare **OK**.  
  
13. Fare clic con il pulsante destro del mouse sulla destinazione **Sample OLE DB Destination** e selezionare **Proprietà**.  
  
14. Nella finestra **Proprietà** verificare che la proprietà **LocaleID** sia impostata su **Inglese (Stati Uniti)** e che la proprietà **DefaultCodePage** sia impostata su **1252**.  
  
## <a name="go-to-next-task"></a>Esecuzione del passaggio successivo
[Passaggio 8: Annotare e formattare il pacchetto della lezione 1](../integration-services/lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
## <a name="see-also"></a>Vedere anche  
[Destinazione OLE DB](../integration-services/data-flow/ole-db-destination.md)  
  
  
  
