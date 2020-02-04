---
title: Risolvere i problemi di pubblicazione o visualizzazione di un report in un server di report in modalità nativa | Microsoft Docs
ms.date: 02/28/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: df7720a1-d178-45bb-8d6f-63e208cae7fe
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6e3a96e3eef90778b0e7877b88ba79cb4e0dd43e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65573852"
---
# <a name="troubleshoot-publishing-or-viewing-a-report-on-a-native-mode-report-server"></a>Risolvere i problemi di pubblicazione o visualizzazione di un report in un server di report in modalità nativa
  
  
  
Quando si pubblica o si carica un report in un server di report configurato in modalità nativa, è possibile che si verifichino problemi specifici alla visualizzazione dei report nel server di report. Utilizzare le informazioni presenti in questo argomento per risolvere questi problemi.   
  
## <a name="why-am-i-being-prompted-for-credentials-when-i-publish-a-report"></a>Vengono richieste le credenziali quando si pubblica un report  
Per distribuire un report in un server di report, è necessario specificare l'indirizzo del server. È possibile che venga visualizzata la finestra di dialogo di accesso di Reporting Services con la richiesta delle credenziali.   
  
Il nome del server di report non è specificato correttamente  
  
  
Quando si distribuisce il report in un server di report in modalità nativa, un errore comune è quello di specificare il nome della cartella dei report anziché il nome del server di report.   
  
Verificare che l'URL del server di report sia l'indirizzo del server di report, ad esempio `https://localhost/reportserver`, e non l'indirizzo della directory virtuale di Gestione report, ad esempio, `https://localhost/reports`. Se per il server di report è stato specificato un numero di porta diverso da quello predefinito, ovvero 80, è necessario specificarlo nell'indirizzo del server di report, ad esempio `https://localhost:81/reportserver`.   
  
 ## <a name="nothing-happens-when-i-toggle-items-in-my-published-report"></a>Non si verifica nulla quando si attivano o disattivano gli elementi nel report pubblicato.  
  Quando si visualizza un report nell'anteprima locale, è possibile attivare o disattivare e mostrare o nascondere gli elementi nel report. Quando si visualizza lo stesso report dopo averlo pubblicato nel server di report, gli elementi Toggle non funzionano più.   
  
\<nome server di report> include un carattere di sottolineatura (_)  
  
Se un report viene eseguito senza errori, ma gli elementi Toggle non funzionano, ad esempio si fa clic sull'icona di espansione (+) e non accade nulla, controllare il nome del computer che ospita il server di report. Se il nome del computer include un carattere di sottolineatura, gli elementi Toggle non funzionano. Questo è un problema noto Non esistono soluzioni alternative.   
  
Per eseguire i report con gli elementi Toggle, è necessario utilizzare un computer che non includa caratteri di sottolineatura nel proprio nome.  
  
## <a name="images-and-charts-do-not-load-when-i-use-run-as-and-a-browser-to-run-my-report"></a>Le immagini e i grafici non vengono caricati quando si utilizza Esegui come e un browser per eseguire il report.  
Quando si esegue Gestione report in un contesto di sicurezza diverso, gli elementi potrebbero non essere tutti visualizzati in un report.   
  
### <a name="insufficient-permissions-on-internet-temporary-file-folders"></a>Autorizzazioni insufficienti per le cartelle dei file temporanei di Internet  
  
In alcuni casi, quando si utilizza Gestione report per visualizzare i report pubblicati contenenti grafici o immagini, è possibile che non vengano visualizzati. Ad esempio, quando si usa il comando **Esegui come** di Microsoft Windows per visualizzare un report con un contesto di sicurezza diverso, potrebbero non essere disponibili le autorizzazioni per la cartella in cui il server di report memorizza nella cache grafici e immagini come file di Internet temporanei.   
  
Verificare di disporre dell'autorizzazione per accedere alle cartelle contenenti i file memorizzati nella cache.   
    
## <a name="see-also"></a>Vedere anche  
[Supporto browser per Reporting Services e Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[Errori ed eventi (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[Risolvere i problemi di recupero dei dati con i report di Reporting Services](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Risolvere i problemi di sottoscrizioni e recapito di Reporting Services](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

