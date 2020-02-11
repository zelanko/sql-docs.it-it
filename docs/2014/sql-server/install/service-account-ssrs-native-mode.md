---
title: Account del servizio (modalità nativa SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.serviceaccount.F1
ms.assetid: face8120-4d32-4c6c-a1e8-99f27d1ff15d
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: db98f9806f48699af996a33675138150803e8812
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952387"
---
# <a name="service-account-ssrs-native-mode"></a>Account del servizio (modalità nativa SSRS)
  Nella pagina Account servizio è possibile specificare l'account con cui viene eseguito il servizio del server di report. Questo account viene configurato inizialmente durante l'installazione, ma può essere modificato se si desidera utilizzare un account o una password diversa. Il servizio Web ReportServer, Gestione report e l'applicazione di elaborazione in background verranno tutti eseguiti con l'identità del servizio specificata in questa pagina.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità nativa.  
  
 L'account specificato per il servizio del server di report deve disporre dell'autorizzazione necessaria per accedere al Registro di sistema, ai file di programma del server di report e al database del server di report. Tutte le autorizzazioni vengono configurate automaticamente per l'account quando si utilizza Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per impostare l'account. Se si utilizza l'account del servizio per connettersi al database del server di report, la Configuration Manager crea un account di accesso al database per l'account e configura le autorizzazioni per il database assegnando l' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] account a RSExecRole nell'istanza che ospita il database del server di report. Il database del server di report è l'unico archivio dati in cui scrive un server di report. Per l'account del servizio non sono necessarie autorizzazioni per altri archivi dati.  
  
 Per aprire questa pagina, avviare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e selezionare il collegamento nel riquadro di navigazione. Per altre informazioni, vedere [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
> [!IMPORTANT]  
>  Ogni volta che è necessario aggiornare l'account o la password, è consigliabile utilizzare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . L'utilizzo di Gestione configurazione per aggiornare l'account garantisce che vengano aggiornate automaticamente anche le altre impostazioni interne che dipendono dall'identità del servizio.  
  
## <a name="options"></a>Opzioni  
 **Utilizza account predefinito**  
 Selezionare **Servizio di rete**, **Sistema locale**o **Servizio locale** dall'elenco. L'unica opzione consigliata è **Servizio di rete** . È tuttavia possibile configurare l'utilizzo di qualsiasi account disponibile.  
  
 **Utilizza un altro account**  
 Selezionare questa opzione per specificare un account utente di Windows. È possibile immettere un account utente locale di Windows o un account utente di dominio. Specificare un account di dominio nel formato: * \<dominio>\\<utente\>*. Specificare un account utente locale di Windows nel formato seguente: * \<nome computer \\><\>utente*. È possibile solo selezionare un account esistente: in Configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è possibile creare nuovi account.  
  
 Il limite massimo di caratteri per l'account è 20.  
  
 Se la rete utilizza l'autenticazione Kerberos e il server di report viene configurato per l'esecuzione con un account utente di dominio, è necessario registrare il servizio con l'account utente. Per altre informazioni, vedere [Registrare un nome dell'entità servizio &#40;SPN&#41; per un server di report](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md).  
  
 Se si passa a un altro tipo di account, ad esempio sostituendo un account di Windows con un altro o un account predefinito con un account di dominio di Windows, verrà richiesto di creare una copia di backup della chiave di crittografia. La copia di backup verrà ripristinata automaticamente quando si seleziona il nuovo account.  
  
> [!NOTE]  
>  In Gestione configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene richiesto di eseguire il backup e il ripristino della chiave di crittografia ogni volta che si modifica l'account del servizio. Questa procedura è necessaria per garantire che i dati crittografati restino disponibili per il server di report. Per altre informazioni su queste azioni, vedere [chiavi di crittografia &#40;modalità nativa di SSRS&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md).  
  
 Inoltre, se si dispone di un server di report configurato per l'esecuzione in modalità integrata SharePoint e si modifica l'account del servizio mediante Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , è necessario aprire anche Amministrazione centrale SharePoint e utilizzare la pagina [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **di** per applicare nuovamente le impostazioni del server di report e dell'istanza. Tramite l'esecuzione di questo passaggio, al nuovo account del servizio verrà concesso l'accesso ai database di SharePoint necessari per l'integrazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con un prodotto o una tecnologia SharePoint. Per ulteriori informazioni sulla concessione dell'accesso al database in Amministrazione centrale SharePoint, vedere [configurazione e amministrazione di un server di Report &#40;Reporting Services modalità sharepoint&#41;](../../../2014/reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md) e [Reporting Services installazione in modalità sharepoint &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
## <a name="choosing-an-account"></a>Scelta di un account  
 Per ottenere risultati ottimali, specificare un account che dispone delle autorizzazioni necessarie per stabilire connessioni di rete, con accesso ai controller di dominio di rete e ai server o ai gateway SMTP aziendali. Nella tabella seguente vengono forniti un riepilogo degli account e alcuni consigli per utilizzarli.  
  
|Account|Spiegazione|  
|-------------|-----------------|  
|Account utente di dominio|Se si possiede un account utente di dominio di Windows che dispone delle autorizzazioni minime necessarie per operazioni sul server di report, è consigliabile utilizzarlo.<br /><br /> Un account utente di dominio rappresenta la scelta consigliata, in quanto isola il servizio del server di report dalle altre applicazioni. L'esecuzione di più applicazioni tramite un account condiviso, ad esempio Servizio di rete, aumenta il rischio di esporre il server di report al controllo da parte di utenti malintenzionati, in quanto una violazione della sicurezza di una delle applicazioni può facilmente estendersi a tutte le applicazioni eseguite utilizzando lo stesso account.<br /><br /> Un account utente di dominio è necessario se si configura il server di report per la delega vincolata o per la modalità integrata SharePoint con i prodotti SharePoint 2010 che richiedono account utente di dominio piuttosto che account predefiniti del computer.<br /><br /> Si noti che se si utilizza un account utente di dominio, sarà necessario modificare periodicamente la password se l'organizzazione applica criteri di scadenza delle password. Potrebbe inoltre essere necessario registrare il servizio con l'account utente. Per altre informazioni, vedere [Registrare un nome dell'entità servizio &#40;SPN&#41; per un server di report](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md).<br /><br /> Evitare di utilizzare un account utente locale di Windows. Gli account locali non dispongono in genere di autorizzazioni sufficienti per accedere alle risorse in altri computer. Per altre informazioni sulle limitazioni imposte alle funzionalità del server di report quando si utilizza un account locale, vedere [Considerazioni sull'utilizzo di account locali](#localaccounts) in questo argomento.|  
|**Servizio di rete**|Il **servizio di rete** è un account predefinito con privilegi minimi che dispone di autorizzazioni di accesso alla rete. Tale account è consigliato se non si dispone di un account utente di dominio o se si desidera evitare le possibili interruzioni del servizio provocate dall'applicazione di criteri di scadenza delle password.<br /><br /> Se si seleziona **Servizio di rete**, tentare di ridurre al minimo il numero degli altri servizi eseguiti con lo stesso account. Una violazione della sicurezza di una delle applicazioni può pregiudicare la sicurezza di tutte le altre applicazioni eseguite con lo stesso account.|  
|**Servizio locale**|Il **servizio locale** è un account predefinito simile a un account utente locale autenticato di Windows. I servizi eseguiti tramite l'account **Servizio locale** possono accedere alle risorse di rete come sessione Null senza credenziali. Questo account non è adatto per scenari di distribuzione Intranet in cui il server di report deve connettersi a un database del server di report remoto o a un controller di dominio di rete per autenticare un utente prima dell'apertura di un report o dell'elaborazione di una sottoscrizione.|  
|**Sistema locale**|**Sistema locale** è un account con privilegi elevati che non è necessario per l'esecuzione di un server di report. Non utilizzare questo account per le installazioni dei server di report. Scegliere piuttosto un account di dominio o l'account **Servizio di rete** .|  
  
##  <a name="localaccounts"></a>Considerazioni sull'utilizzo di account locali  
 La considerazione principale relativa all'utilizzo di account locali consiste nel determinare se il server di report dovrà accedere a server di database remoti, server della posta e controller di dominio. Se si configura il server di report per l'esecuzione come account utente locale di Windows, Servizio locale o Sistema locale occorrerà tenere conto di alcune considerazioni correlate all'impostazione di altre opzioni di configurazione e alla creazione e al recapito delle sottoscrizioni:  
  
-   Se il servizio viene eseguito utilizzando un account locale e si configura una connessione a un database del server di report remoto, il numero di opzioni disponibili in seguito risulterà limitato. In particolare, se si utilizza un database del server di report remoto, sarà necessario configurare la connessione per l'utilizzo di un account utente di dominio o di un account utente di accesso al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che disponga dell'autorizzazione necessaria per accedere all'istanza remota di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   L'esecuzione del servizio tramite un account locale introduce anche nuovi requisiti relativi alla creazione delle sottoscrizioni. Il server di report archivia le informazioni relative agli utenti che creano le sottoscrizioni. Se un utente crea una sottoscrizione mentre è connesso con un account di dominio, il servizio del server di report tenterà di connettersi a un controller di dominio per autenticare l'utente al momento dell'elaborazione della sottoscrizione. Se il servizio viene eseguito utilizzando un account locale, la richiesta di autenticazione ha esito negativo quando viene inviata a un controller di dominio remoto dal server di report. Per ovviare a questa limitazione è possibile utilizzare un'estensione personalizzata per l'autenticazione basata su form oppure fare in modo che tutti gli utenti si connettano al server di report tramite un account utente locale.  
  
-   L'esecuzione del servizio tramite un account locale introduce anche nuovi requisiti relativi al recapito delle sottoscrizioni. Alcune estensioni di recapito includono informazioni sull'account utente nelle definizioni delle sottoscrizioni. Se si inviano report a indirizzi di posta elettronica basati su account utente di dominio e il servizio del server di report viene eseguito utilizzando un account locale, il servizio non sarà in grado di accedere a un controller di dominio remoto per risolvere l'account di posta elettronica di destinazione.  
  
-   Gli account di servizio Windows predefiniti (Servizio locale o Servizio di rete) non sono supportati come account del servizio del server di report su un computer con funzioni di controller di dominio.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../../../2014/sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)   
 [Reporting Services Configuration Manager argomenti della Guida F1 &#40;modalità nativa di SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)  
  
  
