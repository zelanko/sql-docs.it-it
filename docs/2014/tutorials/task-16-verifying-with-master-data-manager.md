---
title: 'Attività 16: Verifica con Master Data Manager . Documenti Microsoft'
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
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484681"
---
# <a name="task-16-verifying-with-master-data-manager"></a>Attività 16: Verifica con Gestione dati master
  In questa attività viene verificato lo stato del processo batch inviato dal pacchetto SSIS e viene controllato che i dati siano stati caricati nel server MDS tramite Gestione dati master.  
  
1.  Avviare Master`http://localhost/MDS`Data **Manager** ( ). Se è già aperto, fare clic su **Microsoft SQL Server Master Data Services** nella parte superiore per passare alla home **page.**  
  
2.  Fare clic su **Gestione integrazione**.  
  
3.  Si noti che è presente un batch con denominato **EIMBatch** inviato nell'elenco. Fare clic su **Importa dati** sulla barra dei menu se non viene visualizzata la schermata seguente.  
  
     ![Batch EIM](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "Batch EIM")  
  
4.  Tornare alla home page facendo clic su **SQL Server 2012 Master Data Services** nella parte superiore.  
  
5.  Assicurarsi che il modello **Fornitori** sia selezionato per **Modello** e **VERSION_1** sia selezionato per **Versione**, quindi fare clic su **Esplora**.  
  
6.  È possibile visualizzare il pacchetto di dati SSIS importato in MDS. I dati devono essere puliti e non hanno valori **di codice** duplicati (Nota: la colonna **SupplierID** in Excel corrisponde all'attributo **Code** dell'entità Supplier in MDS).  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 17: Verifica del progetto DQS Cleansing creato dal pacchetto SSIS](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
