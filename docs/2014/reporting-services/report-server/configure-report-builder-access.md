---
title: Configurare l'accesso a Generatore report | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, Report Builder
- Report Builder 1.0, configuring access
- configuring servers [Reporting Services]
ms.assetid: a79003d0-c905-4d4c-9560-93a7cc1e1dd4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: be19f42fa5e8a154d8f29e359b6a52395c6504d8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66104032"
---
# <a name="configure-report-builder-access"></a>Configurare l'accesso a Generatore report
  Generatore report è uno strumento per il reporting ad hoc installato con un server di report di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configurato per la modalità nativa o la modalità integrata SharePoint.  
  
 L'accesso a Generatore report dipende dai fattori seguenti:  
  
-   Proprietà del server che determinano se Generatore report è disponibile nel server di report.  
  
-   Assegnazioni di ruolo o autorizzazioni tramite le quali Generatore report viene reso disponibile a singoli utenti o gruppi.  
  
-   Impostazioni di autenticazione che determinano se le credenziali utente possono essere passate al server di report o se l'accesso anonimo è configurato sui file dell'applicazione.  
  
 Per utilizzare Generatore report, è necessario disporre di un modello di report pubblicato da utilizzare.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Generatore report non è disponibile in tutte le edizioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 Nel computer client deve essere [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] installato 2,0. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] fornisce l'infrastruttura per l'esecuzione di applicazioni [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] .  
  
 È necessario utilizzare [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 6.0 o versioni successive.  
  
 Generatore report viene sempre eseguito con attendibilità totale e non è possibile configurarlo per l'esecuzione con attendibilità parziale. Nelle versioni precedenti è possibile eseguire Generatore report in attendibilità parziale, ma tale opzione non è supportata in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive.  
  
## <a name="enabling-and-disabling-report-builder"></a>Abilitazione e disabilitazione di Generatore report  
 Generatore report è abilitato per impostazione predefinita. Gli amministratori del server di report hanno la possibilità di disabilitare la funzionalità Generatore report impostando la proprietà di sistema del server di report `EnableReportDesignClientDownload` su `false`. Impostando questa proprietà, vengono disabilitati i download di Generatore report per il server di report.  
  
 Per impostare le proprietà di sistema del server di report, è possibile utilizzare Management Studio o uno script:  
  
-   Per utilizzare Management Studio, connettersi al server di report e utilizzare la pagina relativa alle proprietà avanzate del server per impostare `EnableReportDesignClientDownload` su `false`. Per altre informazioni su come aprire questa pagina, vedere [Impostare le proprietà di un server di report &#40;Management Studio&#41;](../tools/set-report-server-properties-management-studio.md).  
  
-   Per visualizzare uno script di esempio che consente di impostare una proprietà del server di report, vedere [Creare script per le attività di distribuzione e di amministrazione](../tools/script-deployment-and-administrative-tasks.md).  
  
## <a name="role-assignments-granting-report-builder-access-on-a-native-mode-report-server"></a>Assegnazioni di ruolo che concedono l'accesso a Generatore report in un server di report in modalità nativa  
 In un server di report in modalità nativa creare assegnazioni di ruoli utente che includano attività per l'utilizzo di Generatore report. Per creare o modificare definizioni di ruolo e assegnazioni di ruolo sugli elementi e a livello del sito, è necessario essere assegnati ai ruoli Amministratore sistema e Gestione contenuto.  
  
 Nelle istruzioni seguenti si presuppone che vengano utilizzati ruoli predefiniti. Se le definizioni di ruolo sono state modificate o se è stato eseguito l'aggiornamento da SQL Server 2000, controllare i ruoli per verificare che contengano le attività necessarie. Per altre informazioni sulla creazione delle assegnazioni di ruolo, vedere [Concedere l'accesso utente a un server di report &#40;Gestione report&#41;](../security/grant-user-access-to-a-report-server.md).  
  
 Dopo avere creato le assegnazioni di ruolo, gli utenti disporranno dell'autorizzazione per effettuare le operazioni seguenti:  
  
-   Gli utenti assegnati ai ruoli Utente sistema e Visualizzazione possono visualizzare report di Generatore report pubblicati in un server di report, senza la necessità di avviare Generatore report.  
  
-   Gli utenti assegnati ai ruoli Utente sistema e Generatore report possono generare modelli, avviare Generatore report per creare report e salvare report nel server di report.  
  
-   Gli utenti assegnati ai ruoli Utente sistema e Pubblicazione possono pubblicare modelli da Progettazione modelli nel server di report. I modelli vengono utilizzati come origini dati in Generatore report.  
  
-   Gli utenti assegnati ai ruoli Amministratore sistema e Gestione contenuto dispongono delle autorizzazioni complete per creare, visualizzare e gestire report di Generatore report.  
  
#### <a name="to-verify-required-tasks-are-in-the-role-definitions"></a>Per verificare la presenza delle attività necessarie nelle definizioni di ruolo  
  
1.  Avviare Management Studio e connettersi al server di report.  
  
2.  Aprire la cartella **Sicurezza** .  
  
3.  Aprire la cartella **Ruoli a livello di sistema** .  
  
4.  Fare clic con il pulsante destro del mouse su **Amministratore sistema**e scegliere **Proprietà**.  
  
5.  Selezionare **Esecuzione delle definizioni dei report** e clic su **OK**.  
  
6.  Fare clic con il pulsante destro del mouse su **Utente sistema**e scegliere **Proprietà**.  
  
7.  Selezionare **Esecuzione delle definizioni dei report** e clic su **OK**.  
  
8.  Aprire la cartella **Ruoli** .  
  
9. Fare clic con il pulsante destro del mouse su **Visualizzazione**e scegliere **Proprietà**.  
  
10. Selezionare **Visualizzazione di modelli** e quindi fare clic cu **OK**.  
  
11. Fare clic con il pulsante destro del mouse su **Gestione contenuto**e scegliere **Proprietà**.  
  
12. Selezionare **Visualizzazione di modelli**, **Gestione di modelli**e **Utilizzo di report**, quindi fare clic su **OK**.  
  
13. Fare clic con il pulsante destro del mouse su **Pubblicazione**e scegliere **Proprietà**.  
  
14. Selezionare **Gestione di modelli** e quindi fare clic su **OK**.  
  
15. Creare il ruolo Generatore report se non esiste:  
  
    1.  Aprire la cartella **Sicurezza** .  
  
    2.  Fare clic con il pulsante destro del mouse su **Ruoli**e scegliere **Nuovo ruolo**.  
  
    3.  In Nome digitare **Generatore report**.  
  
    4.  In Descrizione immettere una descrizione per il ruolo in modo da indicare lo scopo del ruolo agli utenti di Gestione report.  
  
    5.  Aggiungere le attività seguenti: **Utilizzo di report**, **Visualizzazione di report**, **Visualizzazione di modelli**, **Visualizzazione di risorse**, **Visualizzazione di cartelle**e **Gestione di sottoscrizioni individuali**.  
  
    6.  Fare clic su **OK** per salvare il ruolo.  
  
#### <a name="to-create-role-assignments-that-grant-access-to-report-builder"></a>Per creare assegnazioni di ruolo che concedono l'accesso a Generatore report  
  
1.  Avviare Gestione report.  
  
2.  Fare clic su **Impostazioni sito**.  
  
3.  Fare clic su **Security**.  
  
4.  Se esiste già un'assegnazione di ruolo per l'utente o il gruppo per cui si vuole configurare l'accesso a Generatore report, fare clic su **Modifica**.  
  
     In caso contrario, fare clic su **Nuova assegnazione ruolo**. In Gruppo o utente immettere un account utente o di gruppo di dominio Windows nel formato \<dominio>\\<account\>. Se si utilizza l'autenticazione basata su form o la sicurezza personalizzata, specificare l'account utente o di gruppo nel formato corretto per la propria distribuzione.  
  
5.  Selezionare **Utente sistema**e quindi fare clic su **OK**.  
  
6.  Fare clic su **Home**.  
  
7.  Fare clic sulla scheda **Impostazioni cartella** .  
  
8.  Fare clic sulla scheda **Security** (Sicurezza).  
  
9. Se esiste già un'assegnazione di ruolo per l'utente o il gruppo per cui si vuole configurare l'accesso a Generatore report, fare clic su **Modifica**.  
  
     In caso contrario, fare clic su **Nuova assegnazione ruolo**. In Gruppo o utente immettere un account utente o di gruppo di dominio Windows nel formato \<dominio>\\<account\>. Se si utilizza l'autenticazione basata su form o la sicurezza personalizzata, specificare l'account utente o di gruppo nel formato corretto per la propria distribuzione.  
  
10. Selezionare **Generatore report**e quindi fare clic su **Applica**.  
  
11. Ripetere le operazioni per creare o modificare le assegnazioni di ruolo per utenti o gruppi aggiuntivi.  
  
## <a name="permissions-granting-report-builder-access-on-a-sharepoint-integrated-mode-report-server"></a>Autorizzazioni che concedono l'accesso a Generatore report in un server di report in modalità integrata SharePoint  
 In un server di report in modalità integrata SharePoint l'accesso a Generatore report viene concesso agli utenti di SharePoint che dispongono dei livelli di autorizzazione Collaborazione o Controllo completo.  
  
 Se si utilizzano livelli di autorizzazione personalizzati, è necessario includere Aggiunta elementi e Modifica elementi al livello di autorizzazione. Per altre informazioni sull'accesso a Generatore report tramite i livelli di autorizzazione predefiniti, vedere [Usare la sicurezza predefinita di Windows SharePoint Services per gli elementi del server di report](../security/use-built-in-security-in-windows-sharepoint-services-for-report-server-items.md). Per altre informazioni sui requisiti di autorizzazione per i livelli di autorizzazione personalizzati, vedere [Impostare le autorizzazioni per le operazioni del server di report in un'applicazione Web di SharePoint](../security/set-permissions-for-report-server-operations-in-a-sharepoint-web-application.md).  
  
## <a name="authentication-considerations-and-credential-reuse"></a>Considerazioni sull'autenticazione e riutilizzo delle credenziali  
 Per scaricare e installare i file dell'applicazione in un computer client, in Generatore report viene utilizzata la tecnologia ClickOnce. Tale tecnologia è stata progettata per la distribuzione unidirezionale di applicazioni mediante la quale i file di programma vengono inseriti in un computer client e l'applicazione viene eseguita come processo separato con l'identità dell'utente predefinito. Poiché Generatore report deve connettersi nuovamente al server di report per ottenere i file dell'applicazione e i dati del server di report, è importante comprendere il modo in cui ClickOnce imposta il contesto di sicurezza e invia le richieste ai computer remoti in scenari diversi:  
  
-   ClickOnce viene sempre eseguita come un processo separato nel computer client. L'identità del processo è rappresentata dalle credenziali utente di Windows predefinite. ClickOnce non condivide dati della sessione con Internet Explorer né ottiene il contesto di sicurezza dell'utente corrente da Internet Explorer.  
  
-   ClickOnce invia richieste che specificano la sicurezza integrata di Windows nell'intestazione di autenticazione. Se un server è configurato per un tipo di autenticazione diverso, bloccherà le richieste inviate da ClickOnce restituendo un errore di autenticazione. Per risolvere questo problema, è necessario configurare un server per la sicurezza integrata di Windows oppure consentire l'accesso anonimo per eliminare il controllo di autenticazione.  
  
-   Generatore report apre una connessione a un server di report. Se non si utilizza la sicurezza integrata di Windows con Single Sign-On, gli utenti devono specificare nuovamente le proprie credenziali per consentire a Generatore report di stabilire la connessione al server di report.  
  
 Nella tabella seguente vengono descritti i tipi di autenticazione supportati dal server di report e viene indicato se è necessario utilizzare una configurazione aggiuntiva per accedere a Generatore report.  
  
|Tipo di autenticazione del server di report|Modalità di risposta di Generatore report e dell'utilità di avvio delle applicazioni ClickOnce|  
|---------------------------------------|--------------------------------------------------------------------|  
|Con negoziazione (impostazione predefinita)<br /><br /> NTLM (impostazione predefinita)|Se si utilizza la sicurezza integrata di Windows, le richieste autenticate provenienti da ClickOnce e Generatore report vengono in genere soddisfatte se il client e il server sono distribuiti nello stesso dominio, se l'utente ha eseguito l'accesso al computer client utilizzando un account di dominio con l'autorizzazione per accedere a Generatore report e se il server di report è configurato per l'autenticazione di Windows.<br /><br /> Le richieste vengono soddisfatte perché l'identità utente di ClickOnce e della connessione tramite browser al server di report è la stessa.<br /><br /> Le richieste non verranno soddisfatte se l'utente ha aperto Internet Explorer con Esegui come e ha specificato credenziali non predefinite. Se la sessione utente nel server di report è stata stabilita con un account specifico e ClickOnce viene eseguita con un account diverso, il server di report negherà l'accesso ai file.|  
|Kerberos|Internet Explorer, necessario per utilizzare Generatore report, non supporta direttamente l'autenticazione Kerberos.|  
|Autenticazione di base|In ClickOnce l'autenticazione di base non è supportata e non verranno pertanto formulate richieste che specificano questo tipo di autenticazione nell'intestazione di autenticazione. Non verranno passate credenziali né verrà richiesto all'utente di specificarle. Per risolvere questi problemi, abilitare l'accesso anonimo ai file dell'applicazione di Generatore report.<br /><br /> Se si abilita l'accesso anonimo ai file dell'applicazione di Generatore report, le richieste verranno soddisfatte perché il server di report ignora l'intestazione di autenticazione. Per altre informazioni su come abilitare l'accesso anonimo a Generatore report, vedere [Configurare l'autenticazione di base nel server di report](../security/configure-basic-authentication-on-the-report-server.md).<br /><br /> Dopo che i file dell'applicazione sono stati recuperati da ClickOnce, Generatore report apre una connessione separata a un server di report. Affinché la connessione venga stabilita, gli utenti devono specificare nuovamente le proprie credenziali poiché Generatore report non raccoglie credenziali da Internet Explorer o ClickOnce.<br /><br /> Se il server di report è configurato per l'autenticazione di base e se per i file di programma di Generatore report non è stato abilitato l'accesso anonimo, le richieste non verranno soddisfatte poiché ClickOnce specifica la sicurezza integrata di Windows nelle proprie richieste. Se si configura il server di report per l'autenticazione di base, il server rifiuterà la richiesta poiché in quest'ultima viene specificato un pacchetto di sicurezza non valido e non sono contenute le credenziali previste per il server di report.<br /><br /> Se inoltre il server di report viene configurato per l'utilizzo della modalità integrata SharePoint e il sito di SharePoint utilizza l'autenticazione di base, verrà generato l'errore 401 quando gli utenti tenteranno di utilizzare ClickOnce per installare Generatore report nei computer client. Questo problema si verifica perché SharePoint utilizza un cookie per rendere valida l'autenticazione di un utente per tutta la durata della sessione, ma tale cookie non è supportato da ClickOnce. Quando un utente avvia un'applicazione ClickOnce, ad esempio Generatore report, l'applicazione non passa il cookie a SharePoint e, pertanto, SharePoint nega l'accesso e restituisce l'errore 401.<br /><br /> È possibile risolvere questo problema provando a eseguire una delle operazioni seguenti:<br /><br /> Selezionare l'opzione **memorizza password** quando si forniscono le credenziali utente.<br /><br /> Abilitare l'accesso anonimo alla raccolta siti di SharePoint.<br /><br /> Configurare l'ambiente in modo che l'utente non debba fornire credenziali. In un ambiente Intranet, ad esempio, è possibile configurare il server SharePoint in modo che appartenga a un gruppo di lavoro e quindi creare gli account utente nel computer locale.|  
|Personalizzato|Quando si configura un server di report per utilizzare l'autenticazione personalizzata, su tale server è abilitato l'accesso anonimo e le richieste vengono accettate senza alcun controllo di autenticazione.<br /><br /> Dopo che i file dell'applicazione sono stati recuperati da ClickOnce, Generatore report apre una connessione separata a un server di report. Affinché la connessione venga stabilita, gli utenti devono specificare nuovamente le proprie credenziali poiché Generatore report non raccoglie credenziali da Internet Explorer o ClickOnce.|  
  
## <a name="see-also"></a>Vedi anche  
 [Autenticazione con il server di report](../security/authentication-with-the-report-server.md)   
 [Pianificazione del supporto per Reporting Services e Power View browser &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md)   
 [Avvia Generatore report &#40;Generatore report&#41;](../report-builder/start-report-builder.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Connettersi a un server di report in Management Studio](../tools/connect-to-a-report-server-in-management-studio.md)   
 [Proprietà di sistema del server di report](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)  
  
  
