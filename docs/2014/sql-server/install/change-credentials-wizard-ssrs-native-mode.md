---
title: Procedura guidata Modifica credenziali (modalità nativa SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.changecredentialswizard.F1
helpviewer_keywords:
- Change Credentials Wizard
- report server database, reconfigure
ms.assetid: 9eb4060a-9c3e-41e0-8767-3cfaebc45de7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9dba9988bec98f597a59fe4152b2abdde0d5ccea
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66096713"
---
# <a name="change-credentials-wizard-ssrs-native-mode"></a>Procedura guidata Modifica credenziali (modalità nativa SSRS)
  In Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è disponibile la procedura guidata Modifica credenziali, che consente di eseguire in modo semplificato i passaggi necessari per riconfigurare l'account utilizzato dal server di report per la connessione al database del server di report. Quando si modificano le credenziali, Gestione configurazione aggiorna tutte le autorizzazioni e le informazioni sull'account di accesso al database nel server di database per il database del server di report utilizzato attivamente dal server di report.  
  
 Per avviare la procedura guidata, fare clic su **Modifica credenziali** nella pagina Database di Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per istruzioni su come avviare il [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, consultare [Gestione configurazione Reporting Services &#40;in modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="options"></a>Opzioni  
 **Server di database**  
 Consente di specificare il nome dell'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] in cui è in esecuzione il database del server di report.  
  
 Per connettersi all'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , utilizzare credenziali che dispongono delle autorizzazioni necessarie per accedere al server e aggiornare le informazioni del database. Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utilizza le credenziali di Windows correnti, ma se non si dispone di un account di accesso o di autorizzazioni per il database, è possibile specificare un account di accesso al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Non è possibile specificare credenziali di Windows diverse. Se si desidera connettersi come utente di Windows diverso, accedere utilizzando il nome utente desiderato, quindi avviare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 **Credenziali**  
 Viene specificato l'account utilizzato dal server di report per la connessione al database del server di report. Tra i valori validi sono inclusi l'account del servizio Web ReportServer, un account di accesso al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definito nell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] utilizzata per ospitare il server di report o un account di Windows. Se si usa un account di Windows, è possibile specificare un account locale (*\<nomecomputer >\\< nome utente\>*) se il server di report e il database si trovano sul computer stesso, o un utente di dominio account (*\<dominio >\\< nome utente\>*) se si trovano in computer diversi nello stesso dominio.  
  
 Il server di report creerà un account di accesso al database e assegnerà le autorizzazioni per il database all'account specificato.  
  
 Il server di report non crea l'account stesso. L'account specificato deve essere già presente e valido per la configurazione della distribuzione. In particolare, se il database si trova in un computer remoto e si desidera utilizzare un account di Windows, è necessario specificare un account che disponga di autorizzazioni di accesso nel computer specifico.  
  
 Se il computer è in un dominio diverso o non trusted, utilizzare un account di accesso al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni sulla scelta di un account, vedere [configurare una connessione di Database Server di Report &#40;Gestione configurazione SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
 **Riepilogo**  
 Consente di verificare le impostazioni prima dell'esecuzione della procedura guidata.  
  
 **Continua e termina**  
 Consente di monitorare lo stato di ogni attività.  
  
## <a name="see-also"></a>Vedere anche  
 [Database &#40;modalità nativa SSRS&#41;](../../../2014/sql-server/install/database-ssrs-native-mode.md)   
 [Procedura guidata cambia Database &#40;modalità nativa SSRS&#41;](../../../2014/sql-server/install/change-database-wizard-ssrs-native-mode.md)   
 [Creare un database del server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Gli argomenti della Guida F1 di Gestione configurazione di Reporting Services &#40;modalità nativa SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Configurare una connessione del database del server di report &#40;Gestione configurazione SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
