---
title: Classe SoapException di Reporting Services | Microsoft Docs
description: Informazioni su come risolvere gli errori specifici della classe SoapException di Reporting Services che potrebbero verificarsi.
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], SoapException class
- SoapException class
ms.assetid: 2cec49ee-20b1-40eb-a75b-0908d9c05b34
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1e5dca57a7ccc4d3ca08f4b1c22e460747cc6d46
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "80215726"
---
# <a name="reporting-services-soapexception-class"></a>Classe SoapException di Reporting Services
  È necessario fornire una soluzione per errori specifici di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] che potrebbero verificarsi. In un'applicazione in cui viene chiesto all'utente di creare una cartella, l'utente potrebbe ad esempio tentare di creare una cartella che esiste già. Lo sviluppatore non dispone di controllo sull'immissione dell'utente nei campi relativi al nome e al percorso della cartella nell'applicazione, ma dispone di controllo sull'esperienza utente nel caso in cui si tenti accidentalmente di creare un elemento che esiste già.  
  
 Per semplificare l'individuazione di condizioni di errore specifiche, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] classifica un codice di errore per l'eccezione e restituisce la classificazione dell'errore usando le proprietà della classe **SoapException**. Per altre informazioni, vedere "Classe SoapException" nella documentazione di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK.  
  
 La tabella seguente elenca le proprietà pubbliche della classe **SoapException**.  
  
|Proprietà pubblica|Descrizione|  
|---------------------|-----------------|  
|**Actor**|Codice che ha causato l'eccezione. Il valore è l'URL del metodo del servizio Web.|  
|**Detail**|Informazioni sull'errore specifiche dell'applicazione. Il valore viene impostato dal server di report ed è in formato XML. Per altre informazioni, vedere [Proprietà Detail](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md) e [Uso della proprietà Detail per la gestione di errori specifici](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md).|  
|**HelpLink**|URL o URN di un file della Guida associato all'errore. Il valore viene in genere impostato dal servizio Web e un URL viene impostato su Guida e supporto tecnico [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Poiché [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] supporta più collegamenti alla Guida per gli errori che si verificano, il server di report imposta le informazioni sui collegamenti alla Guida come parte della proprietà **Detail**. Per altre informazioni, vedere [Elemento HelpLink](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md).|  
|**Messaggio**|Messaggio descrittivo localizzato in cui viene descritto l'errore. Il testo può venire visualizzato nell'interfaccia utente dell'applicazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione alla gestione delle eccezioni in Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Tabella degli errori SoapException](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  
