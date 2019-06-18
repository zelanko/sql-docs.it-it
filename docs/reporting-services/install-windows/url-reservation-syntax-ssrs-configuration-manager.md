---
title: Sintassi delle prenotazioni URL (Gestione configurazione SSRS) | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
ms.assetid: 30e4be2e-e65d-462c-895a-5a0a636d042f
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 115035e4ab8711a251ec8d2ac253b9987b5ebe66
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62651668"
---
# <a name="url-reservation-syntax--ssrs-configuration-manager"></a>Sintassi delle prenotazioni URL (Gestione configurazione SSRS)
  In questo argomento vengono descritte le parti della stringa URL per il servizio Web ReportServer e per Gestione report. La stringa URL archiviata internamente ha una struttura diversa da un URL digitato nella barra degli indirizzi di una finestra del browser. La stringa della prenotazione URL viene visualizzata nella finestra Risultati dello strumento di configurazione di Reporting Services quando si configura un URL e nel file RSReportServer.config. Conoscere il modo in cui è definita la stringa URL può risultare utile ai fini della risoluzione dei problemi relativi alle prenotazioni URL o per eseguire una query su HTTP.SYS per visualizzare le prenotazioni URL interne definite nel server.  
  
## <a name="url-syntax"></a>Sintassi URL  
 Un URL del server di report viene archiviato nell'elemento **UrlString** e nell'elemento **VirtualDirectory** . Il motivo per cui **UrlString** e **VirtualDirectory** sono separati in elementi distinti è che si possono avere più stringhe URL ma solo un nome della directory virtuale per ogni applicazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 In HTTP.SYS la prenotazione URL include sia **UrlString** che **VirtualDirectory**. La sintassi per una prenotazione URL include le parti seguenti:  
  
 \<schema>://\<nomehost>:\<porta>/\<directoryvirtuale>  
  
 Nella tabella seguente vengono descritte tutte le proprietà e i valori validi per ciascuna.  
  
|Proprietà|Valori validi|Descrizione|  
|--------------|------------------|-----------------|  
|schema|http o https|Prefissi per connessioni SSL e non SSL.|  
|nomehost|Carattere jolly complesso (+), che equivale al valore **Tutti assegnati** per l'indirizzo IP.<br /><br /> Carattere jolly vulnerabile (\*), che equivale a un indirizzo IP di **Tutti non assegnati**.<br /><br /> Nome di dominio completo<br /><br /> Nome computer<br /><br /> Indirizzo IP (IPv4)<br /><br /> Indirizzo IP (IPv6)|Identifica il server in rete.<br /><br /> Il carattere jolly complesso (+) rappresenta l'impostazione predefinita. HTTP.SYS accetterà tutte le richieste su tutte le schede di rete per una combinazione specifica di porta e directory virtuale. Il server di report accetterà qualsiasi richiesta sulla porta.<br /><br /> Carattere jolly vulnerabile (\*). HTTP.SYS accetta tutte le richieste non gestite da altre prenotazioni URL su tutte le schede di rete per una combinazione specifica di porta e directory virtuale.<br /><br /> Il nome del computer è il nome NETBIOS del computer in rete.<br /><br /> Il nome di dominio completo include indirizzo del dominio e il nome del server, registrato con un controller di dominio o un DNS pubblico.<br /><br /> L'indirizzo IP (IPv4) è l'indirizzo IP di una scheda di rete nel computer in formato IPv4: *nnn.nnn.nnn.nnn*.<br /><br /> L'indirizzo IP (IPv6) è l'indirizzo IP di una scheda di rete nel computer in formato IPv6: \<intestazione>:\<intestazione>:*nnn.nnn.nnn.nnn*.|  
|Port|80<br /><br /> 443<br /><br /> \<personalizzata>|La porta 80 è la porta standard per le richieste HTTP a e da un server.<br /><br /> La porta 443 è la porta standard per le connessioni SSL.<br /><br /> È possibile utilizzare qualsiasi porta che non sia già riservata da un'altra applicazione.|  
|VirtualDirectory|ReportServer *[_NomeIstanza]*<br /><br /> Reports *[_NomeIstanza]*<br /><br /> \<personalizzata>|Specifica il nome dell'applicazione. Questo valore è una stringa. Per impostazione predefinita, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utilizza ReportServer e Report come nomi dell'applicazione per le applicazioni del servizio Web ReportServer e di Gestione report. Se lo si desidera, è possibile utilizzare nomi diversi.<br /><br /> Questo valore è obbligatorio. e identifica l'applicazione.<br /><br /> Specificare solo una directory virtuale per ogni istanza dell'applicazione. Per creare più URL per la stessa applicazione nella stessa istanza, creare più versioni di **UrlString**. Per creare nomi univoci delle directory virtuali per più istanze dell'applicazione, includere il nome di istanza nel nome della directory virtuale utilizzando il carattere di sottolineatura (_) per aggiungere il nome di istanza. *NomeIstanza* è facoltativo, ma è consigliato in presenza di più istanze nello stesso computer. Per altre informazioni sull'impostazione delle prenotazioni URL per le istanze denominate, vedere [Prenotazioni URL per le distribuzioni di più istanze del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/url-reservations-for-multi-instance-report-server-deployments.md).<br /><br /> Il valore per la directory virtuale non supporta la distinzione tra maiuscole e minuscole. È possibile utilizzare qualsiasi stringa, a condizione che non includa caratteri separatori dell'URL o codifica URL.|  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurare un URL &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
  
