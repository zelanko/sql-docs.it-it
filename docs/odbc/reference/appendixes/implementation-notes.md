---
title: Note sull'implementazione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 95b60ba35a867135cfc1f823e08b1a99f0262ca9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135737"
---
# <a name="implementation-notes"></a>Note di implementazione
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 Questa sezione descrive la modalità di implementazione della libreria di cursori ODBC. Descrive come la libreria di cursori mantiene la propria cache esegue istruzioni SQL e implementa le funzioni ODBC.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Cache della libreria di cursori](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [Elaborazione di istruzioni SQL](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [Funzioni ODBC e libreria di cursori](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
