---
title: Configurare Reporting Services per usare un nome alternativo del soggetto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ce458f9f-4b4f-4a58-aa75-9a90dda1e622
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2c0d16d95709746d32323ab7a4e17c0b4405ba12
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63266048"
---
# <a name="configure-reporting-services-to-use-a-subject-alternative-name"></a>Configurare Reporting Services per usare un nome alternativo del soggetto
  Questo argomento descrive come configurare [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS) in modo da usare un nome alternativo del soggetto (SAN) modificando il file rsreportserver.config e usando lo strumento Netsh.exe.  
  
||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] |  
  
 Le istruzioni si applicano all'URL Reporting Service nonché all'URL servizio Web.  
  
 Per usare un nome alternativo del soggetto, è necessario che il certificato SSL sia registrato nel server, firmato e che contenga la chiave privata. Non è possibile usare un certificato autofirmato.  
  
 Gli URL in [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] possono essere configurati per l'uso di un certificato SSL. In genere, un certificato contiene solo un nome del soggetto che consente un solo URL per una sessione SSL (Secure Sockets Layer). Il nome alternativo del soggetto è un campo aggiuntivo nel certificato che consente a un servizio SSL di essere in ascolto e valido per molti URL nonché di condividere la porta SSL con altre applicazioni. Il nome alternativo del soggetto è simile al seguente: www.s2.com.  
  
 Per altre informazioni sulle impostazioni di SSL per [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], vedere [Configurare connessioni SSL in un server di report in modalità nativa](security/configure-ssl-connections-on-a-native-mode-report-server.md).  
  
### <a name="configure-ssrs-to-use-a-subject-alternative-name-for-web-service-url"></a>Configurare SSRS per usare un nome alternativo del soggetto per l'URL servizio Web  
  
1.  Avviare Gestione configurazione Reporting Services.  
  
     Per altre informazioni, vedere [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
2.  Nella pagina **URL servizio Web** selezionare una porta SSL e un certificato SSL.  
  
     ![Gestione configurazione Reporting Services](media/reportingservices-configurationmanager.png "Gestione configurazione Reporting Services")  
  
     Gestione configurazione registra il certificato SSL per la porta.  
  
3.  Aprire il file rsreportserver.config.  
  
     Per impostazione predefinita, nella modalità nativa di SSRS il file si trova nella cartella seguente.  
  
    ```  
    \Program Files\Microsoft SQL Server\MSRS11.MSSQLSERVER\Reporting Services\ReportServer  
    ```  
  
4.  Copiare la sezione URL del servizio Web ReportServer.  
  
     Di seguito, ad esempio, è riportata la sezione URL originale.  
  
    ```  
        <URL>  
         <UrlString>https://localhost:443</UrlString>  
         <AccountSid>S-1-5-20</AccountSid>  
         <AccountName>NT Authority\NetworkService</AccountName>  
        </URL>  
  
    ```  
  
     Di seguito è riportata la sezione URL modificata.  
  
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
  
8.  Mostrare gli urlacl esistenti digitando il testo seguente.  
  
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
 [File di configurazione RSReportServer](report-server/rsreportserver-config-configuration-file.md)   
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Modificare un file di configurazione di Reporting Services &#40;RSreportserver.config&#41;](report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
