---
title: 'Attività 16: Verifica con gestione dati Master | Microsoft Docs'
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
ms.openlocfilehash: 35dd2da7f6cf6598918cd9d109b97f3d314556d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484695"
---
# <a name="task-16-verifying-with-master-data-manager"></a>Attività 16: Verifica con Gestione dati master
  In questa attività viene verificato lo stato del processo batch inviato dal pacchetto SSIS e viene controllato che i dati siano stati caricati nel server MDS tramite Gestione dati master.  
  
1.  Avvio veloce **gestione dati Master** ([http://localhost/MDS](http://localhost/MDS)). Se è già aperto, fare clic su **Microsoft SQL Server Master Data Services** nella parte superiore per passare alle **homepage**.  
  
2.  Fare clic su **Gestione integrazione**.  
  
3.  Si noti che è presente un batch con denominato **EIMBatch** che è stato inviato nell'elenco. Fare clic su **Import Data** nella barra dei menu se non viene visualizzata la schermata seguente.  
  
     ![EIM Batch](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "EIM Batch")  
  
4.  Tornare alla home page, fare clic su **SQL Server 2012 Master Data Services** nella parte superiore.  
  
5.  Assicurarsi che **Suppliers** modello selezionato per **Model** e **VERSION_1** sia selezionato per **versione**e fare clic su  **Esplora**.  
  
6.  È possibile visualizzare il pacchetto di dati SSIS importato in MDS. I dati devono essere puliti e non sono duplicati **codice** valori (Nota: **SupplierID** colonna in Excel corrisponde al **codice** attributo dell'entità Supplier in MDS).  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 17: Verifica del progetto DQS Cleansing creato dal pacchetto SSIS](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
