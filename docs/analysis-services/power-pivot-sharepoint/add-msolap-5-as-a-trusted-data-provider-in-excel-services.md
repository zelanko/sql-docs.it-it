---
title: Aggiungere MSOLAP.5 come Provider di dati attendibile in Excel Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d7576aadda3739709acdffcb1b2419c20d39ed4e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68164450"
---
# <a name="add-msolap5-as-a-trusted-data-provider-in-excel-services"></a>Aggiungere MSOLAP.5 come provider di dati attendibile in Excel Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  MSOLAP.5 si riferisce al provider OLE DB di Analysis Services per SQL Server 2012. Excel Services deve considerare attendibile questo provider prima di effettuare la richiesta di connessione che comporta la disponibilità di dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in un server.  
  
 Se [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint è stato configurato usando lo strumento di configurazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , MSOLAP.5 potrebbe già essere un provider attendibile perché lo strumento include un'azione che soddisfa questo requisito. Se tuttavia si usa PowerShell o Amministrazione centrale oppure se l'azione del provider attendibile è stata esclusa nello strumento di configurazione, il provider potrebbe essere mancante ed è quindi necessario aggiungerlo durante la configurazione della farm per l'accesso ai dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 È sufficiente eseguire questo passaggio una volta per ogni applicazione di servizio Excel Services.  
  
 Per ogni server fisico che gestisce una richiesta di dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , ad esempio un server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint o un server Excel Services, il provider OLE DB deve essere installato nel computer. Un'installazione di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint include sempre il provider OLE DB, ma se Excel Services è in esecuzione in un computer su cui non è disponibile [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint, è necessario installare manualmente il provider. Per altre informazioni, vedere [Installazione del provider OLE DB di Analysis Services nei server di SharePoint](http://msdn.microsoft.com/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
## <a name="add-a-trusted-provider-to-excel-services"></a>Aggiungere un provider attendibile a Excel Services  
  
1.  In Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**, quindi fare clic sull'applicazione di servizio Excel Services.  
  
2.  Fare clic su **Provider di dati attendibili**.  
  
3.  Verificare che MSOLAP.5 sia visualizzato nell'elenco. A seconda di come è stato configurato [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint, MSOLAP.5 potrebbe già essere considerato attendibile.  
  
4.  Se non è elencato, fare clic su **Aggiungi provider di dati attendibile**.  
  
5.  In ID provider, digitare **MSOLAP.5**.  
  
6.  Per Tipo di provider, assicurarsi che sia selezionato OLE DB.  
  
7.  In Descrizione provider digitare **Provider Microsoft OLE DB per OLAP Services 11.0**.  
  
  
