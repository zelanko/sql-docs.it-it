---
title: Esecuzione di query su dati multidimensionali con MDX | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [Analysis Services], querying
ms.assetid: e0a5dd60-35a3-4a4f-b36f-52ecea814886
author: minewiskan
ms.author: owend
ms.openlocfilehash: 7b7589a98636e56e8c592cef213785544e18f4ea
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546201"
---
# <a name="querying-multidimensional-data-with-mdx"></a>Query su dati multidimensionali con MDX
  MDX (Multidimensional Expressions) è il linguaggio di query utilizzato per gestire e recuperare dati multidimensionali in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . MDX è basato sulla specifica XML for Analysis (XMLA), con estensioni specifiche per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . MDX usa espressioni costituite da identificatori, valori, istruzioni, funzioni e operatori che possono essere valutate da [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] per recuperare un oggetto, ad esempio un set o un membro, oppure un valore scalare, ad esempio una stringa o un numero.  
  
 Le query e le espressioni MDX in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] vengono utilizzate per eseguire le operazioni seguenti:  
  
-   Restituire i dati a un'applicazione client da un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cubo.  
  
-   Modellare i risultati delle query.  
  
-   Eseguire attività di progettazione per i cubi, tra cui la definizione di membri calcolati, set denominati, assegnazioni con ambito e indicatori di prestazioni chiave (KPI).  
  
-   Eseguire attività di amministrazione, inclusa la sicurezza di dimensioni e celle.  
  
 MDX è in apparenza simile sotto numerosi aspetti alla sintassi SQL in genere utilizzata con i database relazionali. MDX non è tuttavia un'estensione del linguaggio SQL, rispetto al quale presenta molte differenze. Per creare espressioni MDX per la progettazione o la sicurezza dei cubi oppure per creare query MDX in grado di restituire e modellare dati multidimensionali, è necessario conoscere i concetti di base della modellazione multidimensionale e MDX, degli elementi della sintassi MDX, nonché degli operatori, delle istruzioni e delle funzioni MDX.  
  
> [!NOTE]  
>  Per ulteriori informazioni, vedere la sezione risorse aggiuntive nella pagina [SQL Server 2005-Analysis Services](https://go.microsoft.com/fwlink/?LinkId=80853) del sito Web Microsoft TechNet. Per ulteriori informazioni sui problemi di prestazioni relativi a query e calcoli MDX, vedere la sezione relativa alla scrittura di espressioni MDX efficienti nella [Guida alle prestazioni SQL Server 2005 Analysis Services](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Concetti chiave di MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)|È possibile utilizzare espressioni MDX (Multidimensional Expressions) per eseguire query su dati multidimensionali o creare espressioni MDX da utilizzare all'interno di un cubo, ma è prima necessario comprendere i [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] concetti e la terminologia relativi alle dimensioni.|  
|[Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)|Nel linguaggio MDX (Multidimensional Expressions) è possibile eseguire query su oggetti multidimensionali, ad esempio un cubo, e restituire set di celle multidimensionali contenenti i dati del cubo. In questo argomento e negli argomenti correlati viene fornita una panoramica delle query MDX.|  
|[Nozioni fondamentali sullo scripting MDX &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)|In uno [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] script MDX (Multidimensional Expressions) è costituito da una o più espressioni o istruzioni MDX che popolano un cubo con calcoli.<br /><br /> Uno script MDX definisce il processo di calcolo per un cubo ed è considerato parte del cubo stesso. La modifica di uno script MDX associato a un cubo comporta pertanto la modifica immediata del processo di calcolo per il cubo.<br /><br /> Per creare script MDX, è possibile usare Progettazione cubi in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].|  
  
## <a name="see-also"></a>Vedere anche  
 [Elementi della sintassi MDX &#40;&#41;MDX](/sql/mdx/mdx-syntax-elements-mdx)   
 [Guida di riferimento al linguaggio MDX &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)  
  
  
