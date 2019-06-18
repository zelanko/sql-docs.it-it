---
title: Proprietà server (pagina Registrazione) | Microsoft Docs
ms.date: 06/10/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.logging.f1
ms.assetid: b338deab-4868-4951-9f22-0605add2fc95
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9e9286363970b568e0690b622fac6d94c2b01f6b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571383"
---
# <a name="server-properties-logging-page"></a>Proprietà  server (pagina Registrazione)
  Usare questa pagina [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] in [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] per impostare i limiti relativi ai dati sull'esecuzione dei report raccolti dal server di report. I dati di esecuzione vengono archiviati internamente nel database del server di report. È possibile tenere traccia dell'attività di un server di report eseguito in modalità nativa o in modalità integrata SharePoint. Se il server di report fa parte di una distribuzione con scalabilità orizzontale, nel log di esecuzione del report viene conservato un record di tutte le attività del report per l'intera distribuzione in un unico file di log.  
  
 Per aprire la pagina:
 1) Start [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]
 2) Connettersi a un'istanza di un server di report.
 3) Fare clic con il pulsante destro del mouse sul nome del server di report, quindi scegliere **Proprietà**. 
 4) Fare clic su **Registrazione** per aprire la pagina.  
  
## <a name="options"></a>Opzioni  
 **Attiva la registrazione per l'esecuzione di report**  
 Fare clic per creare e archiviare le informazioni sull'attività del report nel server. Se questa opzione è attivata, tramite il server di report verranno registrati i report utilizzati, la frequenza di elaborazione dei report, il tipo di operazione del report eseguita, il formato di output e l'utente che ha eseguito il report. Per maggiori informazioni su altri punti dati acquisiti nel log, vedere [Vista ExecutionLog ed ExecutionLog3 del server di report](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
 **Rimuovi le voci del log dopo il numero di giorni seguente**  
 Consente di specificare il numero di giorni trascorsi i quali le voci di log verranno rimosse dal log di esecuzione del report. Il valore predefinito è 60 giorni.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare le proprietà di un server di report &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Eseguire la connessione a un server di report in Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [File di log e origini di Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Guida sensibile al contesto del server di report in Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Vista ExecutionLog ed ExecutionLog3 del server di report](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
  
