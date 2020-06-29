---
title: Novità di&#39;(Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, what's new
- what's new [Integration Services]
ms.assetid: da6999c7-e5e3-4a59-a284-1da635995af1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 84f0b668407c89e1d6acc3c8cfbda73f129ca19a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439858"
---
# <a name="what39s-new-integration-services"></a>Novità di&#39;(Integration Services)
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]è invariato rispetto alla versione precedente.  
  
 Per informazioni su altri [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] prodotti e tecnologie, vedere Novità [di SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md).  
  
 Per ulteriori informazioni sulle modifiche correlate a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Business Intelligence, vedere Novità [di Analysis Services e Business Intelligence](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services).  
  
##  <a name="rich-xml-validation-output-in-the-xml-task"></a><a name="ValidateXML"></a> Output di convalida XML avanzato in Attività XML  
 È possibile convalidare documenti XML e ottenere output avanzato degli errori abilitando la proprietà `ValidationDetails` dell'Attività XML. Prima che fosse disponibile la proprietà `ValidationDetails`, la convalida XML da parte dell'Attività XML restituiva solo un risultato di tipo True o False, senza informazioni sugli errori o sulle rispettive posizioni. Attualmente, quando si imposta `ValidationDetails` su True, il file di output contiene informazioni dettagliate su ogni errore, inclusi il numero di riga e la posizione. È possibile usare questa informazione per comprendere, individuare e risolvere gli errori nei documenti XML. Per ulteriori informazioni, vedere [Validate XML with the XML Task](control-flow/xml-task.md).  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] ha introdotto la proprietà `ValidationDetails` in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 2. Questa nuova proprietà non è stata annunciata o documentata in quel momento. La proprietà `ValidationDetails` è disponibile anche in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] e in SQL Server 2016.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità supportate dalle edizioni di SQL Server 2014](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
  
