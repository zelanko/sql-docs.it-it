---
title: Query su dati multidimensionali con MDX | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [Analysis Services], querying
ms.assetid: e0a5dd60-35a3-4a4f-b36f-52ecea814886
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b5bce169a9a18ca10dd8126606ea1f8302969b5b
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "59241949"
---
# <a name="querying-multidimensional-data-with-mdx"></a>Query su dati multidimensionali con MDX
  MDX (Multidimensional Expressions) è il linguaggio di query che consente di usare e recuperare dati multidimensionali in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Il linguaggio MDX è basato sulla specifica XML for Analysis (XMLA), con estensioni specifiche per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. MDX usa espressioni costituite da identificatori, valori, istruzioni, funzioni e operatori che possono essere valutate da [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] per recuperare un oggetto, ad esempio un set o un membro, oppure un valore scalare, ad esempio una stringa o un numero.  
  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] le query e le espressioni MDX vengono usate per le operazioni seguenti:  
  
-   Restituire dati a un'applicazione client da un cubo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .  
  
-   Modellare i risultati delle query.  
  
-   Eseguire attività di progettazione per i cubi, tra cui la definizione di membri calcolati, set denominati, assegnazioni con ambito e indicatori di prestazioni chiave (KPI).  
  
-   Eseguire attività di amministrazione, inclusa la sicurezza di dimensioni e celle.  
  
 MDX è in apparenza simile sotto numerosi aspetti alla sintassi SQL in genere utilizzata con i database relazionali. MDX non è tuttavia un'estensione del linguaggio SQL, rispetto al quale presenta molte differenze. Per creare espressioni MDX per la progettazione o la sicurezza dei cubi oppure per creare query MDX in grado di restituire e modellare dati multidimensionali, è necessario conoscere i concetti di base della modellazione multidimensionale e MDX, degli elementi della sintassi MDX, nonché degli operatori, delle istruzioni e delle funzioni MDX.  
  
> [!NOTE]  
>  Per altre informazioni, vedere la sezione risorse aggiuntive sul [SQL Server 2005 - Analysis Services](https://go.microsoft.com/fwlink/?LinkId=80853) pagina sul sito Web Microsoft TechNet. Per altre informazioni sui problemi di prestazioni correlati a query e calcoli MDX, vedere la sezione "Scrittura efficiente di espressioni MDX" nel [SQL Server 2005 Analysis Services Performance Guide](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide).  
  
## <a name="in-this-section"></a>In questa sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Concetti chiave di MDX &#40;Analysis Services&#41;](../key-concepts-in-mdx-analysis-services.md)|È possibile usare espressioni MDX (Multidimensional Expression) per eseguire query su dati multidimensionali o creare espressioni MDX da usare all'interno di un cubo, ma è prima necessario comprendere i concetti e la terminologia relativi alle dimensioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .|  
|[Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)|Nel linguaggio MDX (Multidimensional Expressions) è possibile eseguire query su oggetti multidimensionali, ad esempio un cubo, e restituire set di celle multidimensionali contenenti i dati del cubo. In questo argomento e negli argomenti correlati viene fornita una panoramica delle query MDX.|  
|[Nozioni fondamentali sullo scripting MDX &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)|In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], uno script MDX (Multidimensional Expressions) è costituito da una o più espressioni o istruzioni MDX che popolano un cubo tramite calcoli.<br /><br /> Uno script MDX definisce il processo di calcolo per un cubo ed è considerato parte del cubo stesso. La modifica di uno script MDX associato a un cubo comporta pertanto la modifica immediata del processo di calcolo per il cubo.<br /><br /> Per creare script MDX, è possibile usare Progettazione cubi in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].|  
  
## <a name="see-also"></a>Vedere anche  
 [Elementi della sintassi MDX &#40;MDX&#41;](/sql/mdx/mdx-syntax-elements-mdx)   
 [Guida di riferimento al linguaggio MDX &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)  
  
  
