---
title: Risolvere i problemi di sottoscrizioni e recapito di Reporting Services | Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: ae1775f7-9919-48ca-8bd7-cc16df274e2c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 84ca5db4b8979b1b49ffc25b809638defc40fe1e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "65572120"
---
# <a name="troubleshoot-reporting-services-subscriptions-and-delivery"></a>Risolvere i problemi di sottoscrizioni e recapito di Reporting Services
  
    
Questo argomento spiega come risolvere i problemi che si verificano quando si usano le funzionalità di sottoscrizione, pianificazione e recapito di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] .  
## <a name="log-information"></a>Informazioni sui log
 
La pagina Sottoscrizione di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] include lo stato di una sottoscrizione. Se però sono presenti problemi relativi a tale sottoscrizione, le informazioni dettagliate pertinenti sono riportate nei log di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] . 
![ssrs_tutorial_datadriven_subscription_status_ReportManager](../../reporting-services/media/ssrs-tutorial-datadriven-subscription-status-reportmanager.png)

**Log di traccia:** i log di traccia sono file di testo scritti a: `\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles`

Di seguito è riportato un esempio di voce log:

```
   subscription WindowsService_10   4c7c    05/24/2016-01:05:06  e ERROR     Failure writing file \\ServerName\SalesReports\so71949.xls : Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareProvider+NetworkErrorException: An impersonation error occurred using the security context of the current user. ---> System.ArgumentException: Value does not fall within the expected range.  05/24/2016
```
Per altre informazioni sui log di traccia di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , vedere: 
+ [Report Server Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)(Log di traccia del server di report).
+ [File di log di Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).

**Visualizzazioni di log di esecuzione:**

I log di esecuzione sono visualizzazioni presenti nel database del server di report SQL. Per altre informazioni su [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , vedere [Vista ExecutionLog ed ExecutionLog3 del server di report](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  

----------
## <a name="unable-to-send-reports-using-e-mail-with-windows-server-2003-and-pop3"></a>Impossibile inviare report tramite posta elettronica con Windows Server 2003 e POP3  
Se si esegue un'applicazione di posta elettronica mediante il protocollo POP3 in Microsoft Windows Server 2003, potrebbe risultare impossibile inviare i report con il server POP3 locale. Se si configura il server di report per inviare messaggi di posta elettronica con il server POP3 locale e si crea una sottoscrizione per l'invio di un report, potrebbe essere visualizzato il messaggio di errore seguente:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Failure sending mail: <error message>`  
  
dove \<error message> viene sostituito da altre informazioni sul messaggio di errore restituite da Collaboration Data Objects (CDO).  
  
### <a name="to-resolve-this-problem"></a>Per risolvere questo problema:  
* Impostare su 1 il valore dell'elemento `SendUsing` nel file **Rsreportserver.config** .  
* Cancellare il valore della proprietà `SMTPServer` in modo che sia vuota. Sarà inoltre necessario specificare un valore per la proprietà `SMTPServerPickupDirectory` .   
  
Per altre informazioni sull'uso di un servizio SMTP locale per il recapito di report tramite posta elettronica, vedere Configurare un server di report per il recapito tramite posta elettronica.  
  
## <a name="failure-sending-mail-the-server-rejected-the-sender-address-the-server-response-was-454-573-client-does-not-have-permission-to-submit-mail-to-this-server"></a>Errore durante l'invio della posta: Indirizzo del mittente respinto dal server. Risposta del server: 454 5.7.3 Il client non dispone delle autorizzazioni necessarie per inviare posta a questo server  
Questo errore si verifica quando le impostazioni dei criteri di sicurezza sul server SMTP consentono ai soli utenti autenticati di inviare posta per il successivo recapito. Se il server SMTP non accetta l'invio di messaggi di posta elettronica da parte di utenti anonimi, rivolgersi all'amministratore di sistema per ricevere informazioni su come ottenere l'autorizzazione all'utilizzo del server.  
> Questo errore può verificarsi anche quando si specifica il nome di un server di Exchange come SMTPServer. Per utilizzare un server di Exchange per il recapito tramite posta elettronica, è necessario specificare il nome del gateway SMTP configurato per il server di Exchange. Richiedere il nome all'amministratore di Exchange.  
  
## <a name="subscriptions-are-not-processing"></a>Le sottoscrizioni non vengono elaborate  
Le sottoscrizioni possono non venire eseguite nei casi seguenti:   
* La pianificazione utilizzata per generare il report è scaduta. Per le sottoscrizioni che generano un aggiornamento dello snapshot del report, la pianificazione utilizzata per l'aggiornamento potrebbe essere scaduta.  
  
* Il server di report, SQL Server Agent o il server di posta elettronica non è in esecuzione.  
* Il report non può essere recapitato, ad esempio perché è troppo grande. Per determinare se il mancato recapito dipende dalle dimensioni del report, salvare il report in un file e quindi inviarlo tramite posta elettronica. Assicurarsi di scegliere lo stesso formato di rendering specificato nella sottoscrizione. Se viene visualizzato un errore di recapito, utilizzare l'estensione per il recapito alla condivisione file anziché Messaggio di posta elettronica da Server report.  
* Il computer utilizzato per il recapito tramite condivisione file non è in funzione o la condivisione file è configurata per l'accesso in sola lettura.  
* L'estensione per il recapito specificata nella sottoscrizione è stata disinstallata o disabilitata.  
* Le impostazioni delle credenziali sono state modificate, passando da valori archiviati a valori integrati o su richiesta.  
* Il nome del parametro o il tipo di dati è stato modificato nella definizione del report e il report è stato ripubblicato. Se in una sottoscrizione è incluso un parametro non più valido, la sottoscrizione diventerà inattiva.  
  
Per altre informazioni, vedere Wiki di TechNet [Troubleshoot issues and errors with Reporting Services](https://social.technet.microsoft.com/wiki/contents/articles/1633.ssrs-troubleshoot-issues-and-errors-with-reporting-services.aspx)(Risoluzione di problemi ed errori di Reporting Services).  
  
  
    
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

