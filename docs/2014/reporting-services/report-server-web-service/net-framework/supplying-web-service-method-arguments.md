---
title: Impostazione degli argomenti dei metodi del servizio Web | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, methods
- Web service [Reporting Services], methods
- methods [Reporting Services], arguments
- XML Web service [Reporting Services], methods
ms.assetid: f7b9ca05-fc4c-4b30-8e5d-172dd0f4a832
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3ef5188934628589751fe92d1839da0efb265766
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60154397"
---
# <a name="supplying-web-service-method-arguments"></a>Impostazione degli argomenti dei metodi del servizio Web
  Un metodo del servizio Web ReportServer invia una richiesta al servizio a un URL specifico utilizzando SOAP tramite HTTP. Il servizio riceve la richiesta, la elabora e restituisce una risposta. Queste richieste e risposte hanno il formato di documenti XML.  
  
## <a name="optional-parameters"></a>Parametri facoltativi  
 In alcuni casi, un metodo del servizio Web può avere parametri di input facoltativi. Anche se un parametro di input per un metodo del servizio Web è facoltativo, è comunque necessario includerlo e impostare il relativo valore su `null` (`Nothing` in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]). Impostando il valore di un parametro su `null` si imposta il valore dell'elemento per tale parametro nella richiesta SOAP su `null`.  
  
 Nell'esempio seguente viene utilizzato il metodo <xref:ReportService2010.ReportingService2010.CreateFolder%2A> per creare una nuova cartella denominata Product Sales nella cartella Sales. Fornendo un valore `null` per le proprietà della cartella, non vengono fornite proprietà specifiche dell'utente per la cartella:  
  
```  
// C#  
rs.CreateFolder("Product Sales", "/Sales", null);  
```  
  
## <a name="complex-data-types"></a>Tipi di dati complessi  
 La classe principale del servizio Web ReportServer è <xref:ReportService2010.ReportingService2010> e viene utilizzata per richiamare le operazioni SOAP o i metodi Web della classe proxy. Per supportare questa classe e i relativi metodi, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] include tipi di dati complessi definiti dall'utente specifici dei parametri di input e output dei metodi del servizio Web. Questi tipi di dati complessi fanno parte della classe proxy generata che è possibile usare per lo sviluppo in ambiente [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
 Quando si genera una classe proxy, i tipi di dati complessi definiti nel file WSDL vengono rappresentati dalle classi proxy, che includono proprietà che corrispondono ai vari elementi SOAP dei tipi di dati complessi. Le sequenze di questi tipi di dati diventano matrici di oggetti che è possibile enumerare nel codice. In questo modo, non è più necessario utilizzare direttamente le strutture XML inviate nei messaggi SOAP. La conversione viene gestita da [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni tramite servizio Web e .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servizio Web ReportServer](../report-server-web-service.md)   
 [Riferimento tecnico &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
