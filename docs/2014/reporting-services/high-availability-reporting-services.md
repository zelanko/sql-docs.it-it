---
title: Disponibilità elevata (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], Reporting Services
- high availability [Reporting Services]
- Reporting Services, high availability
ms.assetid: 50e0813f-f591-4688-9cd1-e6389a3808e5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8bc05f1f669597229a3a07d6ce8487eb19a77201
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63261160"
---
# <a name="high-availability-reporting-services"></a>Disponibilità elevata (Reporting Services)
  Un server di report di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] è un server senza stato (stateless) in cui vengono archiviati dati dell'applicazione, contenuto, proprietà e informazioni sulla sessione in due database relazionali di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . In questa situazione, il modo più efficiente per garantire la disponibilità delle funzionalità di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] consiste nell'esecuzione delle operazioni seguenti:  
  
-   Utilizzare le caratteristiche a disponibilità elevata del [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] per ottimizzare il tempo di attività dei database del server di report. Se si configura un'istanza del [!INCLUDE[ssDE](../includes/ssde-md.md)] per l'esecuzione in un cluster di failover, è possibile selezionarla quando si crea un database del server di report.  
  
-   Utilizzare, per quanto possibile, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../includes/sshadr-md.md)] con i database di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e per le origini dati. Per altre informazioni, vedere [Reporting Services con i gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md).  
  
-   Configurare più server di report in modo che vengano eseguiti in una distribuzione con scalabilità orizzontale, in cui tutti i server condividono un unico database del server di report. La distribuzione di più istanze del server di report, preferibilmente in server diversi, con scalabilità orizzontale consente di non interrompere il servizio ininterrotto nel caso in cui una delle istanze del server di report si arresti.  
  
 Una distribuzione con scalabilità orizzontale consente di condividere un database. Se uno server di report si arresta, gli altri server nella stessa distribuzione continueranno a funzionare.  
  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non riesce a interagire con i cluster. Di per sé, una distribuzione con scalabilità orizzontale non fornisce il bilanciamento carico e non rileva i carichi di elaborazione su un server di report né invia le nuove richieste di elaborazione al server meno occupato. Tale distribuzione inoltre non reindirizza le richieste di elaborazione che non state completate in modo corretto. Per ottenere il bilanciamento del carico, è necessario configurarlo per i server Web che ospitano i server di report e configurare quindi i server di report in una distribuzione con scalabilità orizzontale in modo che condividano lo stesso database del server di report.  
  
 Il servizio Web ReportServer e il servizio Windows sono strettamente integrati e vengono eseguiti insieme come una sola istanza del server di report. Non è possibile configurare separatamente la disponibilità per uno dei due servizi.  
  
## <a name="see-also"></a>Vedere anche  
 [Soluzioni a disponibilità elevata &#40;SQL Server&#41;](../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Configurare una distribuzione con scalabilità orizzontale di un server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)  
  
  
