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
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 04d715bee7fdd8d61796040fa04b3fb68db1d15a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85045364"
---
# <a name="change-credentials-wizard-ssrs-native-mode"></a>Procedura guidata Modifica credenziali (modalità nativa SSRS)
  In Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è disponibile la procedura guidata Modifica credenziali, che consente di eseguire in modo semplificato i passaggi necessari per riconfigurare l'account utilizzato dal server di report per la connessione al database del server di report. Quando si modificano le credenziali, Gestione configurazione aggiorna tutte le autorizzazioni e le informazioni sull'account di accesso al database nel server di database per il database del server di report utilizzato attivamente dal server di report.  
  
 Per avviare la procedura guidata, fare clic su **Modifica credenziali** nella pagina Database di Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per istruzioni su come avviare la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, vedere [Reporting Services Configuration Manager &#40;modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modalità nativa.  
  
## <a name="options"></a>Opzioni  
 **Server di database**  
 Specifica il nome dell' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] istanza di che esegue il database del server di report.  
  
 Per connettersi all'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , utilizzare credenziali che dispongono delle autorizzazioni necessarie per accedere al server e aggiornare le informazioni del database. Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utilizza le credenziali di Windows correnti, ma se non si dispone di un account di accesso o di autorizzazioni per il database, è possibile specificare un account di accesso al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Non è possibile specificare credenziali di Windows diverse. Se si desidera connettersi come utente di Windows diverso, accedere utilizzando il nome utente desiderato, quindi avviare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 **Credenziali**  
 Viene specificato l'account utilizzato dal server di report per la connessione al database del server di report. Tra i valori validi sono inclusi l'account del servizio Web ReportServer, un account di accesso al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definito nell'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] utilizzata per ospitare il server di report o un account di Windows. Se si utilizza un account di Windows, è possibile specificare un account locale (* \<computername> \\<nome \> utente*) se il server di report e il database si trovano nello stesso computer oppure un account utente di dominio (* \<domain> \\<nome utente \> *) se si trovano in computer diversi nello stesso dominio.  
  
 Il server di report creerà un account di accesso al database e assegnerà le autorizzazioni per il database all'account specificato.  
  
 Il server di report non crea l'account stesso. L'account specificato deve essere già presente e valido per la configurazione della distribuzione. In particolare, se il database si trova in un computer remoto e si desidera utilizzare un account di Windows, è necessario specificare un account che disponga di autorizzazioni di accesso nel computer specifico.  
  
 Se il computer è in un dominio diverso o non trusted, utilizzare un account di accesso al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per ulteriori informazioni sulla scelta di un account, vedere [configurare una connessione del database del server di Report &#40;SSRS Configuration Manager&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
 **Riepilogo**  
 Consente di verificare le impostazioni prima dell'esecuzione della procedura guidata.  
  
 **Continua e termina**  
 Consente di monitorare lo stato di ogni attività.  
  
## <a name="see-also"></a>Vedere anche  
 [Database &#40;modalità nativa SSRS&#41;](../../../2014/sql-server/install/database-ssrs-native-mode.md)   
 [Procedura guidata Cambia database &#40;modalità nativa SSRS&#41;](../../../2014/sql-server/install/change-database-wizard-ssrs-native-mode.md)   
 [Creazione di un database del server di report in modalità nativa &#40;Configuration Manager SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Reporting Services Configuration Manager argomenti della Guida F1 &#40;modalità nativa di SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Configurare una connessione del database del server di report &#40;Gestione configurazione SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
