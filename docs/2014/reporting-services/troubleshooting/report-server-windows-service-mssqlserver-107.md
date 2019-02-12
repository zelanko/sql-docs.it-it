---
title: Servizio Windows ReportServer (MSSQLServer) 107 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- MSSQLServer 107 error
ms.assetid: 52b5704b-27f9-400a-a821-d8fa0786afe4
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5351b052a26b2a4f5b9bc9d91f93aa2e4cdc5357
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020283"
---
# <a name="report-server-windows-service-mssqlserver-107"></a>Servizio Windows ReportServer (MSSQLServer) 107
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|107|  
|Origine evento|Servizio Windows ReportServer|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Testo del messaggio|Il servizio Windows ReportServer (MSSQLSERVER) non è in grado di connettersi al database del server di report.|  
  
## <a name="explanation"></a>Spiegazione  
 Il servizio del server di report di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è in grado di connettersi al database del server di report. Questo errore si verifica durante un riavvio del servizio se non è possibile stabilire una connessione al database del server di report. Di seguito vengono riportate le condizioni in presenza delle quali si verifica l'errore:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] non è in esecuzione quando il servizio del server di report viene avviato.  
  
-   Non è possibile eseguire la connessione al servizio [!INCLUDE[ssDE](../../includes/ssde-md.md)] perché le connessioni remote o il protocollo TCP/IP non è abilitato.  
  
-   Il database del server di report non è configurato in modo corretto.  
  
-   L'account di servizio non è configurato correttamente o l'account non dispone più di autorizzazioni sul database del server di report. Questa situazione può verificarsi se non si utilizza lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per configurare l'account o il database del server di report.  
  
## <a name="user-action"></a>Azione dell'utente  
 Avviare il servizio [!INCLUDE[ssDE](../../includes/ssde-md.md)] se non è in esecuzione e verificare che le connessioni remote siano abilitate per il protocollo TCP/IP.  
  
 Utilizzare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per configurare il database del server di report e l'account di servizio.  
  
## <a name="internal-only"></a>Solo interno  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Avviare e arrestare il servizio del server di report](../report-server/start-and-stop-the-report-server-service.md)  
  
  
