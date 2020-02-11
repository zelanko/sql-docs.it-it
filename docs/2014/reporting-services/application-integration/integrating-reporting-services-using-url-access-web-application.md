---
title: Uso dell'accesso con URL in un'applicazione Web | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- links [Reporting Services], URL access
- URL access [Reporting Services], Web applications
- POST requests
- direct addressing [Reporting Services]
- Web applications [Reporting Services]
- hyperlinks [Reporting Services]
ms.assetid: 39e7918c-ad2d-4ca6-b099-2dd4dbdb83dc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6a8625af05b13331d513608bc20eb8dd9678d01a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62714578"
---
# <a name="using-url-access-in-a-web-application"></a>Utilizzo dell'accesso con URL in un'applicazione Web
  L'accesso con URL in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è progettato in maniera specifica per consentire l'accesso ai singoli report in una rete. Questo tipo di accesso è ottimale per l'integrazione delle funzionalità di visualizzazione e navigazione del report in un'applicazione Web personalizzata. Per utilizzare l'accesso con URL nelle applicazioni Web, è possibile:  
  
-   Indirizzare un URL a un server di report specifico da un portale o un sito Web.  
  
-   Utilizzare un metodo POST di un form e passare i parametri della stringa di query a un URL del server di report utilizzando i campi del form.  
  
## <a name="url-access-through-direct-addressing"></a>Accesso con URL tramite indirizzamento diretto  
 Per accedere a un elemento di un server di report o di un database del server di report utilizzando un URL, è sufficiente fornire l'indirizzo dell'URL da un browser o un'applicazione. È inoltre possibile fornire parametri dell'URL che possono influire sull'aspetto del report o della risorsa a cui si accede. Un URL può puntare a un server di report tramite la barra degli indirizzi di un browser oppure può essere l'origine di un oggetto **IFrame** che fa parte di un portale o un'applicazione Web di dimensioni più grandi. È possibile includere collegamenti ipertestuali ai report in diverse pagine Web del portale, nonché impostare come destinazione un frame specifico per il report oppure aprire una nuova finestra del browser nel processo.  
  
 Nell'esempio seguente il collegamento ipertestuale punta a un frame denominato "main" che potrebbe essere diverso da quello che include il collegamento ipertestuale. Il collegamento ipertestuale potrebbe fare parte del portale Web.  
  
```  
<a href="http://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main" target="main" >  
   Click here for the Territory Sales Drilldown sample report  
</a>  
```  
  
 Nell'esempio precedente l'impostazione relativa alle informazioni sul dispositivo, **LinkTarget**, viene passata con un valore "main" nella stringa di query dell'URL. In questo modo, anche qualsiasi collegamento ipertestuale drill-through nel report punta al frame denominato "main".  
  
 Per altre informazioni sulle impostazioni relative alle informazioni sul dispositivo, vedere [Passaggio delle impostazioni relative alle informazioni sul dispositivo alle estensioni per il rendering](../report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
 Si noti che in numerosi server e browser il numero di caratteri consentito in un URL è limitato. In alcuni casi, è previsto un limite di 256 caratteri. Per aggirare questa limitazione, è possibile utilizzare richieste POST con invio del form.  
  
> [!NOTE]  
>  In Internet Explorer la lunghezza massima per gli URL è di 2.083 caratteri. Questo limite si applica agli URL delle richieste sia POST che GET. Per POST, tuttavia, non vi è un limite imposto dalla dimensione dell'URL per l'invio di coppie nome/valore come parte di un form, in quanto il trasferimento avviene nell'intestazione e non nell'URL.  
  
## <a name="url-access-through-a-form-post-method"></a>Accesso con URL tramite un metodo POST del form  
 Quando un utente richiede dati da un server di report utilizzando l'accesso con URL, la richiesta HTTP utilizza il metodo GET. Si tratta di un'operazione equivalente all'invio di un form con METHOD = "GET". Per le richieste di URL o l'invio di form con METHOD = "GET" il limite è definito dal numero massimo di caratteri che possono essere elaborati da un server o da un browser.  
  
 Con le richieste POST (METHOD = "POST" e campi di input), le coppie nome/valore vengono trasferite nell'intestazione e non nell'URL. Le coppie nome/valore della stringa di query non fanno pertanto parte dell'URL ed è quindi possibile fornire elenchi di parametri molto più lunghi e complessi.  
  
 Se si utilizza l'accesso diretto, un utente può vedere l'URL per il server di report e potrebbe modificare la stringa di query o annotare la richiesta URL specifica e i parametri del server di report per utilizzarli successivamente.  
  
 L'esempio HTML seguente illustra l'utilizzo di un form che consente di puntare a un server di report con un URL specifico e di passare i parametri della stringa di query come parte dei campi di input del form.  
  
```  
<FORM id="frmRender" action="http://server/reportserver?/SampleReports/  
   Territory Sales Drilldown" method="post" target="_self">  
   <INPUT type="hidden" name="rs:Command" value="Render">   
   <INPUT type="hidden" name="rc:LinkTarget" value="main">  
   <INPUT type="hidden" name="rs:Format" value="HTML4.0">  
   <INPUT type="submit" value="Button">  
</FORM>  
```  
  
 Nell'esempio precedente se un utente fa clic sul pulsante sul form, il server di report restituisce un report visualizzabile in formato HTML indirizzato al frame corrente. Una stringa di accesso con URL paragonabile potrebbe essere simile alla seguente:  
  
```  
http://server/reportserver?/SampleReports/Territory Sales   
Drilldown&rs:Command=Render&rc:LinkTarget=main&rs:Format=HTML4.0  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Integrazione di Reporting Services in applicazioni](../application-integration/integrating-reporting-services-into-applications.md)   
 [Integrazione di Reporting Services tramite l'accesso con URL](integrating-reporting-services-using-url-access.md)   
 [Utilizzo dell'accesso con URL in un'applicazione Windows](integrating-reporting-services-using-url-access-windows-application.md)   
 [Accesso con URL &#40;SSRS&#41;](../url-access-ssrs.md)  
  
  
