---
title: Avviare e arrestare il servizio del server di report | Microsoft Docs
ms.date: 05/21/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- stopping Report Server service
- Report Server Windows service, starting
- Report Server service, starting
- starting Report Server service
ms.assetid: 6ec69ac3-27b0-472d-91e1-733af9078ed2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6463dc7e4b17992138a61e6a37277149fccfda68
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66270197"
---
# <a name="start-and-stop-the-report-server-service"></a>Avviare e arrestare il servizio del server di report

  Un server di report viene implementato come un servizio Windows che contiene il servizio Web ReportServer, il portale Web e un'applicazione di elaborazione in background. Se si desidera utilizzare qualsiasi funzionalità del server di report, è necessario che il servizio sia in esecuzione. L'arresto del servizio determina l'interruzione di tutte le operazioni eseguite sul server di report.  
  
 Mentre il servizio è arrestato, le richieste di elaborazione di report e sottoscrizioni pianificate che sarebbero state eseguite in caso di attività del servizio vengono aggiunte alla coda. Questa situazione si verifica poiché i processi eseguiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent creano gli eventi. Se si desidera evitare un backlog di operazioni mentre il servizio è disattivato, arrestare anche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 Per avviare e arrestare il servizio del server di report, è possibile utilizzare diversi strumenti, ad esempio lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e lo strumento Servizi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Se, oltre ad avviare o arrestare il servizio, si modifica ad esempio l'account del servizio, è necessario usare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. L'utilizzo di altri strumenti per modificare l'account del servizio può causare l'interruzione dell'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per altre informazioni, vedere [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
 Non è possibile sospendere e riprendere l'esecuzione del servizio. Non sono disponibili parametri di avvio. Sebbene non esistano dipendenze esplicite, se il server di report deve supportare sottoscrizioni o operazioni su report pianificate, è necessario che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia in esecuzione.  
  
## <a name="use-the-reporting-services-configuration-tool"></a>Usare lo strumento di configurazione di Reporting Services  
  
1. Avviare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e connettersi al server di report.  
  
2. Nella pagina Stato Server report selezionare **Arresta** o **Avvia**.  
  
## <a name="use-administrative-tools"></a>Usare Strumenti di amministrazione  

- In Strumenti di amministrazione aprire Servizi, fare clic con il pulsante destro del mouse su **SQL Server Reporting Services (MSSQLSERVER)** , quindi scegliere **Arresta** o **Riavvia**.  
  
- Se si eseguono più istanze o se il server di report è in esecuzione come istanza denominata, verificare che il nome dell'istanza tra parentesi corrisponda all'istanza del server di report da arrestare o riavviare.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Avvio, arresto o sospensione del servizio SQL Server Agent](https://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)  
  