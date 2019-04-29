---
title: Estrarre i dati tramite l'origine OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- extracting data [Integration Services]
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: 4ca6eeb5-b60e-4b81-86dd-0674be8ae8d8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8303cc8e30a9099a11a43cc2b4bfac341873a044
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62902607"
---
# <a name="extract-data-by-using-the-ole-db-source"></a>Estrazione dei dati tramite l'origine OLE DB
  È possibile aggiungere e configurare un'origine OLE DB solo se il pacchetto include già almeno un'attività Flusso di dati.  
  
### <a name="to-extract-data-using-an-ole-db-source"></a>Per estrarre dati tramite un'origine OLE DB  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di dati** e quindi dalla **Casella degli strumenti**trascinare l'origine OLE DB nell'area di progettazione.  
  
4.  Fare doppio clic sull'origine OLE DB.  
  
5.  Nella pagina **Gestione connessione** della finestra di dialogo **Editor origine OLE DB** selezionare una gestione connessione OLE DB esistente oppure fare clic su **Nuova** per creare una nuova gestione connessione. Per altre informazioni, vedere [Gestione connessione OLE DB](../connection-manager/ole-db-connection-manager.md).  
  
6.  Selezionare il metodo di accesso ai dati:  
  
    -   **Tabella o vista** Selezionare la tabella o vista del database a cui deve connettersi la gestione connessione OLE DB.  
  
    -   **Variabile nome vista o nome tabella** Selezionare la variabile definita dall'utente che contiene il nome della tabella o vista del database a cui deve connettersi la gestione connessione OLE DB.  
  
    -   **Comando SQL** Digitare un comando SQL oppure fare clic su **Compila query** per scrivere un comando SQL usando **Generatore query**.  
  
        > [!NOTE]  
        >  Il comando può includere parametri. Per altre informazioni, vedere [Mapping dei parametri di query a variabili in un componente di un flusso di dati](map-query-parameters-to-variables-in-a-data-flow-component.md).  
  
    -   **Comando SQL da variabile** Selezionare la variabile definita dall'utente che contiene il comando SQL.  
  
        > [!NOTE]  
        >  La variabile deve essere definita nell'ambito della stessa attività Flusso di dati che contiene l'origine OLE DB, oppure nell'ambito dello stesso pacchetto, e deve avere un tipo di dati string.  
  
7.  Per aggiornare il mapping tra colonne esterne e colonne di output, fare clic su **Colonne** e selezionare colonne diverse nell'elenco **Colonna esterna** .  
  
8.  Facoltativamente, aggiornare i nomi delle colonne di output modificando i valori nell'elenco **Colonna di output** .  
  
9. Per configurare l'output degli errori, fare clic su **Output errori**. Per altre informazioni, vedere [Configurare un output degli errori in un componente del flusso di dati](../configure-an-error-output-in-a-data-flow-component.md).  
  
10. Facendo clic su **Anteprima** è possibile visualizzare fino a 200 righe di dati estratti dall'origine OLE DB.  
  
11. Fare clic su **OK**.  
  
12. Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Origine OLE DB](ole-db-source.md)   
 [Trasformazioni di Integration Services](transformations/integration-services-transformations.md)   
 [Percorsi in Integration Services](integration-services-paths.md)   
 [Attività Flusso di dati](../control-flow/data-flow-task.md)  
  
  
