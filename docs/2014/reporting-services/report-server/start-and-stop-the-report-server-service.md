---
title: Avviare e arrestare il servizio del server di report | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- stopping Report Server service
- Report Server Windows service, starting
- Report Server service, starting
- starting Report Server service
ms.assetid: 6ec69ac3-27b0-472d-91e1-733af9078ed2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f4bd22faaa9d0f3b6ce213c37e20615492b1e95d
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59968337"
---
# <a name="start-and-stop-the-report-server-service"></a>Avviare e arrestare il servizio del server di report
  Un server di report viene implementato come un servizio Windows che contiene il servizio Web ReportServer, Gestione report e un'applicazione di elaborazione in background. Se si desidera utilizzare qualsiasi funzionalità del server di report, è necessario che il servizio sia in esecuzione. L'arresto del servizio determina l'interruzione di tutte le operazioni eseguite sul server di report.  
  
 Mentre il servizio è arrestato, le richieste di elaborazione di report e sottoscrizioni pianificate che sarebbero state eseguite in caso di attività del servizio vengono aggiunte alla coda. Questa situazione si verifica poiché i processi eseguiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent creano gli eventi. Se si desidera evitare un backlog di operazioni mentre il servizio è disattivato, arrestare anche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 Per avviare e arrestare il servizio del server di report, è possibile utilizzare diversi strumenti, ad esempio lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e lo strumento Servizi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Se, oltre ad avviare o arrestare il servizio, si modifica ad esempio l'account del servizio, è necessario utilizzare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . L'utilizzo di altri strumenti per modificare l'account del servizio può causare l'interruzione dell'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per altre informazioni, vedere [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
 Non è possibile sospendere e riprendere l'esecuzione del servizio. Non sono disponibili parametri di avvio. Sebbene non esistano dipendenze esplicite, se il server di report deve supportare sottoscrizioni o operazioni su report pianificate, è necessario che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia in esecuzione.  
  
### <a name="to-start-or-stop-the-service-using-the-reporting-services-configuration-tool"></a>Per avviare o arrestare il servizio utilizzando lo strumento di configurazione di Reporting Services  
  
1.  Avviare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e connettersi al server di report.  
  
2.  Nella pagina Stato Server report fare clic su **Arresta** o **Avvia**.  
  
### <a name="to-start-or-stop-the-service-using-services-in-administrative-tools"></a>Per avviare o arrestare il servizio utilizzando lo strumento Servizi in Strumenti di amministrazione  
  
-   In Strumenti di amministrazione aprire Servizi, fare clic con il pulsante destro del mouse su **SQL Server Reporting Services (MSSQLSERVER)**, quindi scegliere **Arresta** o **Riavvia**.  
  
 Se si eseguono più istanze o se il server di report è in esecuzione come istanza denominata, verificare che il nome dell'istanza tra parentesi corrisponda all'istanza del server di report da arrestare o riavviare.  
  
### <a name="to-start-or-stop-the-service-using-sql-server-configuration-manager"></a>Per arrestare e riavviare il servizio utilizzando Gestione configurazione SQL Server.  
  
1.  Avviare Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Selezionare Servizi di SQL Server, fare clic con il pulsante destro del mouse su **SQL Server Reporting Services**, quindi scegliere **Arresta** o **Riavvia**.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
