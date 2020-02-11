---
title: Controllo del supporto e della variabilità delle funzionalità | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: ff45f220-9b8b-4c44-82f8-a8e9913fffea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 21495e538a554a477336d1a92926c11fe762c5af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68062658"
---
# <a name="checking-feature-support-and-variability"></a>Controllo del supporto e della variabilità delle funzionalità
Per controllare il supporto e la variabilità delle funzionalità, le applicazioni in genere chiamano **SQLGetInfo**, **SQLGetFunctions**e **SQLGetTypeInfo**. Un punto di partenza valido è l'API del driver e i livelli di conformità della grammatica SQL. Che descrivono livelli ampi di supporto della funzionalità. L'applicazione può quindi chiamare **SQLGetInfo** con altre opzioni per determinare il supporto o la variabilità delle funzionalità necessarie, **SQLGetFunctions** per determinare se le funzioni necessarie oltre il livello di conformità restituito sono supportate e **SQLGetTypeInfo** per determinare quali tipi di dati SQL sono supportati.  
  
 Un'applicazione può determinare se un'istruzione o un attributo di connessione è supportato chiamando **SQLSetStmtAttr** o **SQLSetConnectAttr** con tale attributo. Se la funzione restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, l'attributo è supportato. Se restituisce SQL_ERROR e SQLSTATE HYC00 (funzionalità facoltativa non implementata), l'attributo non è supportato.  
  
 Le applicazioni possono inoltre determinare una quantità limitata di informazioni prima di connettersi al **driver chiamando SQLDrivers.**
