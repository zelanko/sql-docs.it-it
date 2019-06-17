---
title: "Esercitazione: Uso dell'origine OData [SSIS] | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2c64cf8b-5edb-48df-8ffe-697096258f71
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7a799707dc57e07528afb29c135a5ee394c56354
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770217"
---
# <a name="tutorial-using-the-odata-source-ssis"></a>Esercitazione: Uso dell'origine OData [SSIS]
  In questa esercitazione viene eseguito il processo per estrarre la raccolta **Dipendenti** del servizio **Northwind** OData di esempio (http://services.odata.org/V3/Northwind/Northwind.svc/) e caricarla in un file flat.  
  
## <a name="1-create-an-integration-services-project"></a>1. Creare un progetto di Integration Services  
  
1.  Avviare **SQL Server Data Tools** o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
2.  Fare clic su **Nuovo**dal menu **File**, quindi scegliere **Progetto**.  
  
3.  Nella finestra di dialogo **Nuovo progetto** espandere **Installato**, **Modelli**, **Business Intelligence**, quindi scegliere **Integration Services**.  
  
4.  Selezionare **Progetto di Integration Services** come tipo di progetto.  
  
5.  Immettere un **nome** e selezionare un **percorso** per il progetto, quindi fare clic su **OK**.  
  
## <a name="2-add-and-configure-odata-source-to-the-ssis-package"></a>2. Aggiungere e configurare l'origine OData per il pacchetto SSIS  
  
1.  Trascinare un'**Attività Flusso di dati** da **Casella degli strumenti SSIS** all'area di progettazione del flusso di controllo del pacchetto SSIS.  
  
2.  Fare clic sulla scheda **Flusso di dati** oppure fare doppio clic sull' **attività Flusso di dati** appena aggiunta per avviare l' **area di progettazione Flusso di dati**.  
  
3.  Trascinare **Origine Odata** dal gruppo **Comune** in **Casella degli strumenti SSIS**. Quando si installa per la prima volta, **Origine Odata** viene visualizzato nel gruppo **Comune** in **Casella degli strumenti SSIS**.  
  
4.  Fare doppio clic sul componente **Origine OData** per aprire la finestra di dialogo **Editor origine OData** .  
  
5.  Fare clic su **Nuovo** per aggiungere una nuova gestione connessione OData.  
  
6.  Immettere l'URL del servizio OData in **percorso documento di servizio**. Può essere l'URL del documento di servizio o l'URL di un'entità o di un feed specifico. Ai fini di questa esercitazione, digitare [ http://services.odata.org/V3/Northwind/Northwind.svc/ ](http://services.odata.org/V3/Northwind/Northwind.svc/).  
  
7.  Verificare che sia selezionato **Autenticazione di Windows** come **autenticazione** da utilizzare per accedere al servizio OData. **Autenticazione di Windows** è selezionato per impostazione predefinita. Per utilizzare l'autenticazione di base, selezionare **Usa il nome utente e la password seguenti**.  
  
8.  Fare clic su **Test connessione** per la connessione e fare clic su **OK** per creare un'istanza della gestione connessione OData.  
  
9. Nella finestra di dialogo **Editor origine OData** , verificare che **Raccolta** sia selezionato per l'opzione **Utilizza raccolta in percorso risorse** .  
  
10. Selezionare **Dipendenti** nell'elenco a discesa **Raccolta**.  
  
11. Immettere tutti i filtri o le opzioni query OData aggiuntive per **Opzioni query**. Ex. $orderby=CompanyName&$top=100. Ai fini di questa esercitazione immettere **$top=5**.  
  
12. Fare clic su **Anteprima** per visualizzare un'anteprima dei dati.  
  
13. Fare clic su **Colonne** nel riquadro di navigazione sinistro per passare alla pagina **Colonne** .  
  
14. Scegliere **EmployeeID**, **FirstName**e **LastName** da **Colonne esterne disponibili** selezionando le caselle di controllo.  
  
15. Fare clic su **OK** per chiudere la finestra di dialogo **Editor origine OData** .  
  
## <a name="3-add-flat-file-destination-and-test-the-solution"></a>3. Aggiungere la destinazione del file flat e testare la soluzione  
  
1.  Trascinare una **Destinazione file flat** dalla **casella degli strumenti SSIS** all'area di progettazione del flusso di dati sotto il componente **Origine Odata**.  
  
2.  Connettere il componente **Origine Odata** al componente **Destinazione file flat** utilizzando la freccia blu.  
  
3.  Fare doppio clic su **Destinazione file flat**. Viene visualizzata la finestra di dialogo **Editor destinazione file flat** .  
  
4.  Nella finestra di dialogo **Editor destinazione file flat** fare clic su **Nuovo** per creare una nuova gestione connessione file flat.  
  
5.  Nella finestra di dialogo **Formato file flat** selezionare **Delimitato**. Viene visualizzata la finestra di dialogo **Editor gestione connessione file flat** .  
  
6.  Nella finestra di dialogo **Editor gestione connessione file flat** immettere **c:\Employees.txt**in **Nome file**.  
  
7.  Fare clic su **Colonne**nel pannello di navigazione sinistro. In questa pagina è possibile visualizzare l'anteprima dei dati.  
  
8.  Fare clic su OK per chiudere la finestra di dialogo **Editor gestione connessione file flat** .  
  
9. Nella finestra di dialogo **Editor destinazione file flat** fare clic su **Mapping** nel riquadro di navigazione sinistro. Controllare i mapping.  
  
10. Fare clic su OK per chiudere la finestra di dialogo **Editor destinazione file flat** .  
  
11. Compilare ed eseguire il pacchetto SSIS. Verificare che il file di output venga creato con l'ID, il nome e il cognome di 5 dipendenti dal feed OData.  
  
  
