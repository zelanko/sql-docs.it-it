---
title: Servizio Windows ReportServer (MSSQLServer) 107 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- MSSQLServer 107 error
ms.assetid: 52b5704b-27f9-400a-a821-d8fa0786afe4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a7751fdc3e04f25b80b4f95dfc26abb8a0844a92
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66099299"
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
  
  
