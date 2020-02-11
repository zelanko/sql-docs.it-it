---
title: Monitoraggio per le esecuzioni di pacchetti e altre operazioni | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cbbcd79f-ab9b-46ec-84cb-4821c1d16b99
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6f6a4e147c90fe7c4f25f5c8b821b4787ec3be71
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62766983"
---
# <a name="monitoring-for-package-executions-and-other-operations"></a>Monitoraggio per le esecuzioni di pacchetti e altre operazioni
  È possibile monitorare esecuzioni di pacchetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , convalide di progetto e altre operazioni di usando uno o più strumenti tra quelli indicati di seguito. Alcuni strumenti, tra cui le scelte dei dati, sono disponibili solo per i progetti distribuiti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
-   Log  
  
     Per altre informazioni, vedere [registrazione di Integration Services &#40;SSIS&#41;](integration-services-ssis-logging.md).  
  
-   Report  
  
     Per altre informazioni, vedere [report per il server Integration Services](../reports-for-the-integration-services-server.md).  
  
-   Viste  
  
     Per altre informazioni, vedere [viste &#40;Catalogo di Integration Services&#41;](/sql/integration-services/system-views/views-integration-services-catalog).  
  
-   Contatori delle prestazioni  
  
     Per altre informazioni, vedere [i contatori delle prestazioni](performance-counters.md).  
  
-   Scelte dei dati  
  
## <a name="operation-types"></a>Tipi di operazione  
 Nel catalogo `SSISDB` vengono monitorati numerosi tipi diversi di operazioni nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A ogni operazione possono essere associati più messaggi. Ogni messaggio può essere classificato in uno dei molti tipi diversi. Ad esempio, un messaggio può essere informativo, di avviso o di errore. Per l'elenco completo dei tipi di messaggi, vedere la documentazione relativa alla vista Transact-SQL [catalog.operation_messages &#40;Database SSISDB&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database). Per l'elenco completo dei tipi di operazioni, vedere [catalog.operations &#40;Database SSISDB&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database).  
  
 Nove diversi tipi di stato consentono di indicare lo stato di un'operazione. Per l'elenco completo dei tipi di stato, vedere la vista [catalog.operations &#40;Database SSISDB&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database).  
  
## <a name="related-content"></a>Contenuto correlato  
 Intervento nel blog relativo alla [panoramica dell'API T-SQL SSIS](https://go.microsoft.com/fwlink/?LinkId=249051)su blogs.msdn.com.  
  
  
