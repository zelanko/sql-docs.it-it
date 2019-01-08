---
title: Usare sottoscrizioni personali | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], My Subscriptions page
- My Subscriptions page [Reporting Services]
ms.assetid: e96623ba-677e-4748-8787-f32bed3b5c12
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 63154af6d155dd05e1f07d38185830fefc30068a
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53371363"
---
# <a name="use-my-subscriptions"></a>Utilizzare Sottoscrizioni personali
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Gestione report è disponibile un' **sottoscrizioni personali** pagina che consente di organizzare tutte le sottoscrizioni in un'unica posizione. La pagina Sottoscrizioni personali consente infatti di visualizzare, modificare ed eliminare le sottoscrizioni esistenti. Non è tuttavia possibile utilizzarla per creare sottoscrizioni.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] |  
  
 Nella pagina Sottoscrizioni personali è possibile ordinare le sottoscrizioni per cartella, report, descrizione, trigger, data di ultima esecuzione o stato. Tutti i valori sono in ordine alfabetico, ad eccezione di quelli del campo Ultima esecuzione, che sono in ordine cronologico.  
  
 Nella pagina Sottoscrizioni personali sono visualizzate solo le sottoscrizioni create dall'utente che vi accede. Non sono elencate né sottoscrizioni di proprietà di altri utenti, nemmeno se questi sono sottoscrittori delle sottoscrizioni elencate, né sottoscrizioni guidate dai dati.  
  
 Non è possibile individuare una sottoscrizione eseguendo ricerche per nome o altri tipi di ricerche, ad esempio in base al trigger, alle informazioni di stato e così via. Per altre informazioni, vedere [creare, modificare ed eliminare sottoscrizioni Standard &#40;Reporting Services in modalità nativa&#41;](create-and-manage-subscriptions-for-native-mode-report-servers.md).  
  
## <a name="how-to-use-my-subscriptions"></a>Come utilizzare la pagina Sottoscrizioni personali  
 La pagina Sottoscrizioni personali è disponibile attraverso Gestione report. Per accedere alla pagina sottoscrizioni personali, fare clic su **sottoscrizioni personali** sulla barra degli strumenti globale di gestione Report.  
  
## <a name="use-windows-powershell-to-list-mysubscriptions"></a>Utilizzare Windows PowerShell per elencare MySubscriptions  
 ![Contenuto correlato di PowerShell](../media/rs-powershellicon.jpg "Contenuto correlato di PowerShell")  
  
 Tramite il seguente script di PowerShell verrà restituito l'elenco delle sottoscrizioni e delle proprietà di sottoscrizione per l'utente corrente. Per altre informazioni, vedere [Metodo ReportingService2010.ListMySubscriptions](https://technet.microsoft.com/library/reportservice2010.reportingservice2010.listmysubscriptions.aspx).  
  
```  
#server -  all subscriptions of the current user at the given server or site  
$server="[server name]/reportserver"  
$rs2010 = New-WebServiceProxy -Uri "http://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
  
$subscriptions=ListMySubscriptions(ItemPathOrSiteURL)  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status  
#uncomment the following to list all the subscription properties  
#$subscriptions  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Sottoscrizioni guidate dai dati](data-driven-subscriptions.md)   
 [Sottoscrizioni e recapito &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [Creare e gestire sottoscrizioni per server di report in modalità nativa](../create-manage-subscriptions-native-mode-report-servers.md)  
  
  
