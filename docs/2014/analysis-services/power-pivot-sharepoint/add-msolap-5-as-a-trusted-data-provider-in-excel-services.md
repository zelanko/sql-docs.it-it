---
title: Aggiungere MSOLAP.5 come Provider di dati attendibile in Excel Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: c1f40fa4-de6d-41ee-8124-14b4d65988f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 354ca92c8ed66c7669863cc234fe4999ab95e662
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743297"
---
# <a name="add-msolap5-as-a-trusted-data-provider-in-excel-services"></a>Aggiungere MSOLAP.5 come provider di dati attendibile in Excel Services
  MSOLAP.5 si riferisce al provider OLE DB di Analysis Services per SQL Server 2012. In Excel Services questo provider deve essere considerato attendibile prima di effettuare la richiesta di connessione che comporta la disponibilità di dati PowerPivot in un server.  
  
 Se è stato configurato PowerPivot per SharePoint utilizzando lo strumento di configurazione PowerPivot, MSOLAP.5 potrebbe già essere un provider attendibile perché lo strumento include un'azione che soddisfa questo requisito. Se tuttavia si utilizza PowerShell o Amministrazione centrale oppure se l'azione del provider attendibile è stata esclusa nello strumento di configurazione, è possibile che il provider risulti mancante ed è quindi necessario aggiungerlo durante la configurazione della farm per l'accesso ai dati PowerPivot.  
  
 È sufficiente eseguire questo passaggio una volta per ogni applicazione di servizio Excel Services.  
  
 Ogni server fisico che gestisce una richiesta di dati PowerPivot, ad esempio un server PowerPivot per SharePoint o un server Excel Services, deve disporre del provider OLE DB installato nel computer. Un'installazione di PowerPivot per SharePoint include sempre il provider OLE DB, ma se Excel Services è in esecuzione in un computer che non dispone di PowerPivot per SharePoint, è necessario installare manualmente il provider. Per altre informazioni, vedere [Installazione del provider OLE DB di Analysis Services nei server di SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).  
  
## <a name="add-a-trusted-provider-to-excel-services"></a>Aggiungere un provider attendibile a Excel Services  
  
1.  In Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**, quindi fare clic sull'applicazione di servizio Excel Services.  
  
2.  Fare clic su **Provider di dati attendibili**.  
  
3.  Verificare che MSOLAP.5 sia visualizzato nell'elenco. A seconda di come è stato configurato PowerPivot per SharePoint, MSOLAP.5 potrebbe già essere considerato attendibile.  
  
4.  Se non è elencato, fare clic su **Aggiungi provider di dati attendibile**.  
  
5.  In ID provider, digitare `MSOLAP.5`.  
  
6.  Per Tipo di provider, assicurarsi che sia selezionato OLE DB.  
  
7.  In Descrizione provider digitare **Provider Microsoft OLE DB per OLAP Services 11.0**.  
  
  
