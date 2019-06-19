---
title: (MDX MultiDimensional Expression) di gestione degli errori | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5d6679e264ee15fd6a1ba038d3c6492aec07c81c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62802716"
---
# <a name="error-handling-mdx"></a>Gestione degli errori (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Ogni cubo può controllare la modalità con cui verranno gestiti gli errori di uno script MDX (Multidimensional Expressions). La gestione degli errori viene eseguita tramite l'enumeratore **ScriptErrorHandlingMode** . I possibili valori dell'enumeratore sono i seguenti:  
  
 **IgnoreNone**  
 Induce il server a generare un errore quando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] rileva un errore nello script MDX.  
  
 **IgnoreAll**  
 Induce il server a ignorare tutti i comandi dello script MDX che contengono un errore, compresi gli errori di sintassi e gli errori di risoluzione dei nomi.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
