---
title: Elenchi di controllo configurazione - sistema di piattaforma Analitica | Microsoft Docs
description: Fornisce elenchi di controllo per le attività necessarie per configurare il sistema di piattaforma Analitica per il proprio ambiente. Queste attività di configurazione sono necessari prima di poter usare l'appliance.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: ada3d2f782a33caf5334361a9682c53cf7cdec95
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52398604"
---
# <a name="appliance-configuration-checklists-for-analytics-platform-system"></a>Elenchi di controllo configurazione Appliance per il sistema di piattaforma Analitica
Fornisce elenchi di controllo per le attività necessarie per configurare il sistema di piattaforma Analitica per il proprio ambiente. Queste attività di configurazione sono necessari prima di poter usare l'appliance.  
  
> [!WARNING]  
> Tramite il sistema di piattaforma Analitica**Configuration Manager** è il modo migliore e l'unico modo per eseguire le attività disponibili nello strumento è supportato.  
  
## <a name="BeforeTasks"></a>Prima di iniziare  
  
### <a name="prerequisites"></a>Prerequisiti  
  
1.  L'appliance deve essere installata nel data center e lo spegnimento.  
  
2.  Assicurarsi di avere le informazioni seguenti, che viene fornite dal fornitore IHV:  
  
    -   Indirizzo IP esterno per il nodo di controllo di PDW (*PDW_region -* CTL01)  
  
    -   Nome di dominio di Appliance  
  
    -   Nome utente e password per l'amministratore di dominio del dispositivo  
  
3.  Ottenere un certificato attendibile. Si importerà questo in un passaggio successivo per consentire ai client di connettersi al **Console di amministrazione** con connessioni protette. Salvare il certificato al nodo di controllo in un file PFX protetto da password.  
  
4.  Avviare il **Configuration Manager**, usando la procedura seguente:  
  
    1.  Uso **Desktop remoto** per connettersi al nodo di controllo di PDW (*PDW_region*-CTL01). (Potrebbe essere necessario connettersi con l'indirizzo IP esterno per CTL01)  
  
    2.  Avviare il **Configuration Manager** dalle **avviare** rapida del nodo di controllo di PDW. La prima schermata di Configuration Manager consente di visualizzare la topologia di appliance, che è stata creata dal fornitore IHV. È un elenco dei nodi hardware riconosciuti dal software SQL Server PDW come parte dell'appliance. Non è necessario modificare le impostazioni nella schermata di topologia dello strumento.  
  
## <a name="CMTasks"></a>Eseguire attività di Configuration Manager  
SQL Server PDW**Configuration Manager** (PDWCM) è uno strumento di amministrazione di appliance che gli amministratori di sistema di SQL Server PDW utilizzano per eseguire operazioni a livello di appliance e modificare le impostazioni a livello di dispositivo. Ad esempio, usare PDWCM per reimpostare le password, impostare il fuso orario, modificare gli indirizzi IP, configurare i certificati SSL, abilitare l'accesso remoto attraverso il firewall, avviare o arrestare l'appliance e impostare l'inizializzazione immediata dei File.  
  
Uso **Configuration Manager** per eseguire attività di configurazione seguenti.  
  
|Attività di configurazione|Descrizione|  
|----------------------|---------------|  
|Acquisire familiarità con i nomi di componenti fisici|[Componenti fisici dell'infrastruttura di Appliance e PDW &#40;sistema di piattaforma Analitica&#41;](pdw-and-appliance-fabric-physical-components.md)|  
|Avviare Gestione configurazione SQL Server PDW|[Avviare Gestione configurazione &#40;sistema di piattaforma Analitica&#41;](launch-the-configuration-manager.md)|  
|Modificare la password di amministratore di dominio|L'appliance è un privato Windows Active Directory Domain Services usato per autenticare i nodi all'interno dell'appliance.<br /><br />Fornitore IHV configurare l'appliance con una password di amministratore di dominio predefinito. Questa operazione deve essere modificato in una password sicura.<br /><br />Il **Configuration Manager** è l'unica modalità supportata per modificare la password di amministratore di dominio.<br /><br />Per altre informazioni, vedere [reimpostazione delle Password &#40;sistema di piattaforma Analitica&#41;](password-reset.md).|  
|Modificare la password per il **sa** logon|SQL Server PDW è un accesso di amministratore di sistema denominato **sa**. Il **sa** accesso dispone di tutti i privilegi. Non è possibile concedere, negare o revocare qualsiasi autorizzazione. Anche possibile visualizzare tutte le viste di sistema.<br /><br />Per altre informazioni, vedere [reimpostazione delle Password &#40;sistema di piattaforma Analitica&#41;](password-reset.md).|  
|Impostare il fuso orario dispositivo|Impostare l'ora (tempo desiderato di locale o altro) per tutti i nodi di appliance.<br /><br />Per altre informazioni, vedere [configurazione del fuso orario Appliance &#40;sistema di piattaforma Analitica&#41;](appliance-time-zone-configuration.md).|  
|Specificare le impostazioni di rete accessibile pubblicamente per l'appliance di SQL Server PDW|[Configurazione di rete di Appliance &#40;sistema di piattaforma Analitica&#41;](appliance-network-configuration.md)|  
|Importare un certificato di sicurezza per la Console di amministrazione|Un certificato possa fornire connessioni Secure Sockets Layer (SSL) su HTTPS per il [monitorare l'Appliance usando la Console di amministrazione &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-the-admin-console.md). Per impostazione predefinita, il **Console di amministrazione** include un certificato autofirmato che fornisce privacy, ma non l'autenticazione del server. Questo certificato restituisce inoltre un errore in Internet Explorer che indica che: "Si è verificato un problema con il certificato di sicurezza di questo sito Web" quando l'utente si connette. Anche se questa connessione consente di crittografare i dati in transito tra il client e server, la connessione è ancora soggetta a rischi da utenti malintenzionati.<br /><br />Gli amministratori di SQL Server PDW devono acquisire immediatamente un certificato concatenato a un'autorità di certificazione attendibile riconosciuta dal client, allo scopo di avere una connessione sicura e rimuovere l'errore che segnala di Internet Explorer. Questa operazione richiede un nome di dominio completo che esegue il mapping di indirizzi IP virtuali del nodo di controllo (scelta consigliata) o le barre di un nome di certificato che corrisponde al valore che gli utenti digitano nel relativo indirizzo del browser per accedere alla Console di amministrazione.<br /><br />Usare la **Configuration Manager** per aggiungere o rimuovere i certificati attendibili. Direttamente utilizzando lo strumento di configurazione di Microsoft Windows HTTP Services certificato (`winHttpCertCfg.exe`) per gestire i certificati non è supportata.<br /><br />Per altre informazioni, vedere [Provisioning del certificato PDW &#40;sistema di piattaforma Analitica&#41;](pdw-certificate-provisioning.md).|
|Opzione della funzionalità|Visualizza le informazioni sulle opzioni di funzionalità che sono stati introdotti in AU7 sistema di piattaforma Analitica. Utilizzare questa pagina per aggiornare o attivare/disabilitare funzionalità e impostazioni di sistema di piattaforma Analitica. La modifica di valori della funzionalità commutatore richiede un riavvio del servizio.<br /><br />Per altre informazioni, vedere [opzione della funzionalità PDW &#40;sistema di piattaforma Analitica&#41;](appliance-feature-switch.md).|
|Abilitare o disabilitare le regole del Firewall di Windows che consentono o impediscono l'accesso a determinate porte nell'appliance di SQL Server PDW.|Fornitore IHV verrà configurare e abilitare le regole del firewall necessarie per l'appliance per il corretto funzionamento. Nella maggior parte dei casi non si verrà abilitare o disabilitare le regole del firewall.<br /><br />Per altre informazioni, vedere [configurazione del Firewall PDW &#40;sistema di piattaforma Analitica&#41;](pdw-firewall-configuration.md).|  
|Avviare e arrestare l'appliance di SQL Server PDW|Arresta o Avvia l'appliance di SQL Server PDW. Per altre informazioni, vedere [stato dei servizi PDW &#40;sistema di piattaforma Analitica&#41;](pdw-services-status.md).|  
|Verifica l'inizializzazione immediata dei File Opzioni usando la **privilegi** nella finestra di dialogo|Inizializzazione immediata dei File è una funzionalità di SQL Server che consente operazioni di file di dati eseguire più rapidamente. Viene abilitata in SQL Server PDW solo se l'account del servizio di rete è stato concesso il privilegio di diritto SE_MANAGE_VOLUME_NAME. È disattivata per impostazione predefinita.<br /><br />Per altre informazioni, vedere [configurazione dell'inizializzazione immediata dei File &#40;sistema di piattaforma Analitica&#41;](instant-file-initialization-configuration.md).|  
|Ripristinare il database master da un backup|Elimina l'oggetto corrente **master** del database e lo sostituisce con una copia di backup. Per altre informazioni, vedere [ripristinare il Master Database &#40;sistema di piattaforma Analitica&#41;](restore-the-master-database.md).|  
  
## <a name="AddTasks"></a>Eseguire attività di configurazione aggiuntive  
Dopo aver eseguito il **Configuration Manager** attività, eseguire il seguente elenco di attività di configurazione aggiuntive. Alcune di queste attività sono facoltativi.  
  
|Attività di configurazione|Descrizione|  
|----------------------|---------------|  
|Il software antivirus di terze parti può essere installato e configurato nell'appliance di SQL Server PDW per con connessione esterna di nodi.<br /><br />(Facoltativo)|Per altre informazioni, vedere [Software Antivirus &#40;sistema di piattaforma Analitica&#41;](antivirus-software.md).|  
|La password per la modalità ripristino servizi directory può essere modificata.<br /><br />(Facoltativo)|Per altre informazioni, vedere [Password dell'amministratore impostato per l'accesso ai nodi AD in modalità ripristino servizi Directory &#40;modalità ripristino servizi directory&#41; &#40;sistema di piattaforma Analitica&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md).|  
|Configurare l'appliance per ricevere gli aggiornamenti software<br /><br />(Consigliato)|L'appliance deve essere configurato per ricevere gli aggiornamenti per il software sottostante e SQL Server PDW.<br /><br />Per altre informazioni, vedere [configurare Windows Server Update Services &#40;WSUS&#41; &#40;sistema di piattaforma Analitica&#41;](configure-windows-server-update-services-wsus.md). Per informazioni su WSUS, vedere [manutenzione Software &#40;sistema di piattaforma Analitica&#41;](software-servicing.md).|  
|Configurare la connettività a dati esterni, ad esempio Hadoop o Azure nell'archivio blob.<br /><br />(Facoltativo)|Per altre informazioni, vedere [configurare la connettività di PolyBase ai dati esterni &#40;sistema di piattaforma Analitica&#41;](configure-polybase-connectivity-to-external-data.md).|  
|Configurare il Software Antivirus<br /><br />(Facoltativo)|Le soluzioni antivirus di terze parti può essere usato per proteggere i nodi accessibile pubblicamente, ma non è obbligatorio. Seguire le istruzioni in.|  
|Configurare le schede di rete InfiniBand nel Backup e il caricamento dei server<br /><br />(Facoltativo)|Per configurare il Backup e il caricamento di server per connettersi a SQL Server PDW con rete InfiniBand, è necessario configurare le schede di rete per consentire l'appliance DNS per risolvere la connessione di InfiniBand per la rete InfiniBand attualmente attiva.|  
|Configurare per l'invio di dati di telemetria a Microsoft<br /><br />(Facoltativo)|Per configurare il sistema di piattaforma Analitica per inviare i dati di telemetria a Microsoft, è necessario eseguire uno script di PowerShell nel nodo di controllo. Per istruzioni specifiche, vedere [commenti e suggerimenti di dati di telemetria a Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md).|  
  
## <a name="see-also"></a>Vedere anche  
[Il Software antivirus &#40;sistema di piattaforma Analitica&#41;](antivirus-software.md)  
[Configurare le schede di rete InfiniBand &#40;SQL Server PDW&#41;](configure-infiniband-network-adapters.md)  
  
