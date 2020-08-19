---
description: "Passaggio 2: Inizializzare l'applicazione"
title: "Passaggio 2: inizializzare l'applicazione | Microsoft Docs"
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26d20a5b10ee7b414b9285a388359b3a93029f16
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482884"
---
# <a name="step-2-initialize-the-application"></a>Passaggio 2: Inizializzare l'applicazione
Il secondo passaggio consiste nell'inizializzare l'applicazione, come illustrato nella figura seguente. Esattamente ciò che viene fatto qui varia a seconda dell'applicazione.  
  
 ![Inizializzazione di un'applicazione ODBC](../../../odbc/reference/develop-app/media/pr12.gif "pr12")  
  
 A questo punto, è comune usare **SQLGetInfo** per individuare le funzionalità del driver. Per ulteriori informazioni, vedere [considerazioni sulle funzionalità del database da utilizzare](../../../odbc/reference/develop-app/considering-database-features-to-use.md).  
  
 Tutte le applicazioni devono allocare un handle di istruzione con **SQLAllocHandle**e molte applicazioni impostano attributi di istruzione, ad esempio il tipo di cursore con **SQLSetStmtAttr**. Per ulteriori informazioni, vedere [allocazione di un handle di istruzione](../../../odbc/reference/develop-app/allocating-a-statement-handle-odbc.md) e di [attributi di istruzione](../../../odbc/reference/develop-app/statement-attributes.md).
