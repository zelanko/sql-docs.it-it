---
title: Passare un parametro del report in un URL | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], passing parameters
- passing parameters [Reporting Services]
ms.assetid: f93a94cc-27b5-435a-aa85-69e6ec6459ad
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a78727d3b0ab3ee1909f9e86032ab392642b5603
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211210"
---
# <a name="pass-a-report-parameter-within-a-url"></a>Passare un parametro del report in un URL
  È possibile passare parametri del report a un report includendoli in un URL del report. Questi parametri URL non hanno il prefisso in quanto vengono passati direttamente al motore di elaborazione dei report.  
  
> [!IMPORTANT]  
>  È importante che nell'URL sia inclusa la sintassi proxy `_vti_bin` per indirizzare la richiesta tramite SharePoint e il proxy HTTP di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Tramite il proxy viene aggiunto del contesto alla richiesta HTTP. Questo contesto è necessario per garantire l'esecuzione corretta del report per i server di report in modalità SharePoint.  
>   
>  Se non si include la sintassi del proxy, è necessario anteporre al parametro il prefisso *rp:*.  
  
 Tutti i parametri di query possono disporre di parametri di report corrispondenti. Passare un parametro di query a un report passando il parametro di report corrispondente. Per altre informazioni, vedere [Compilare una query in Progettazione query relazionale &#40;Generatore report e SSRS&#41;](../reporting-services/report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md).  
  
> [!IMPORTANT]
>  Nei parametri dei report viene fatta distinzione tra maiuscole e minuscole.  
> 
> [!NOTE]
>  Ai parametri del report viene applicata la distinzione tra maiuscole e minuscole e in essi vengono utilizzati i caratteri speciali seguenti:  
> 
>  -   Qualsiasi spazio nella stringa dell'URL viene sostituito con i caratteri "% 20", in base agli standard di codifica degli URL.  
> -   Lo spazio nella parte di parametro dell'URL viene sostituito con un carattere più (+).  
> -   Il punto e virgola in una parte qualsiasi della stringa viene sostituito con i caratteri "%3A".  
> -   La codifica appropriata dell'URL deve venire eseguita automaticamente dai browser. Non è necessario codificare manualmente i caratteri.  
  
 Per impostare un parametro del report all'interno di un URL, utilizzare la sintassi seguente:  
  
```  
  
parameter=value  
```  
  
 Per specificare ad esempio due parametri, "ReportMonth" e "ReportYear", definiti in un report, usare l'URL seguente relativo a un server di report in modalità nativa:  
  
```  
https://myrshost/ReportServer?/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2&ReportMonth=3&ReportYear=2008  
```  
  
 Ad esempio, per specificare gli stessi due parametri definiti in un report, utilizzare l'URL seguente per un server di report in modalità integrata SharePoint. Si noti `/_vti_bin`:  
  
```  
https://myspsite/subsite/_vti_bin/reportserver?https://myspsite/subsite/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2.rdl&ReportMonth=3&ReportYear=2008  
```  
  
 Per passare un valore Null per un parametro, utilizzare la sintassi seguente:  
  
```  
  
parameter  
:isnull=true  
  
```  
  
 Ad esempio,  
  
```  
SalesOrderNumber:isnull=true  
```  
  
 Per passare un valore **Boolean** , usare 0 per false e 1 per true. Per passare un valore **Float** , includere il separatore decimale corrispondente alle impostazioni locali del server  
  
> [!NOTE]  
>  Se il report contiene un parametro del report con un valore predefinito e il valore della proprietà **Prompt** è **false** (ovvero la proprietà Richiesta all'utente non è selezionata in Gestione report), non è possibile passare un valore per tale parametro in un URL. In questo modo, gli amministratori possono impedire agli utenti finali di aggiungere o modificare i valori di determinati parametri dei report.  
  
##  <a name="bkmk_examples"></a> Esempi aggiuntivi  
 Nell'esempio di URL seguente sono inclusi spazi e più parametri  
  
-   Nel nome della cartella "SQL Server User Education Team" sono inclusi spazi che vengono sostituiti dal carattere "+".  
  
-   Nel nome del report "team project report" sono inclusi spazi che vengono sostituiti dal carattere "+".  
  
-   Passaggio di due parametri di "teamgrouping2" con un valore di "xgroup" e "teamgrouping1" con un valore di "ygroup".  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup  
```  
  
 Nell'esempio di URL seguente è incluso un parametro multivalore "OrderID". Il formato per il parametro multivalore prevede la ripetizione del nome del parametro per ogni valore.  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup&OrderID=747&OrderID=787&OrderID=12  
```  
  
 Nell'esempio di URL seguente viene passato un singolo parametro *SellStartDate* con un valore "7/1/2005", per un server di report in modalità nativa.  
  
```  
https://myserver/ReportServer/Pages/ReportViewer.aspx?%2fProduct_and_Sales_Report_AdventureWorks&SellStartDate=7/1/2005  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso con URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Riferimento ai parametri di accesso con URL](../reporting-services/url-access-parameter-reference.md)  
  
  
