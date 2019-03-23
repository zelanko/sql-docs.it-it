---
title: Visualizzare gli eventi per il servizio Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- events [Integration Services]
- service [Integration Services], events
- Integration Services service, events
ms.assetid: 37e23946-10d1-4116-8568-8fd24067102e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8c00739cefe457575e6b05dee368d8965775a387
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58389190"
---
# <a name="view-events-for-the-integration-services-service"></a>Visualizzare eventi per il servizio Integration Services
  Sono disponibili due strumenti nei quali è possibile visualizzare eventi per il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   La finestra di dialogo **Visualizzatore file di log** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Nella finestra di dialogo **Visualizzatore file di log** sono disponibili opzioni per l'esportazione, l'applicazione di filtri e l'esecuzione di ricerche nel log. Per altre informazioni sulle opzioni della finestra di dialogo **Visualizzatore file di log**, vedere [Guida sensibile al contesto del Visualizzatore file di log](../relational-databases/logs/log-file-viewer-f1-help.md).  
  
-   Visualizzatore eventi di Windows.  
  
 Per descrizioni degli eventi registrati dal servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , vedere [Eventi registrati dal servizio Integration Services](service/events-logged-by-the-integration-services-service.md).  
  
### <a name="to-view-service-events-for-integration-services-in-sql-server-management-studio"></a>Per visualizzare gli eventi del servizio per Integration Services in SQL Server Management Studio  
  
1.  Aprire [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  Scegliere **Connetti Esplora oggetti** dal menu **File**.  
  
3.  Nella finestra di dialogo **Connetti al server** selezionare il tipo di server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , selezionare o individuare il server a cui connettersi e quindi fare clic su **Connetti**.  
  
4.  In Esplora oggetti fare clic con il pulsante destro del mouse su [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e quindi scegliere **Visualizza log**.  
  
5.  Per visualizzare gli eventi di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , selezionare **SQL Server Integration Services**. L'opzione **Eventi NT** , selezionata automaticamente, viene deselezionata quando si seleziona l'opzione **SQL Server Integration Services** .  
  
### <a name="to-view-service-events-for-integration-services-in-windows-event-viewer"></a>Per visualizzare gli eventi del servizio per Integration Services in Windows nel Visualizzatore eventi  
  
1.  Nel **Pannello di controllo**fare clic su **Strumenti di amministrazione**nella visualizzazione classica oppure su **Prestazioni e manutenzione** e quindi su **Strumenti di amministrazione**nella visualizzazione per categorie.  
  
2.  Fare clic su **Visualizzatore eventi**.  
  
3.  Nella finestra di dialogo **Visualizzatore eventi** fare clic su **Applicazione**.  
  
4.  Nello snap-in **Applicazione** individuare nella colonna **Origine** la voce con valore **SQLISService**, fare clic con il pulsante destro del mouse sulla voce e quindi scegliere **Proprietà**.  
  
5.  Facoltativamente, fare clic sulla freccia SU o freccia GIÙ per visualizzare l'evento precedente o successivo.  
  
6.  Facoltativamente, fare clic sul pulsante Copia negli Appunti per copiare le informazioni sugli eventi.  
  
7.  Impostare la visualizzazione dei dati degli eventi in base a byte o parole.  
  
8.  Fare clic su **OK**.  
  
9. Scegliere **Esci** dal menu **File** per chiudere la finestra di dialogo **Visualizzatore eventi** .  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione del servizio Integration Services](../../2014/integration-services/manage-the-integration-services-service.md)   
 [Aggiunta di un registro per i contatori delle prestazioni del flusso di dati](performance/performance-counters.md)  
  
  
