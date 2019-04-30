---
title: Accedere a elementi del Server di Report tramite accesso con URL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- referencing URL items for report server access
- URL access [Reporting Services], report servers
ms.assetid: a58b4ca6-129d-45e9-95c7-e9169fe5bba4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3a345cd609c4cfd79f9e93a2b63e71bbddde36ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233563"
---
# <a name="access-report-server-items-using-url-access"></a>Elementi del Server di Report l'accesso usando l'accesso con URL
  In questo argomento viene descritto come accedere a elementi catalogo di tipi diversi in un report i dati del server o in un sito di SharePoint usando *rs: Command*=*valore*.  
  
 Non è necessario aggiungere questa stringa del parametro. Se viene omesso, il server di report restituisce il tipo di elemento e il valore del parametro appropriato viene selezionato automaticamente. Se tuttavia si utilizza il *rs: Command*=*valore* stringa nell'URL migliora le prestazioni del server di report.  
  
 Si noti il `_vti_bin` sintassi del proxy negli esempi seguenti. Per altre informazioni sull'utilizzo la sintassi del proxy, vedere [riferimento ai parametri di accesso URL](url-access-parameter-reference.md).  
  
## <a name="access-a-report"></a>Accedere a un Report  
 Per visualizzare un report nel browser, usare il *rs: Command*=*rendering* parametro. Ad esempio:  
  
 `Native` `http://myrshost/reportserver?/Sales/YearlySalesByCategory&rs:Command=Render`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales/YearlySalesByCategory&rs:Command=Render`  
  
> [!TIP]  
>  È importante includere l'URL di `_vti_bin` sintassi del proxy per instradare la richiesta attraverso SharePoint e [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] proxy HTTP. Il proxy aggiunge un contesto per la richiesta HTTP, contesto necessario per garantire l'esecuzione corretta del report per il server di report in modalità SharePoint.  
  
## <a name="access-a-resource"></a>Accedere a una risorsa  
 Per accedere a una risorsa, usare il *rs: Command*=*GetResourceContents* parametro. Se la risorsa è compatibile con il browser, ad esempio un'immagine, viene aperto nel browser. In caso contrario, viene chiesto di aprire o salvare il file o la risorsa disco.  
  
 `Native` `http://myrshost/reportserver?/Sales/StorePicture&rs:Command=GetResourceContents`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales/StorePicture.jpg&rs:Command=GetResourceContents`  
  
## <a name="access-a-data-source"></a>Accedere a un'origine dati  
 Per accedere a un'origine dati, usare il *rs: Command*=*GetDataSourceContents* parametro. Se il browser supporta XML, la definizione dell'origine dati viene visualizzata se sei un utente autenticato con `Read Contents` l'autorizzazione per l'origine dati. Ad esempio:  
  
 `Native` `http://myrshost/reportserver?/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales/AdventureWorks2012&rs:Command=GetDataSourceContents`  
  
 La struttura XML potrebbe essere simile all'esempio seguente:  
  
```  
<DataSourceDefinition>  
   <Extension>SQL</Extension>  
   <ConnectString>Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security Info=False;Initial Catalog=AdventureWorks2012;Data Source=MYSERVER1;</ConnectString>  
   <CredentialRetrieval>Integrated</CredentialRetrieval>  
   <WindowsCredentials>False</WindowsCredentials>  
   <ImpersonateUser>False</ImpersonateUser>  
   <Prompt />  
   <Enabled>True</Enabled>  
</DataSourceDefinition>  
```  
  
 La stringa di connessione viene restituita in base il **SecureConnectionLevel** l'impostazione del server di report. Per altre informazioni sul **SecureConnectionLevel** ll'impostazione, vedere [usando metodi del servizio Web protetti](report-server-web-service/net-framework/using-secure-web-service-methods.md).  
  
## <a name="access-the-contents-of-a-folder"></a>Accedere al contenuto di una cartella  
 Per accedere al contenuto di una cartella, usare il *rs: Command*=*GetChildren* parametro. Viene restituita una pagina generica di navigazione della cartella che contiene i collegamenti per le sottocartelle, report, origini dati e le risorse nella cartella richiesta. Ad esempio:  
  
 `Native` `http://myrshost/reportserver?/Sales&rs:Command=GetChildren`  
  
 `SharePoint` `http://myspsite/subsite/_vti_bin/reportserver? http://myspsite/subsite/Sales&rs:Command=GetChildren`  
  
 L'interfaccia utente visualizzata è simile alla modalità utilizzata dall'esplorazione directory [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Information Server (IIS). Il numero di versione, inclusi il numero di build del server di report viene visualizzato anche sotto l'elenco della cartella.  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso con URL &#40;SSRS&#41;](url-access-ssrs.md)   
 [Riferimento ai parametri di accesso URL](url-access-parameter-reference.md)  
  
  
