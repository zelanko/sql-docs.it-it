---
title: 'Attività 16: verifica con Gestione dati master | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 57ad9d3e-8f95-4df6-af01-c291ccf49164
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d9828c02625ae2bc5a85859577a237b4c4fa99c5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81484681"
---
# <a name="task-16-verifying-with-master-data-manager"></a>Attività 16: Verifica con Gestione dati master
  In questa attività viene verificato lo stato del processo batch inviato dal pacchetto SSIS e viene controllato che i dati siano stati caricati nel server MDS tramite Gestione dati master.  
  
1.  Avviare **Gestione dati master** (`http://localhost/MDS`). Se è già aperto, fare clic su **Microsoft SQL Server Master Data Services** nella parte superiore per passare al **Home page**.  
  
2.  Fare clic su **Gestione integrazione**.  
  
3.  Si noti che è presente un batch con il nome **EIMBatch** inviato nell'elenco. Se non viene visualizzata la schermata seguente, fare clic su **Importa dati** nella barra dei menu.  
  
     ![Batch EIM](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "Batch EIM")  
  
4.  Tornare al home page facendo clic **SQL Server Master Data Services 2012** nella parte superiore.  
  
5.  Verificare che il **modello Suppliers** sia selezionato **per modello** e **VERSION_1** sia selezionato per **versione**, quindi fare clic su **Esplora**.  
  
6.  È possibile visualizzare il pacchetto di dati SSIS importato in MDS. I dati devono essere puliti e non contengono valori di **codice** duplicati (Nota: la colonna **SupplierID** in Excel corrisponde all'attributo **Code** dell'entità Supplier in MDS).  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 17: Verifica del progetto DQS Cleansing creato dal pacchetto SSIS](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
