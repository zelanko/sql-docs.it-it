---
title: "Passaggio 2: Inizializzazione dell'applicazione | Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- initializing applications [ODBC]
- application process [ODBC], initializing applications
ms.assetid: 23a7a230-ae2c-4a5e-9760-d2e17f92c389
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 41030015645bda11242a703a163f26104e66dba0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114254"
---
# <a name="step-2-initialize-the-application"></a>Passaggio 2: Inizializzare l'applicazione
Il secondo passaggio consiste nell'inizializzare l'applicazione, come illustrato nella figura seguente. Esattamente ciò che viene eseguita qui varia in base all'applicazione.  
  
 ![Mostra l'inizializzazione di un'applicazione ODBC](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 A questo punto, accade spesso di usare **SQLGetInfo** per individuare le funzionalità del driver. Per altre informazioni, vedere [prendere in considerazione le funzionalità di Database da utilizzare](../../../odbc/reference/develop-app/considering-database-features-to-use.md).  
  
 Tutte le applicazioni devono allocare un handle di istruzione con **SQLAllocHandle**, e molte applicazioni di impostavano gli attributi di istruzione, ad esempio il tipo di cursore, con **SQLSetStmtAttr**. Per altre informazioni, vedere [allocare un Handle di istruzione](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) e [gli attributi di istruzione](../../../odbc/reference/develop-app/statement-attributes.md).
