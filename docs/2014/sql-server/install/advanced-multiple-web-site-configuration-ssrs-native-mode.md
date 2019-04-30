---
title: Configurazione avanzata più siti Web (modalità nativa SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.advancedmultiplewebsiteconfig.F1
ms.assetid: af4ede43-2225-45b5-ae7e-9202411551ba
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d6860e41991d00e6cd0c2869413dca110422c4e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63226016"
---
# <a name="advanced-multiple-web-site-configuration-ssrs-native-mode"></a>Configurazione avanzata più siti Web (modalità nativa SSRS)
  Questa finestra di dialogo consente di creare e gestire gli URL utilizzati per accedere a un server di report o a Gestione report. La finestra di dialogo **Configurazione avanzata più siti Web** viene utilizzata per creare URL aggiuntivi, URL personalizzati che includono un nome di intestazione host o per specificare un indirizzo IP in formato IPv4 o IPv6.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 La creazione di più URL è utile se si desidera configurare modalità di accesso diverse a un server di report. L'accesso al server di report tramite connessioni Intranet ed Extranet, ad esempio, richiede in genere che siano presenti più URL per ogni tipo di connessione.  
  
 Per aprire la finestra di dialogo **Configurazione avanzata più siti Web** fare clic su **Avanzate** nella pagina **URL servizio Web** o **URL Gestione report** di Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Quando la finestra di dialogo **Configurazione avanzata più siti Web** viene visualizzata, è possibile fare clic su **Aggiungi** o **Modifica** per definire nuovi URL o modificare o eliminare URL esistenti.  
  
 Scegliere **OK** per salvare le modifiche. Se dopo avere aggiunto o rimosso URL si chiude la finestra di dialogo senza prima avere scelto **OK**, le modifiche andranno perdute.  
  
## <a name="options"></a>Opzioni  
 **Indirizzo IP**  
 Identifica il computer server di report in una rete TCP/IP. I valori validi includono:  
  
-   **Tutti assegnati** : specifica che qualunque indirizzo IP assegnato al computer può essere utilizzato in un URL che punta a un'applicazione del server di report. Questo valore include anche i nomi host descrittivi, ad esempio i nomi computer, che possono essere risolti da un DNS in un indirizzo IP assegnato al computer. Si tratta del valore predefinito per un URL di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   **Non assegnati** : specifica che il server di report accetterà qualsiasi richiesta per cui non esiste una corrispondenza esatta per l'indirizzo IP o il nome host. Non utilizzare questo valore se è già in uso in un'altra applicazione Web. In caso contrario, verrà interrotta l'esecuzione del servizio per l'altra applicazione.  
  
-   **127.0.0.1** : utilizzato per accedere a localhost. Tale indirizzo supporta l'amministrazione locale nel computer server di report. Se si seleziona solo questo valore, potranno accedere all'applicazione solo gli utenti connessi localmente al computer server di report.  
  
-   *Nnn.nnn.nnn.nnn* : indirizzo IPv4 di una scheda di rete nel computer. Se la rete utilizza l'indirizzamento IPv6, l'indirizzo IP sarà un valore a 128 bit 8 campi a 4 byte è simile al seguente formato: \<intestazione >:*nnnn:nnnn:nnnn:nnnn*.  
  
     Se si dispone di più schede, verrà visualizzato un indirizzo IP per ognuna. Se si seleziona solo questo valore, l'accesso all'applicazione sarà limitato all'indirizzo IP specificato e a qualsiasi nome host di cui il DNS esegue il mapping all'indirizzo. Non è possibile utilizzare localhost per accedere a un server di report, né utilizzare gli indirizzi IP di altre schede di rete installate nel computer server di report.  
  
 **Porta**  
 Consente di specificare la porta monitorata dal server di report per le richieste. Il numero di porta predefinito è 80. Se si utilizza la porta 80, non è necessario includerla nell'URL. Se si usa qualsiasi altro numero di porta, è sempre necessario includerlo nell'URL (ad esempio, http://localhost:8181/reports).  
  
 **Intestazione host**  
 Se è già stata definita un'intestazione host in un DNS risolto nel computer, è possibile specificare tale intestazione host in un URL configurato per l'accesso al server di report.  
  
 Un'intestazione host è un nome univoco che consente a più siti Web di condividere un singolo indirizzo IP e una singola porta. I nomi di intestazione host sono più semplici da ricordare e da digitare rispetto all'indirizzo IP e ai numeri di porta. Un esempio di un nome di intestazione host potrebbe essere www.adventure-works.com.  
  
 **Porta SSL**  
 Consente di specificare la porta per le connessioni SSL. Il numero di porta predefinito per SSL è 443.  
  
 **Certificato SSL**  
 Consente di specificare il nome di un certificato SSL installato nel computer. Se il certificato esegue il mapping a un carattere jolly, è possibile utilizzarlo per una connessione del server di report.  
  
 Consente di specificare il nome completo del computer per cui viene registrato il certificato. Il nome specificato deve essere identico al nome per cui viene registrato il certificato.  
  
 Per utilizzare questa opzione, è necessario disporre di un certificato installato. È inoltre necessario modificare l'impostazione di configurazione UrlRoot nel file RSReportServer.config in modo che specifichi il nome completo del computer per il quale viene registrato il certificato. Per altre informazioni, vedere [Configurare connessioni SSL in un server di report in modalità nativa](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Rilasciato a**  
 Indica il nome del computer per cui è stato creato il certificato.  
  
 **Aggiungi**  
 Consente di definire un URL aggiuntivo.  
  
 **Modifica**  
 Consente di modificare qualsiasi parte della sintassi dell'URL.  
  
 **Rimuovi**  
 Consente di cancellare una voce di URL dall'elenco.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Configurare un URL &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
