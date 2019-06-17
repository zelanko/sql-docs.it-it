---
title: Using Secure Web Service Methods (Uso di metodi del servizio Web protetti) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], secure connections
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: 87329299-c2ea-4517-9148-d855726768a9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e88a164602f9bbe6ad42c3897285a484cac94466
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62518661"
---
# <a name="using-secure-web-service-methods"></a>Utilizzo di metodi del servizio Web protetti
  Alcuni metodi del servizio Web ReportServer possono richiedere una connessione protetta per essere richiamati. I metodi che richiedono una connessione protetta sono determinati dall'impostazione `SecureConnectionLevel` nel file RSReportServer.config. Il valore dell'impostazione è un valore intero con un intervallo valido compreso tra 0 e un numero superiore. Nella tabella seguente vengono descritti questi valori.  
  
|Level|Descrizione|  
|-----------|-----------------|  
|**0**|Livello di sicurezza basso. Le chiamate effettuate all'API SOAP di Reporting Services non richiedono una connessione protetta.|  
|Maggiore di **0**|Livello di sicurezza medio. Tutte le chiamate effettuate all'API SOAP di Reporting Services richiedono una connessione protetta.|  
  
 È possibile utilizzare il metodo <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> del servizio Web per restituire un elenco di metodi del servizio Web che richiedono una connessione protetta in base alla configurazione corrente del server di report. In uno scenario SSL è necessario valutare l'elenco di metodi restituiti da <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> e modificare il nome dello schema dell'URI del servizio Web in "https" o "http", a seconda del metodo chiamato.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni tramite servizio Web e .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servizio Web ReportServer](../report-server-web-service.md)  
  
  
