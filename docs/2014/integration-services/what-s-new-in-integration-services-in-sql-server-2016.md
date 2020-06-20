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
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 1d17451c8706722b0dac21d777f35a17fe319799
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972471"
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
  
  
