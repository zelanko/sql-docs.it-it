---
title: Controllo del supporto e della variabilità delle funzionalità Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47f16160c05d1c410e3889f0bb857befe88df5b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299171"
---
# <a name="checking-feature-support-and-variability"></a>Controllo del supporto e della variabilità delle funzionalità
Per verificare il supporto e la variabilità delle funzionalità, le applicazioni in genere chiamano **SQLGetInfo**, **SQLGetFunctions**e **SQLGetTypeInfo**. Un buon punto di partenza è l'API del driver e i livelli di conformità grammaticale SQL. Questi descrivono ampi livelli di supporto delle funzionalità. L'applicazione può quindi chiamare **SQLGetInfo** con altre opzioni per determinare il supporto o la variabilità delle funzionalità necessarie, **SQLGetFunctions** per determinare se le funzioni necessarie oltre il livello di conformità restituito sono supportate e **SQLGetTypeInfo** per determinare i tipi di dati SQL supportati.  
  
 Un'applicazione può determinare se un'istruzione o un attributo di connessione è supportato chiamando **SQLSetStmtAttr** o **SQLSetConnectAttr** con tale attributo. Se la funzione restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, l'attributo è supportato; se restituisce SQL_ERROR e SQLSTATE HYC00 (funzionalità facoltativa non implementata), l'attributo non è supportato.  
  
 Le applicazioni possono inoltre determinare una quantità limitata di informazioni prima di connettersi al driver chiamando **SQLDrivers**.
