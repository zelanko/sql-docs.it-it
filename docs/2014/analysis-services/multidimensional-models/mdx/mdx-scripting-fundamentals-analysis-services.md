---
title: Nozioni fondamentali sullo scripting MDX (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], scripts
- calculations [Analysis Services], scripts
- MDX [Analysis Services], scripts
- scripts [MDX]
- cubes [Analysis Services], calculations
- Multidimensional Expressions [Analysis Services], scripts
ms.assetid: fdecb3ce-7c87-4bab-8000-532ba7a29f96
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2f7638339d8fc366ee384d453f6df683f3bd41f8
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546253"
---
# <a name="mdx-scripting-fundamentals-analysis-services"></a>Nozioni fondamentali sullo scripting MDX (Analysis Services)
  In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], uno script MDX (Multidimensional Expressions) è costituito da una o più espressioni o istruzioni MDX che popolano un cubo tramite calcoli.  
  
 Uno script MDX definisce il processo di calcolo per un cubo ed è considerato parte del cubo stesso. La modifica di uno script MDX associato a un cubo comporta pertanto la modifica immediata del processo di calcolo per il cubo.  
  
 Per creare script MDX, è possibile usare Progettazione cubi in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. Per altre informazioni, vedere [Definire le assegnazioni e altri comandi script](../define-assignments-and-other-script-commands.md) e [Introduction to MDX Scripting in Microsoft SQL Server 2005](https://go.microsoft.com/fwlink/?LinkId=81892)(Introduzione alla creazione di script MDX in Microsoft SQL Server 2005).  
  
 Per problemi di prestazioni relativi a query e calcoli MDX, vedere la sezione relativa all'ottimizzazione MDX nella [guida alle prestazioni di SQL Server Analysis Services](https://go.microsoft.com/fwlink/p/?LinkId=399050).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Script MDX di base &#40;MDX&#41;](the-basic-mdx-script-mdx.md)|Include informazioni dettagliate sullo script MDX di base, compreso lo script MDX predefinito inserito in ogni cubo, e sui principi generali di funzionamento degli script MDX nei cubi di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Gestione di ambito e contesto &#40;MDX&#41;](managing-scope-and-context-mdx.md)|Descrive come usare l'istruzione [CALCULATE](/sql/mdx/mdx-scripting-calculate) , l'istruzione [SCOPE](/sql/mdx/mdx-scripting-scope) e la funzione [This](/sql/mdx/this-mdx) per gestire il contesto e l'ambito in uno script MDX.|  
|[Utilizzo di variabili e parametri &#40;MDX&#41;](using-variables-and-parameters-mdx.md)|Descrive come usare le variabili e i parametri in uno script MDX.|  
|[Gestione degli errori &#40;MDX&#41;](error-handling-mdx.md)|Illustra la gestione degli errori in uno script MDX.|  
|[Istruzioni e funzioni MDX supportate &#40;MDX&#41;](supported-mdx-mdx.md)|Include un elenco di istruzioni, funzioni e operatori MDX supportati negli script MDX.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento al linguaggio MDX &#40;MDX&#41;](/sql/mdx/mdx-language-reference-mdx)  
  
  
