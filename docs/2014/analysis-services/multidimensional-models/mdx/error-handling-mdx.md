---
title: Gestione degli errori (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [MDX], exceptions
- exceptions [MDX]
ms.assetid: bc6ff0af-9fe6-44d6-bc3c-801d71ea41a9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 611e7636f9a5cd6393da4a8412b6c02bcc9ddaf8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074682"
---
# <a name="error-handling-mdx"></a>Gestione degli errori (MDX)
  Ogni cubo può controllare la modalità con cui verranno gestiti gli errori di uno script MDX (Multidimensional Expressions). Per la gestione degli errori viene utilizzato l'enumeratore `ScriptErrorHandlingMode`. I possibili valori dell'enumeratore sono i seguenti:  
  
 `IgnoreNone`  
 Determina la generazione di un errore da parte [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] del server quando viene rilevato un errore nello script MDX.  
  
 `IgnoreAll`  
 Induce il server a ignorare tutti i comandi dello script MDX che contengono un errore, compresi gli errori di sintassi e gli errori di risoluzione dei nomi.  
  
## <a name="see-also"></a>Vedi anche  
 <xref:Microsoft.AnalysisServices.Cube.ScriptErrorHandlingMode%2A>  
  
  
