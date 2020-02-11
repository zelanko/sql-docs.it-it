---
title: Opzioni di configurazione Reporting Services (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.ins.instwizard.reportserverinstoptions.f1
helpviewer_keywords:
- Report Server Installation Options page [SQL Server Installation Wizard]
- report servers [Reporting Services], installing
- SQL Server Installation Wizard, Report Server Installation Options page
ms.assetid: e4561f6c-bc7f-467e-821a-cde8e5cd7391
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 1b54661c47ff40af595be55d444f6c0ffb4bc2cd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952118"
---
# <a name="reporting-services-configuration-options-ssrs"></a>Opzioni di configurazione di Reporting Services (SSRS)
  Usare la pagina **Configurazione di Reporting Services** dell'Installazione guidata di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per specificare le modalità di installazione e di configurazione di un'istanza del server di report. La disponibilità di un'opzione di installazione dipende dalle opzioni scelte in precedenza nella pagina **Selezione funzionalità** e dall'installazione o meno di un'istanza locale del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] contemporaneamente all'installazione del server di report.  
  
 In alcuni casi, se nel computer è installato un certificato Secure Sockets Layer (SSL) associato a un carattere jolly complesso, il programma di installazione creerà gli URL di Reporting Services utilizzando il prefisso HTTPS. Per ulteriori informazioni sulla modalità di mapping dei certificati agli URL Reporting Services, vedere [configurazione di un server di report per le connessioni SSL (Secure Sockets Layer)](https://go.microsoft.com/fwlink/?LinkId=199089) (https://go.microsoft.com/fwlink/?LinkId=199089) in documentazione online di SQL Server.  
  
 Per le informazioni più recenti relative [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a e all'installazione e alla configurazione di questa versione, vedere [informazioni aggiuntive sull'installazione](https://go.microsoft.com/fwlink/?LinkId=207425) https://go.microsoft.com/fwlink/?LinkId=207425).  
  
## <a name="options"></a>Opzioni  
  
### <a name="reporting-services-native-mode"></a>Modalità nativa di Reporting Services  
 Se non è possibile eseguire la configurazione predefinita del server di report poiché uno o più requisiti non vengono soddisfatti, l'Installazione guidata consentirà solo l'opzione di installazione minima. Al termine dell'installazione, sarà possibile copiare i file necessari e utilizzare Gestione configurazione Reporting Services per configurare un server di report in modalità nativa.  
  
> [!NOTE]  
>  La presenza di un file di database del server di report può impedire l'installazione se si seleziona una delle opzioni di installazione predefinite. Quando si seleziona un'opzione di installazione predefinita, il programma di installazione tenta di creare un database del server di report utilizzando il nome predefinito. Se è già presente un database con lo stesso nome, l'installazione avrà esito negativo e sarà necessario eseguirne il rollback. Per evitare questo problema, è possibile rinominare il database esistente prima di eseguire l'installazione oppure selezionare l'opzione **Solo installazione** in modo da poter specificare impostazioni personalizzate per il database al termine dell'installazione.  
  
#### <a name="install-and-configure"></a>Installare e configurare  
 Consente di installare un'istanza del server di report in modalità nativa utilizzando i valori predefiniti per i database del server di report, l'account del servizio e le prenotazioni di URL. Se si sceglie questa opzione, l'istanza del server di report è pronta per essere utilizzata al termine dell'installazione. Durante l'installazione viene creato un database del server di report utilizzando un'istanza locale di [!INCLUDE[ssDE](../../includes/ssde-md.md)] e viene configurato un server di report per l'utilizzo dei valori predefiniti.  
  
 Questa opzione è disponibile solo se i valori predefiniti utilizzati nell'installazione di un server di report sono validi per il sistema. Questa opzione è consigliabile per gli sviluppatori che desiderano installare tutti i componenti localmente e per gli utenti che desiderano valutare il software.  
  
 Per visualizzare le informazioni relative alle impostazioni predefinite usate durante l'installazione o per individuare i motivi per cui è impossibile installare la configurazione predefinita, fare clic su **Dettagli**. Per ulteriori informazioni sulla configurazione predefinita per un server di report in modalità nativa, vedere [configurazione predefinita per un'installazione in modalità nativa (Reporting Services)](https://go.microsoft.com/fwlink/?LinkId=199091) (https://go.microsoft.com/fwlink/?LinkId=199091).  
  
#### <a name="install-only"></a>Solo installazione  
 Consente di installare i file di programma del server di report, di creare l'account del servizio del server di report e di registrare il provider di Strumentazione gestione Windows (WMI) per il server di report. Questa opzione di installazione viene definita installazione di tipo "solo file". Selezionare questa opzione se non si desidera utilizzare la configurazione predefinita. Se la configurazione predefinita non può essere installata o se si esegue l'installazione di un cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che include [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], questa è l'unica opzione disponibile. Per ulteriori informazioni su un'installazione di solo file, vedere [installazione di solo file (Reporting Services)](https://go.microsoft.com/fwlink/?LinkId=199093) (https://go.microsoft.com/fwlink/?LinkId=199093).  
  
 Al termine dell'installazione, è necessario creare il database del server di report e configurare quest'ultimo prima di utilizzarlo. Per configurare un server di report e creare il database, utilizzare Gestione configurazione Reporting Services. Per ulteriori informazioni, vedere [procedura: creazione di un database del server di report (configurazione Reporting Services)](https://go.microsoft.com/fwlink/?LinkId=199094) (https://go.microsoft.com/fwlink/?LinkId=199094) e [configurazione di una connessione al database del server di report](https://go.microsoft.com/fwlink/?LinkId=199095) (https://go.microsoft.com/fwlink/?LinkId=199095)).  
  
### <a name="reporting-services-sharepoint-mode"></a>Modalità SharePoint di Reporting Services  
  
#### <a name="install-only"></a>Solo installazione  
 Consente di installare i file di programma del server di report e i cmdlet di PowerShell. Al termine dell'installazione, sarà necessario avviare SharePoint Services per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e creare un'applicazione di servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per altre informazioni, vedere quanto riportato di seguito.  
  
-   [Installazione di Reporting Services server di report in modalità SharePoint per Power View e avvisi dati](https://go.microsoft.com/fwlink/?LinkId=207543) (https://go.microsoft.com/fwlink/?LinkId=207543).  
  
-   [Installare Reporting Services modalità SharePoint come una singola farm di server](https://go.microsoft.com/fwlink/?LinkId=207544) (https://go.microsoft.com/fwlink/?LinkId=207544).  
  
-   [Reporting Services server di report (SSRS)](https://go.microsoft.com/fwlink/?LinkID=207244) (https://go.microsoft.com/fwlink/?LinkID=207244).  
  
## <a name="installing-the-reporting-services-add-in-for-sharepoint-technologies"></a>Installazione del componente aggiuntivo Reporting Services per le tecnologie SharePoint  
 A partire dalla versione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , è possibile installare il componente aggiuntivo come parte dell'installazione di SQL Server, nella pagina Selezione funzionalità dell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 È tuttavia possibile installare il componente aggiuntivo di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per SharePoint 2010 mediante uno dei metodi seguenti:  
  
-   Eseguire lo strumento di preparazione dei prodotti SharePoint 2010 **PreRequisiteInstaller.exe**.  
  
-   Eseguire l'installazione dal supporto di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Fare clic sul file **rsSharePoint.msi** nella cartella Setup nel supporto di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al termine dell'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Scaricare e installare il componente aggiuntivo. Per ulteriori informazioni, vedere [la posizione in cui trovare il componente aggiuntivo Reporting Services per prodotti SharePoint](https://go.microsoft.com/fwlink/?LinkID=208634) (https://go.microsoft.com/fwlink/?LinkID=208634).  
  
## <a name="see-also"></a>Vedere anche  
 [Avvia Reporting Services Configuration Manager](https://go.microsoft.com/fwlink/?LinkId=199096)   
 [Creazione di un database del server di report (configurazione Reporting Services)](https://go.microsoft.com/fwlink/?LinkId=199094)   
 [Aggiornare ed eseguire la migrazione Reporting Services](https://go.microsoft.com/fwlink/?LinkID=245628)   
 [Installazione dal prompt dei comandi delle modalità SharePoint e nativa di Reporting Services](https://go.microsoft.com/fwlink/?LinkId=217620)  
  
  
