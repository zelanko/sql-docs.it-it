---
title: Proprietà server (pagina Registrazione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.logging.f1
ms.assetid: b338deab-4868-4951-9f22-0605add2fc95
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2a04c27fd790a1ad5c4ba453b43af5983a6440e3
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66099526"
---
# <a name="server-properties-logging-page"></a>Proprietà  server (pagina Registrazione)
  Utilizzare questa pagina per impostare i limiti relativi ai dati sull'esecuzione dei report raccolti dal server di report. I dati di esecuzione vengono archiviati internamente nel database del server di report. È possibile tenere traccia dell'attività di un server di report eseguito in modalità nativa o in modalità integrata SharePoint. Se il server di report fa parte di una distribuzione con scalabilità orizzontale, nel log di esecuzione del report viene conservato un record di tutte le attività del report per l'intera distribuzione in un unico file di log.  
  
 Per aprire questa pagina, avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], connettersi a un server di report, il nome del server di report e scegliere **proprietà**. Fare clic su **Registrazione** per aprire la pagina.  
  
## <a name="options"></a>Opzioni  
 **Attiva la registrazione per l'esecuzione di report**  
 Fare clic per creare e archiviare le informazioni sull'attività del report nel server. Se questa opzione è attivata, tramite il server di report verranno registrati i report utilizzati, la frequenza di elaborazione dei report, il tipo di operazione del report eseguita, il formato di output e l'utente che ha eseguito il report. Per altre informazioni sui punti dati aggiuntivi che vengono acquisiti nel log, vedere [Log di esecuzione Server di Report e vista ExecutionLog3](../report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
 **Rimuovi le voci del log dopo il numero di giorni seguente**  
 Consente di specificare il numero di giorni trascorsi i quali le voci di log verranno rimosse dal log di esecuzione del report. Il valore predefinito è 60 giorni.  
  
## <a name="see-also"></a>Vedere anche  
 [Impostare le proprietà di un server di report &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Eseguire la connessione a un server di report in Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [File di log e origini di Reporting Services](../report-server/reporting-services-log-files-and-sources.md)   
 [Guida sensibile al contesto del server di report in Management Studio](report-server-in-management-studio-f1-help.md)   
 [Log di esecuzione del server di report e la vista ExecutionLog3](../report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
  
