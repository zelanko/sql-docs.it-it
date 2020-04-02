---
title: Using Secure Web Service Methods (Uso di metodi del servizio Web protetti) | Microsoft Docs
description: Richiedere una connessione sicura per i metodi del servizio Web ReportServer con l'impostazione SecureConnectionLevel nel file di configurazione RSReportServer.
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], secure connections
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: 87329299-c2ea-4517-9148-d855726768a9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ddbc92de40fa15840e9c12cd482b1488bd54f7b9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "79509602"
---
# <a name="using-secure-web-service-methods"></a>Utilizzo di metodi del servizio Web protetti
  Alcuni metodi del servizio Web ReportServer possono richiedere una connessione protetta per essere richiamati. I metodi che richiedono una connessione protetta sono determinati dall'impostazione **SecureConnectionLevel** nel file RSReportServer.config. Il valore dell'impostazione è un valore intero con un intervallo valido compreso tra 0 e un numero superiore. Nella tabella seguente vengono descritti questi valori.  
  
|Level|Descrizione|  
|-----------|-----------------|  
|**0**|Livello di sicurezza basso. Le chiamate effettuate all'API SOAP di Reporting Services non richiedono una connessione protetta.|  
|Maggiore di **0**|Livello di sicurezza medio. Tutte le chiamate effettuate all'API SOAP di Reporting Services richiedono una connessione protetta.|  
  
 È possibile utilizzare il metodo <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> del servizio Web per restituire un elenco di metodi del servizio Web che richiedono una connessione protetta in base alla configurazione corrente del server di report. In uno scenario SSL è necessario valutare l'elenco di metodi restituiti da <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> e modificare il nome dello schema dell'URI del servizio Web in "https" o "http", a seconda del metodo chiamato.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni tramite servizio Web e .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servizio Web ReportServer](../../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
