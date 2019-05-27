---
title: Segnala lo stato del Server (modalità nativa SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.serverstatus.F1
ms.assetid: 2f63ad1c-1bc2-449d-b451-fb39a0060838
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0d9f59bde50c325f0694cc6cdd9441d80ea61f02
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092702"
---
# <a name="report-server-status-ssrs-native-mode"></a>Stato del server di report (modalità nativa SSRS)
  Utilizzare questa pagina per visualizzare le informazioni sull'istanza del server di report a cui si è attualmente connessi. Questa rappresenta la pagina iniziale per la configurazione del server di report. Ulteriori pagine sono disponibili per configurare gli URL, l'account del servizio, il database del server di report, il recapito tramite posta elettronica del server di report, la distribuzione con scalabilità orizzontale e le chiavi di crittografia.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Per aprire questa pagina, avviare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e connettersi all'istanza del server di report. Per altre informazioni, vedere [Gestione configurazione Reporting Services &#40;CANC&#41;](reporting-services-configuration-manager-native-mode.md).  
  
> [!TIP]  
>  Il[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager (RSConfigTool.exe) viene installato con un livello di privilegio "highestAvailable". Questo comportamento si verifica per motivi strutturali. Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] richiede la comunicazione con le API di WMI per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Una parte della comunicazione di WMI per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] richiede un livello superiore o privilegi amministrativi.  
  
 Se si effettua una connessione al server di report e tutti i collegamenti alle pagine sono visualizzati in grigio, verificare che il servizio del server di report sia stato avviato. Il **segnalare lo stato del servizio:** Deve essere "avviato". Per verificare lo stato del servizio è possibile utilizzare anche l'applicazione console Servizi in Strumenti di amministrazione.  
  
## <a name="options"></a>Opzioni  
 **Istanza di SQL Server**  
 Consente di visualizzare informazioni sull'istanza del server di report alla quale si è attualmente connessi. I nomi delle istanze del server di report si basano sulle istanze denominate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . L'istanza predefinita è MSSQLSERVER. Un'istanza denominata è un valore specificato durante l'installazione. Per ulteriori informazioni sulle istanze, vedere [lavorare con più versioni e istanze di SQL Server](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
> [!NOTE]  
>  In SQL Server Express with Advanced Services l'istanza predefinita è SQLExpress.  
  
 **ID istanza**  
 Corrisponde a una cartella nel file system in cui sono archiviati i file di programma per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a cui si è connessi. Il valore **ID istanza** viene assegnato dal programma di installazione nel formato *componente*.*istanza*, dove *componente* è un valore che significa un componente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e *istanza* è un nome di istanza. Il nome dell'istanza predefinita è MSSQLSERVER. Se ad esempio si installano istanze predefinite dei componenti [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , i nomi delle cartella corrispondenti sono:  
  
-   MSSQL12.MSSQLSERVER  
  
-   MSAS12.MSSQLSERVER  
  
-   MSRS12.MSSQLSERVER  
  
 Se si installa una seconda istanza di un componente già installato, ad esempio il [!INCLUDE[ssDE](../../includes/ssde-md.md)], e si assegna all'istanza il nome Contoso, il valore di **ID istanza** sarà MSSQL12.Contoso.  
  
 **Edizione**  
 Consente di visualizzare le informazioni sull'edizione. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Funzionalità supportate dalle edizioni di SQL Server](https://go.microsoft.com/fwlink/?linkid=232473).  
  
 **Versione prodotto**  
 Viene visualizzata la versione installata di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 **Database del server di report**  
 Consente di visualizzare il nome del database del server di report in cui sono archiviati i dati dell'applicazione per l'istanza del server di report corrente.  
  
 **Modalità Server di report**  
 Tramite questa opzione deve essere sempre visualizzato un valore di **Nativa**. Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] supporta solo server di report in modalità nativa. Se si visualizza un valore della **modalità integrata SharePoint**, è possibile che la distribuzione in modalità nativa non sia configurata correttamente, pertanto è necessario connettersi a un catalogo del report in modalità nativa. Utilizzare la pagina **Database** di Gestione configurazione per modificare il database e creare un nuovo database o connettersi a un catalogo del database del server di report in modalità nativa esistente.  
  
 **Stato server**  
 Indica se il servizio del server di report è in esecuzione.  
  
 **Start**  
 Consente di avviare il servizio del server di report. Il riavvio del servizio è necessario dopo avere apportato alcune modifiche di configurazione, ad esempio quando si riconfigura un server di report in seguito alla modifica del nome di un computer. Se si riconfigurano le prenotazioni URL, il servizio verrà riavviato automaticamente. Il riavvio è necessario per rendere effettive le modifiche.  
  
 **Arresta**  
 Consente di arrestare il servizio del server di report. L'arresto del servizio causa l'interruzione del funzionamento del server di report. Per altre informazioni, vedere [avviare e arrestare il servizio ReportServer](../../reporting-services/report-server/start-and-stop-the-report-server-service.md) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
## <a name="see-also"></a>Vedere anche  
 [Gli argomenti della Guida F1 di Gestione configurazione di Reporting Services &#40;modalità nativa SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Gestione configurazione Reporting Services &#40;/del&#41;](/sql/2014/sql-server/install/reporting-services-configuration-manager-native-mode)   
 [Inizializzare un server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)  
  
  
