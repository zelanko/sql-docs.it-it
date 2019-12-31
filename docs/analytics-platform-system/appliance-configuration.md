---
title: Elenchi di controllo di configurazione
description: Fornisce elenchi di controllo per le attività necessarie per configurare il sistema di piattaforma di analisi per il proprio ambiente. Queste attività di configurazione sono necessarie prima di poter usare l'appliance.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 80fc899400be167badaae9d617d43a61e0d346b5
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401459"
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>Elenchi di controllo della configurazione dell'appliance per il sistema di piattaforma Analytics
Fornisce elenchi di controllo per le attività necessarie per configurare il sistema di piattaforma di analisi per il proprio ambiente. Queste attività di configurazione sono necessarie prima di poter usare l'appliance.  
  
> [!WARNING]  
> L'uso del sistema di piattaforma di analisi**Configuration Manager** rappresenta il modo migliore e l'unico modo supportato per eseguire le attività disponibili nello strumento.  
  
## <a name="BeforeTasks"></a>Prima di iniziare  
  
### <a name="prerequisites"></a>Prerequisiti  
  
1.  Il dispositivo deve essere installato nel data center e acceso.  
  
2.  Assicurarsi di avere le informazioni seguenti, fornite dalla IHV:  
  
    -   Indirizzo IP esterno per il nodo di controllo PDW (*PDW_region-* CTL01)  
  
    -   Nome di dominio dell'appliance  
  
    -   Nome utente e password per l'amministratore di dominio del dispositivo  
  
3.  Ottenere un certificato attendibile. Questa operazione verrà importata in un passaggio successivo per consentire ai client di connettersi alla **console di amministrazione** con connessioni sicure. Salvare il certificato nel nodo di controllo in un file PFX protetto da password.  
  
4.  Avviare il **Configuration Manager**attenendosi alla procedura seguente:  
  
    1.  Usare **Desktop remoto** per connettersi al nodo di controllo PDW (*PDW_region*-CTL01). Potrebbe essere necessario connettersi con l'indirizzo IP esterno per CTL01.  
  
    2.  Avviare il **Configuration Manager** dal menu **Start** del nodo di controllo PDW. La prima schermata del Configuration Manager Visualizza la topologia dell'appliance, creata da IHV. Si tratta di un elenco dei nodi hardware riconosciuti dal software SQL Server PDW come parte del dispositivo. Non è necessario modificare le impostazioni nella schermata della topologia dell'appliance.  
  
## <a name="CMTasks"></a>Eseguire attività Configuration Manager  
Il SQL Server PDW**Configuration Manager** (PDWCM) è uno strumento di amministrazione dell'appliance che SQL Server PDW amministratori di sistema usano per eseguire operazioni a livello di appliance e per modificare le impostazioni a livello di dispositivo. Ad esempio, usare PDWCM per reimpostare le password, impostare il fuso orario, modificare gli indirizzi IP, configurare i certificati SSL, abilitare l'accesso remoto tramite il firewall, avviare o arrestare l'appliance e impostare l'inizializzazione immediata dei file.  
  
Utilizzare **Configuration Manager** per eseguire le attività di configurazione seguenti.  
  
|Attività di configurazione|Description|  
|----------------------|---------------|  
|Acquisire familiarità con i nomi dei componenti fisici|[Componenti fisici di infrastruttura PDW e appliance &#40;sistema di piattaforma di analisi&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|Avvia SQL Server PDW Configuration Manager|[Avviare la piattaforma Configuration Manager &#40;Analytics System&#41;](launch-the-configuration-manager.md)|  
|Modificare la password dell'amministratore di dominio|Il dispositivo dispone di un Active Directory Domain Services di Windows privato usato per autenticare i nodi all'interno dell'appliance.<br /><br />Il IHV configurare l'appliance con una password di amministratore di dominio predefinita. Questa operazione deve essere cambiata in una password sicura.<br /><br />Il **Configuration Manager** è l'unico modo supportato per modificare la password dell'amministratore di dominio.<br /><br />Per ulteriori informazioni, vedere la pagina relativa alla [reimpostazione della Password &#40;&#41;di sistema della piattaforma Analytics ](password-reset.md).|  
|Modificare la password per l'accesso **sa**|SQL Server PDW dispone di un accesso amministratore di sistema denominato **sa**. L'accesso **sa** ha tutti i privilegi. Può concedere, negare o revocare qualsiasi autorizzazione. È anche possibile visualizzare tutte le visualizzazioni di sistema.<br /><br />Per ulteriori informazioni, vedere la pagina relativa alla [reimpostazione della Password &#40;&#41;di sistema della piattaforma Analytics ](password-reset.md).|  
|Impostare il fuso orario del dispositivo|Impostare l'ora (locale o altra ora desiderata) per tutti i nodi del dispositivo.<br /><br />Per altre informazioni, vedere [configurazione del fuso orario del dispositivo &#40;piattaforma ](appliance-time-zone-configuration.md)di strumenti di analisi&#41;di sistema.|  
|Specificare le impostazioni di rete rivolte all'esterno per l'appliance SQL Server PDW|[Configurazione di rete Appliance &#40;sistema della piattaforma di analisi&#41;](appliance-network-configuration.md)|  
|Importare un certificato di sicurezza per la console di amministrazione|Un certificato può fornire connessioni SSL (Secure Sockets Layer) tramite HTTPS al [monitoraggio dell'appliance tramite la console di amministrazione &#40;&#41;di sistema della piattaforma di analisi ](monitor-the-appliance-by-using-the-admin-console.md). Per impostazione predefinita, la **console di amministrazione** include un certificato autofirmato che fornisce privacy, ma non l'autenticazione server. Questo certificato restituisce anche un errore in Internet Explorer: "si è verificato un problema con il certificato di sicurezza del sito Web" quando l'utente si connette. Sebbene questa connessione crittografa i dati in corso tra il client e il server, la connessione è ancora a rischio da utenti malintenzionati.<br /><br />SQL Server PDW gli amministratori devono acquisire immediatamente un certificato concatenato a un'autorità di certificazione attendibile riconosciuta dai client, per disporre di una connessione protetta e rimuovere l'errore segnalato da Internet Explorer. Questa operazione richiede un nome di dominio completo che esegue il mapping dell'indirizzo IP virtuale (scelta consigliata) del nodo di controllo o un nome di certificato che corrisponda al valore digitato dagli utenti nelle barre degli indirizzi del browser per accedere alla console di amministrazione.<br /><br />Usare il **Configuration Manager** per aggiungere o rimuovere certificati attendibili. Lo strumento di configurazione dei certificati dei servizi HTTP di Microsoft`winHttpCertCfg.exe`Windows () per gestire i certificati non è supportato.<br /><br />Per altre informazioni, vedere [PDW certificate provisioning &#40;Analytics Platform System&#41;](pdw-certificate-provisioning.md).|
|Opzione funzionalità|Visualizza informazioni sulle opzioni di funzionalità introdotte in Analytics Platform System AU7. Usare questa pagina per aggiornare o abilitare/disabilitare le funzionalità e le impostazioni in Analytics Platform System. Per modificare i valori delle opzioni di funzionalità è necessario riavviare il servizio.<br /><br />Per altre informazioni, vedere [opzione di funzionalità PDW &#40;&#41;di sistema della piattaforma di analisi ](appliance-feature-switch.md).|
|Abilitare o disabilitare Windows Firewall regole che consentono o impediscono l'accesso a porte specifiche sul dispositivo SQL Server PDW.|Il IHV configurerà e consentirà le regole del firewall necessarie per il corretto funzionamento dell'appliance. Nella maggior parte dei casi non sarà possibile abilitare o disabilitare le regole del firewall.<br /><br />Per ulteriori informazioni, vedere la pagina relativa alla [configurazione del firewall PDW &#40;&#41;di sistema della piattaforma di analisi ](pdw-firewall-configuration.md).|  
|Avviare e arrestare il dispositivo SQL Server PDW|Arresta o avvia l'appliance SQL Server PDW. Per ulteriori informazioni, vedere la pagina relativa [allo stato dei servizi PDW &#40;&#41;di sistema della piattaforma di analisi ](pdw-services-status.md).|  
|Esaminare le opzioni di inizializzazione immediata dei file utilizzando la finestra di dialogo **privilegi**|L'inizializzazione immediata dei file è una funzionalità SQL Server che consente l'esecuzione più rapida delle operazioni sui file di dati. È abilitata nei SQL Server PDW solo se all'account del servizio di rete è stato concesso il privilegio SE_MANAGE_VOLUME_NAME. È disattivata per impostazione predefinita.<br /><br />Per ulteriori informazioni, vedere [configurazione dell'inizializzazione immediata dei File &#40;&#41;del sistema della piattaforma di analisi ](instant-file-initialization-configuration.md).|  
|Ripristinare il database master da un backup|Elimina il database **Master** corrente e lo sostituisce con un backup. Per ulteriori informazioni, vedere [Restore the Master Database &#40;Analytics Platform System&#41;](restore-the-master-database.md).|  
  
## <a name="AddTasks"></a>Eseguire attività di configurazione aggiuntive  
Dopo aver eseguito le attività di **Configuration Manager** , eseguire il seguente elenco di attività di configurazione aggiuntive. Alcune di queste attività sono facoltative.  
  
|Attività di configurazione|Description|  
|----------------------|---------------|  
|Il software antivirus di terze parti può essere installato e configurato nell'appliance di SQL Server PDW per i nodi rivolte all'esterno.<br /><br />(Facoltativa)|Per ulteriori informazioni, vedere la pagina relativa al [&#41;del sistema &#40;Analytics del software antivirus ](antivirus-software.md).|  
|La password per la modalità ripristino servizi directory può essere modificata.<br /><br />(Facoltativa)|Per ulteriori informazioni, vedere la pagina relativa alla [configurazione della password amministratore per l'accesso ai nodi ad in modalità ripristino servizi Directory &#40;ripristino servizi directory&#41; &#40;&#41;di sistema della piattaforma ](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md).|  
|Configurare l'appliance per la ricezione degli aggiornamenti software<br /><br />(Consigliato)|Il dispositivo deve essere configurato in modo da ricevere gli aggiornamenti per la SQL Server PDW e il software sottostante.<br /><br />Per ulteriori informazioni, vedere [Configure Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md). Per informazioni su WSUS, vedere la pagina relativa al [&#41;del sistema della piattaforma &#40;Analytics ](software-servicing.md).|  
|Configurare la connettività a dati esterni, ad esempio Hadoop o archiviazione BLOB di Azure.<br /><br />(Facoltativa)|Per altre informazioni, vedere [configurare la connettività di base per i dati esterni &#40;&#41;di sistema della piattaforma di analisi ](configure-polybase-connectivity-to-external-data.md).|  
|Configurare il software antivirus<br /><br />(Facoltativa)|Le soluzioni antivirus di terze parti possono essere usate per proteggere i nodi rivolte all'esterno, ma non è obbligatorio. Attenersi alle linee guida riportate in.|  
|Configurare le schede di rete InfiniBand nei server di backup e di caricamento<br /><br />(Facoltativa)|Per configurare il backup e il caricamento dei server per la connessione a SQL Server PDW tramite la rete InfiniBand, è necessario configurare le schede di rete per consentire al DNS dell'appliance di risolvere la connessione InfiniBand alla rete InfiniBand attualmente attiva.|  
|Configurare per inviare i dati di telemetria a Microsoft<br /><br />(Facoltativa)|Per configurare Analytics Platform System per l'invio di dati di telemetria a Microsoft, è necessario eseguire uno script di PowerShell nel nodo di controllo. Per istruzioni specifiche, vedere [inviare il feedback di telemetria a Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md).|  
  
## <a name="see-also"></a>Vedere anche  
[Software antivirus &#40;piattaforma del sistema di analisi&#41;](antivirus-software.md)  
[Configurare le schede di rete InfiniBand &#40;SQL Server PDW&#41;](configure-infiniband-network-adapters.md)  
  
