---
title: Configurare l'autenticazione di base nel server di report | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, configuration
- Basic authentication
ms.assetid: 8faf2938-b71b-4e61-a172-46da2209ff55
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 32b46265b5da376bc974b55c48bf54bad88917d8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102168"
---
# <a name="configure-basic-authentication-on-the-report-server"></a>configurazione dell'autenticazione di base nel server di report
  Per impostazione predefinita, tramite Reporting Services vengono accettate richieste che consentono di specificare l'autenticazione con negoziazione e NTLM. Se la distribuzione include applicazioni client o browser che utilizzano l'autenticazione di base, è necessario aggiungere questo tipo di autenticazione all'elenco di tipi supportati. Inoltre, se si desidera utilizzare Generatore report, è necessario abilitare l'accesso anonimo ai relativi file.  
  
 Per configurare l'autenticazione di base nel server di report, modificare gli elementi e i valori XML nel file RSReportServer.config. È possibile copiare e incollare gli esempi disponibili in questo argomento per sostituire i valori predefiniti.  
  
 Prima di abilitare l'autenticazione di base, verificare che l'infrastruttura di sicurezza la supporti. Con l'autenticazione di base, il servizio Web ReportServer passa le credenziali all'autorità di sicurezza locale. Se nelle credenziali è specificato un account utente locale, l'utente viene autenticato dall'autorità di sicurezza locale nel computer del server di report e ottiene un token di sicurezza valido per le risorse locali. Le credenziali per gli account utente di dominio vengono inoltrate e autenticate da un controller di dominio. Il ticket risultante è valido per le risorse di rete.  
  
 La crittografia del canale, ad esempio Secure Sockets Layer (SSL), è necessaria se si desidera ridurre i rischi associati all'intercettazione delle credenziali durante il transito verso un controller di dominio nella rete. L'autenticazione di base trasmette il nome utente in testo non crittografato e la password con la codifica in base 64. Con l'aggiunta della crittografia del canale, il pacchetto diventa illeggibile. Per altre informazioni, vedere [Configurare connessioni SSL in un server di report in modalità nativa](configure-ssl-connections-on-a-native-mode-report-server.md).  
  
 Dopo aver abilitato l'autenticazione di base, tenere presente che gli utenti non possono selezionare l'opzione **sicurezza integrata di Windows** durante l'impostazione delle proprietà di connessione a un'origine dati esterna che fornisce i dati a un report. Nelle pagine di proprietà dell'origine dati l'opzione verrà visualizzata in grigio.  
  
> [!NOTE]  
>  Le istruzioni seguenti sono relative a un server di report in modalità nativa. Se il server di report è distribuito in modalità integrata SharePoint, è necessario utilizzare le impostazioni di autenticazione predefinite che specificano la sicurezza integrata di Windows. Per supportare server di report in modalità integrata SharePoint, il server di report utilizza caratteristiche interne nell'estensione di autenticazione di Windows predefinita.  
  
### <a name="to-configure-a-report-server-to-use-basic-authentication"></a>Per configurare un server di report per l'utilizzo dell'autenticazione di base  
  
1.  Aprire RSReportServer.config in un editor di testo.  
  
     Il file si trova in * \<unità>:* \Programmi\Microsoft SQL Server\MSRS12. Services\ReportServer. MSSQLSERVER\Reporting  
  
2.  Trovare <`Authentication`>.  
  
3.  Tra le strutture XML seguenti, copiare quella che corrisponde meglio alle proprie esigenze. Nella prima struttura XML sono disponibili segnaposti per la specifica di tutti gli elementi, descritti nella sezione successiva:  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsBasic>  
                       <LogonMethod>3</LogonMethod>  
                       <Realm></Realm>  
                       <DefaultDomain></DefaultDomain>  
                 </RSWindowsBasic>  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
     Se si utilizzano i valori predefiniti, è possibile copiare la struttura di elementi minima:  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsBasic/>  
          </AuthenticationTypes>  
    ```  
  
4.  Incollarlo sulle voci esistenti per <`Authentication`>.  
  
     Se si utilizzano più tipi di autenticazione, aggiungere solo l'elemento `RSWindowsBasic`, ma non eliminare le voci relative a `RSWindowsNegotiate`, `RSWindowsNTLM` o `RSWindowsKerberos`.  
  
     Per supportare il browser Safari, non è possibile configurare il server di report per l'utilizzo di più tipi di autenticazione. È necessario specificare solo `RSWindowsBasic` ed eliminare le altre voci.  
  
     Si noti che non è possibile utilizzare `Custom` con altri tipi di autenticazione.  
  
5.  Sostituire i valori vuoti per `Realm` <> o `DefaultDomain` <> con valori validi per l'ambiente in uso.  
  
6.  Salvare il file.  
  
7.  Se è stata configurata una distribuzione con scalabilità orizzontale, ripetere questi passaggi per gli altri server di report presenti nella distribuzione.  
  
8.  Riavviare il server di report per cancellare qualsiasi sessione attualmente aperta.  
  
## <a name="rswindowsbasic-reference"></a>Riferimento per RSWindowsBasic  
 Quando si configura l'autenticazione di base, è possibile specificare gli elementi seguenti.  
  
|Elemento|Obbligatoria|Valori validi|  
|-------------|--------------|------------------|  
|LogonMethod|Sì<br /><br /> Se non si specifica un valore, verrà utilizzato 3.|
  `2` = accesso alla rete, destinato ai server ad alte prestazioni per l'autenticazione di password in testo normale.<br /><br /> 
  `3` = accesso non crittografato, che mantiene le credenziali di accesso nel pacchetto di autenticazione inviato con ogni richiesta HTTP, consentendo al server di rappresentare l'utente in caso di connessione ad altri server della rete. Valore predefinito.<br /><br /> Nota: i valori 0 (per accesso interattivo) e 1 (per accesso batch) NON sono supportati in [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)].|  
|Realm|Facoltativo|Specifica una partizione delle risorse che include le caratteristiche di autorizzazione e autenticazione utilizzate per controllare l'accesso alle risorse protette nell'organizzazione.|  
|DefaultDomain|Facoltativo|Specifica il dominio utilizzato dal server per autenticare l'utente. Questo valore è facoltativo, ma se non viene specificato il server di report utilizzerà il nome del computer come dominio. Se il computer è un membro di dominio, tale dominio rappresenta il dominio predefinito. Se il server di report è stato installato in un controller di dominio, il dominio utilizzato è quello controllato dal computer.|  
  
## <a name="enabling-anonymous-access-to-report-builder-application-files"></a>Abilitazione dell'accesso anonimo ai file dell'applicazione Generatore report  
 Per scaricare e installare i file dell'applicazione in un computer client, Generatore report utilizza la tecnologia ClickOnce. All'avvio nel computer client, l'utilità di avvio delle applicazioni ClickOnce richiederà file dell'applicazione aggiuntivi nel computer del server di report. Se il server di report è configurato per l'autenticazione di base, il controllo dell'autenticazione tramite l'utilità di avvio non riuscirà, in quanto questo tipo di autenticazione non è supportato.  
  
 Per risolvere questo problema, è possibile configurare l'accesso anonimo ai file di programma di Generatore report. In questo modo, ClickOnce è in grado di ignorare il controllo dell'autenticazione quando recupera i file. Per abilitare l'accesso anonimo, effettuare le operazioni seguenti:  
  
-   Verificare che il server di report sia configurato per l'autenticazione di base.  
  
-   Creare una cartella bin sotto ReportBuilder e copiarvi quattro assembly.  
  
-   Aggiungere l'elemento `IsReportBuilderAnonymousAccessEnabled` a RSReportServer.config e impostarlo su `True`. Dopo aver salvato il file, il server di report crea un nuovo endpoint in Generatore report. Tale endpoint viene utilizzato internamente per accedere ai file del programma e non include un'interfaccia programmatica che è possibile utilizzare nel codice. Grazie a un endpoint distinto, Generatore report può eseguire il proprio dominio applicazione con il limite di processo del servizio del server di report.  
  
-   Se si desidera, è possibile specificare un account con privilegi minimi per elaborare le richieste in un contesto di sicurezza diverso rispetto a quello del server di report. Questo account diventa l'account anonimo per l'accesso ai file di Generatore report in un server di report. L'account imposta l'identità del thread nel processo di lavoro ASP.NET. Le richieste eseguite in tale thread vengono passate al server di report senza controllo di autenticazione. Questo account è equivalente all'account IUSR_\<Machine> in Internet Information Services (IIS), utilizzato per impostare il contesto di sicurezza per i processi di lavoro di ASP.NET quando sono abilitati l'accesso anonimo e la rappresentazione. Per specificare l'account, aggiungerlo in un file Web.config di Generatore report.  
  
 Se si desidera abilitare l'accesso anonimo ai file del programma Generatore report, è necessario che il server di report sia configurato per l'autenticazione di base. Se il server di report non è configurato per l'autenticazione di base e si prova ad abilitare l'accesso anonimo, viene generato un errore.  
  
 Per ulteriori informazioni sui problemi di autenticazione e Generatore report, vedere [Configure Generatore report Access](../report-server/configure-report-builder-access.md).  
  
#### <a name="to-configure-report-builder-access-on-a-report-server-configured-for-basic-authentication"></a>Per configurare l'accesso a Generatore report in un server di report configurato per l'autenticazione di base  
  
1.  Verificare che il server di report sia configurato per l'autenticazione di base controllando le impostazioni di autenticazione nel file RSReportServer.config.  
  
2.  Creare una cartella BIN sotto la cartella ReportBuilder. Per impostazione predefinita, il percorso di questa cartella è \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\ReportBuilder.  
  
3.  Copiare gli assembly seguenti dalla cartella ReportServer\Bin alla cartella ReportBuilder\BIN:  
  
     Microsoft.ReportingServices.Diagnostics.dll  
  
     Microsoft.ReportingServices.Interfaces.dll  
  
     ReportingServicesAppDomainManager.dll  
  
     RSHttpRuntime.dll  
  
4.  Se si desidera, creare un file Web.config per elaborare le richieste di Generatore report con un account anonimo:  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
    <system.web>  
    <authentication mode="Windows" />    
    <identity impersonate="true " userName="username" password="password"/>  
    </system.web>  
    </configuration>  
    ```  
  
     Se si include un file Web.config, la modalità di autenticazione deve essere impostata su `Windows`.  
  
     `Identity impersonate`può essere `True` o `False`.  
  
    -   Impostarla su `False` se non si desidera che ASP.NET legga il token di sicurezza. La richiesta verrà eseguita nel contesto di sicurezza del servizio del server di report.  
  
    -   Impostarla su `True` se si desidera che ASP.NET legga il token di sicurezza dal livello host. Se questa opzione viene impostata su `True`, è necessario specificare anche `userName` e `password` per definire un account anonimo. Le credenziali specificate determineranno il contesto di sicurezza in cui viene generata la richiesta.  
  
5.  Salvare il file Web.config nella cartella ReportBuilder\bin.  
  
6.  Aprire file RSReportServer.config, quindi nella sezione Servizi individuare `IsReportManagerEnabled` e aggiungere di seguito l'impostazione seguente:  
  
    ```  
    <IsReportBuilderAnonymousAccessEnabled>True</IsReportBuilderAnonymousAccessEnabled>  
    ```  
  
7.  Salvare e chiudere il file RSReportServer.config.  
  
8.  Riavviare il server di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Domini applicazione per applicazioni del server di report](../report-server/application-domains-for-report-server-applications.md)   
 [Sicurezza e protezione di Reporting Services](reporting-services-security-and-protection.md)  
  
  
