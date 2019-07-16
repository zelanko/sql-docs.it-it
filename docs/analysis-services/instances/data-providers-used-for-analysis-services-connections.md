---
title: Provider di dati utilizzati per le connessioni di Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f5ba97f90b877896d68cd62598f11d0845fb698e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209535"
---
# <a name="client-libraries-data-providers-used-for-analysis-services-connections"></a>Librerie client (provider di dati) usate per le connessioni di Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

Analysis Services offre tre librerie client, anche noto come **provider di dati**, per l'accesso ai dati da strumenti e applicazioni client e server. Strumenti come SQL Server Management Studio e SSDT e applicazioni, come Power BI Desktop ed Excel connettersi ad Analysis Services usando queste librerie. Due delle librerie client, ADOMD.NET e Analysis Services Management Objects (AMO) sono librerie client gestite. Il provider OLE DB per Analysis Services (MSOLAP DLL) è una libreria client nativa. Le librerie client sono gli stessi per SQL Server Analysis Services e Azure Analysis Services.
  
##  <a name="bkmk_downloadsite"></a> Come ottenere le versioni più recenti  
 La versione installata in un computer client deve corrispondere alla versione principale del server che fornisce i dati. Se l'installazione del server è più recente dei provider di dati installati nelle workstation in rete, potrebbe essere necessario installare librerie più recenti.  

Librerie client incluse nei precedenti Feature Pack di SQL Server corrispondono a tale versione SQL; Tuttavia, potrebbero non essere la versione più recente. La connessione ad Azure Analysis Services potrebbe richiedere versioni successive. Tutte le versioni sono compatibili con le versioni precedenti.

Per ottenere la versione più recente, vedere [librerie Client per la connessione ad Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-data-providers). 
  
## <a name="see-also"></a>Vedere anche  
 [Connettersi ad Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)  
  
  
