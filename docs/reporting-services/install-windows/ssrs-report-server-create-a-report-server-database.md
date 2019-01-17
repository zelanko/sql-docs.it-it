---
title: Creare un database del server di report (Gestione configurazione SSRS) | Microsoft Docs
author: markingmyname
ms.author: maghan
manager: kfile
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/12/2018
ms.openlocfilehash: a893b213b5678fa1c5cea7f4735da239bdf01048
ms.sourcegitcommit: 40c3b86793d91531a919f598dd312f7e572171ec
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53328741"
---
# <a name="create-a-report-server-database"></a>Creare un database del server di report

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **modalità nativa** usa due database relazionali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'archiviazione di metadati e oggetti del server di report. Un database è utilizzato per l'archiviazione primaria e l'altro per l'archiviazione dei dati temporanei. I database vengono creati assieme e associati in base al nome. Con un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinita, i database sono denominati **reportserver** e **reportservertempdb**. I due database vengono detti collettivamente "database del server di report" o "catalogo del server di report".

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **modalità SharePoint** include un terzo database usato per i metadati di avviso dei dati. I tre database vengono creati per ogni applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e nei nomi dei database è incluso, per impostazione predefinita, un GUID che rappresenta l'applicazione di servizio. Di seguito sono riportati nomi di esempio dei tre database della modalità SharePoint:

- ReportingService_90a9f37075544f22953c4a62e4a9f370  
  
- ReportingService_90a9f37075544f22953c4a62e4a9f370TempDB  
  
- ReportingService_90a9f37075544f22953c4a62e4a9f370_Alerting  
  
> [!IMPORTANT]  
> Non scrivere applicazioni che eseguono query sul database del server di report. Il database del server di report non è uno schema pubblico. La struttura della tabella potrebbe cambiare da una versione all'altra. Se si scrive un'applicazione che richiede l'accesso al database del server di report, utilizzare sempre le API di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per accedere al database del server di report.  
> L'eccezione a questa situazione è rappresentata dalle viste del log di esecuzione. Per altre informazioni, vedere [Vista ExecutionLog ed ExecutionLog3 del server di report](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)  
  
## <a name="ways-to-create-the-report-server-database"></a>Creazione del database del server di report

 **Modalità nativa:** è possibile creare il database del server di report in modalità nativa nei modi seguenti:  
  
- Automatico: usare la configurazione guidata di SQL Server, se si sceglie l'opzione di installazione della configurazione predefinita. Nell'Installazione guidata di SQL Server, si tratta dell'opzione **Installazione e configurazione** disponibile nella pagina delle opzioni di installazione del server di report. Se si sceglie l'opzione **Solo installazione** , è necessario usare Gestione configurazione Reporting Services per creare il database.  
  
- Manuale: usare Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. È necessario creare manualmente il database del server di report se per ospitare il database si utilizza un [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] remoto. Per altre informazioni, vedere [Creare un database del server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
 **Modalità SharePoint:** nella pagina delle opzioni di installazione del server di report è disponibile la sola opzione **Solo installazione** per la modalità SharePoint. Questa opzione consente di installare tutti i file di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e il servizio condiviso [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Il passaggio successivo prevede la creazione di almeno un'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in una delle modalità seguenti:  
  
- Utilizzare Amministrazione centrale SharePoint per creare un'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per altre informazioni vedere la sezione relativa all'applicazione di servizio in [Passaggio 3: Creare un'applicazione di servizio Reporting Services](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md#bkmk_create_serrviceapplication).  
  
- Utilizzare i cmdlet PowerShell [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per creare un'applicazione di servizio e i database del server di report. Per altre informazioni, vedere l'esempio per la creazione di applicazioni di servizio nell'argomento [Cmdlet di PowerShell per la modalità SharePoint di Reporting Services](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  
  
## <a name="database-server-version-requirements"></a>Requisiti relativi alla versione del server di database

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene usato per ospitare i database del server di report. L'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] può essere un'istanza locale o remota. Di seguito sono riportate le versioni supportate del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] che possono essere utilizzate per ospitare i database del server di report:  
  
- [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
- [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
- [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
- [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
- [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 Per creare il database del server di report in un computer remoto, è necessario configurare la connessione per l'utilizzo di un account utente di dominio o un account di servizio con accesso alla rete. Se si sceglie di utilizzare un'istanza remota di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , valutare attentamente le credenziali che il server di report dovrà utilizzare per connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Configurare una connessione del database del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
> [!IMPORTANT]  
> Il server di report e l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ospita il database del server di report possono trovarsi in domini diversi. Per la distribuzione in Internet, è pratica comune utilizzare un server protetto da firewall. Se si configura un server di report per l'accesso a Internet, utilizzare credenziali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per connettersi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] protetta dal firewall e utilizzare IPSEC per proteggere la connessione.  
  
## <a name="database-server-edition-requirements"></a>Requisiti relativi all'edizione del server di database

 Quando si crea un database del server di report, tenere presente che non tutte le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere usate per ospitare il database. Per altre informazioni, vedere [Requisiti dell'edizione server del database del server di report](../reporting-services-features-supported-by-the-editions-of-sql-server-2016.md#report-server-database-server-edition-requirements) di [Funzionalità di Reporting Services supportate dalle edizioni di SQL Server 2017](../reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).  

## <a name="next-steps"></a>Passaggi successivi

[Gestione configurazione Reporting Services](https://msdn.microsoft.com/63519ef4-e68a-42fb-9cf7-31228ea4e434)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
