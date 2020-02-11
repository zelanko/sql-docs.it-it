---
title: Elemento HelpLink | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- HelpLink element
- SoapException class
ms.assetid: a4489103-a874-44c2-8f75-95cb238928ed
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7bdd18641663003a1878fe0af0ac1d39a16eda1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046025"
---
# <a name="helplink-element"></a>Elemento HelpLink
  L'elemento **HelpLink** della proprietà **Detail** è una stringa URL generata dal server di report. L'URL rimanda a una pagina Web gestita dal Supporto tecnico [!INCLUDE[msCoName](../../../includes/msconame-md.md)] e fornisce ulteriori informazioni e articoli della Knowledge Base su errori specifici che si verificano in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. La sintassi dell'URL è la seguente:  
  
 **http://** www.Microsoft.com**/****/** Products**/** ee transform. aspx **? Valore EvtSrc**=__ **&valore EvtID**=__ **&valore ProdName**=__ **&**=_valore_ ProdVer  
  
 Nella tabella seguente sono elencati gli argomenti dell'URL **HelpLink**.  
  
|Argomento|valore|  
|--------------|-----------|  
|**EvtSrc**|"Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings"|  
|**EvtID**|Codice di errore del server di report, ad esempio rsReservedItem.|  
|**ProdName**|"Microsoft SQL%20Server%20Reporting%20Services". Il valore del nome del prodotto è codificato nell'URL.|  
|**ProdVer**|Numero di versione di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Il valore "8,00" indica [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].|  
  
 Nell'esempio seguente viene illustrato l'URL **HelpLink** restituito per il codice `rsReservedItem`di errore. Questo errore si verifica quando un utente tenta di modificare o di eliminare un elemento riservato in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]:  
  
```  
https://www.microsoft.com/products/ee/transform.aspx?  
EvtSrc=Microsoft.ReportingServices.Diagnostics.ErrorStrings.resources.Strings  
&EvtID=rsReservedItem&ProdName=Microsoft%20SQL%20Server%20Reporting%20Services&ProdVer=8.00  
```  
  
 È possibile accedere all'elemento **HelpLink** nel codice usando la classe **SoapException**.  
  
```vb  
Try  
   rs.DeleteItem("/Report1")  
  
Catch e As SoapException  
   Console.WriteLine(e.Detail("HelpLink").InnerXml)  
End Try  
```  
  
```csharp  
try  
{  
   rs.DeleteItem("/Report1");  
}  
  
catch (SoapException e)  
{  
   Console.WriteLine(e.Detail["HelpLink"].InnerXml);  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione alla gestione delle eccezioni in Reporting Services](../introducing-exception-handling-in-reporting-services.md)   
 [Classe SoapException di Reporting Services](reporting-services-soapexception-class.md)   
 [Uso della proprietà Detail per la gestione di errori specifici](../best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
