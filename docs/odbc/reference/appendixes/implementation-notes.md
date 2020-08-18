---
description: Note sull'implementazione
title: Note sull'implementazione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7ec14b9c-69b8-4c6e-838a-88d1ebdc8725
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7117e0d8af856a16a47414f5a8c3ec11c475cb92
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483264"
---
# <a name="implementation-notes"></a>Note sull'implementazione
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità di cursore del driver.  
  
 In questa sezione viene descritta la modalità di implementazione della libreria di cursori ODBC. Viene descritto il modo in cui la libreria di cursori mantiene la propria cache, esegue istruzioni SQL e implementa le funzioni ODBC.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Cache della libreria di cursori](../../../odbc/reference/appendixes/cursor-library-cache.md)  
  
-   [Elaborazione di istruzioni SQL](../../../odbc/reference/appendixes/processing-sql-statements.md)  
  
-   [Funzioni ODBC e libreria di cursori](../../../odbc/reference/appendixes/odbc-functions-and-the-cursor-library.md)
