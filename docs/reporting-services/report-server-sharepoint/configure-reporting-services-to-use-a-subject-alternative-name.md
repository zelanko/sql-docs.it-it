---
title: Configurare Reporting Services per usare un nome alternativo del soggetto | Microsoft Docs
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 493abba0e4396b6f12670dd3214d19e4767c4d0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580014"
---
# <a name="configure-reporting-services-to-use-a-subject-alternative-name"></a>Configurare Reporting Services per usare un nome alternativo del soggetto

Questo argomento descrive come configurare Reporting Services (SSRS) in modo da usare un nome alternativo del soggetto (SAN) modificando il file rsreportserver.config e usando lo strumento Netsh.exe.

Le istruzioni si applicano all'URL Reporting Service nonché all'URL servizio Web.

Per usare un nome alternativo del soggetto, è necessario che il certificato SSL sia registrato nel server, firmato e che contenga la chiave privata. Non è possibile usare un certificato autofirmato.  
  
 Gli URL in Reporting Services possono essere configurati per l'uso di un certificato SSL. In genere, un certificato contiene solo un nome del soggetto che consente un solo URL per una sessione SSL (Secure Sockets Layer). Il nome alternativo del soggetto è un campo aggiuntivo nel certificato che consente a un servizio SSL di essere in ascolto per molti URL nonché di condividere la porta SSL con altre applicazioni. Il nome alternativo del soggetto è simile a `www.s2.com`.  
  
 Per altre informazioni sulle impostazioni di SSL per Reporting Services, vedere [Configurare connessioni SSL in un server di report in modalità nativa](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md).  
  
## <a name="configure-ssrs-to-use-a-subject-alternative-name-for-web-service-url"></a>Configurare SSRS per usare un nome alternativo del soggetto per l'URL servizio Web
  
1.  Avviare Gestione configurazione Reporting Services.  
  
     Per altre informazioni, vedere [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2.  Nella pagina **URL servizio Web** selezionare una porta SSL e un certificato SSL.  
  
     ![Gestione configurazione Reporting Services](../../reporting-services/report-server-sharepoint/media/reportingservices-configurationmanager.png "Gestione configurazione Reporting Services")  
  
     Gestione configurazione registra il certificato SSL per la porta.  
  
3.  Aprire il file rsreportserver.config.  
  
     Per impostazione predefinita, nella modalità nativa di SSRS il file si trova nella cartella seguente:  
  
    ```  
    \Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
4.  Copiare la sezione URL del servizio Web ReportServer.  
  
     Ad esempio, la sezione URL originale è:  
  
    ```  
        <URL>  
         <UrlString>https://localhost:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
     La sezione URL modificata è:
  
    ```  
    <URL>  
         <UrlString>https://www.s1.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
        <URL>  
         <UrlString>https://www.s2.com:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
5.  Salvare il file rsreportserver.config.  
  
6.  Avviare un prompt dei comandi come amministratore ed eseguire lo strumento Netsh.exe.  
  
    ```  
    C:\windows\system32\netsh  
    ```  
  
7.  Passare al contesto http digitando il testo seguente.  
  
    ```  
    Netsh>http  
    ```  
  
8.  Mostrare gli urlacl esistenti digitando il testo seguente:
  
    ```  
    Netsh http>show urlacl  
    ```  
  
     Verrà visualizzata una voce simile alla seguente.  
  
    ```  
    Reserved URL            : https:// www.s1.com:443/ReportServer/  
        User: NT SERVICE\ReportServer  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;S-1-5-80-1234567890-123456789-123456789-123456789-1234567890)  
    ```  
  
     Un urlacl è un elenco di controllo di accesso discrezionale (DACL, Discretionary Access Control List) per un URL riservato.  
  
9. Creare una nuova voce per il nome alternativo del soggetto con lo stesso utente e SDDL della voce esistente digitando il testo seguente.  
  
    ```  
    netsh http>add urlacl  url=https://www.s2.com:443/ReportServer    
    user="NT Service\ReportServer" sddl=D:(A;;GX;;;S-1-5-80-1234567980-12346579-123456789-123456789-1234567890)  
  
    ```  
  
10. Nella pagina **Stato server di report** di Gestione configurazione Reporting Services fare clic su **Arresta** e quindi su **Avvia** per riavviare il server di report.  
  
## <a name="see-also"></a>Vedere anche

 [File di configurazione RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Gestione configurazione Reporting Services](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Modificare un file di configurazione di Reporting Services](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Configurare gli URL del server di report](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
