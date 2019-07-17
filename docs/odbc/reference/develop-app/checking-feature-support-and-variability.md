---
title: Controlla il supporto delle funzionalità e la variabilità | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062658"
---
# <a name="checking-feature-support-and-variability"></a>Controllo del supporto e della variabilità delle funzionalità
Per verificare il supporto delle funzionalità e la variabilità, le applicazioni in genere chiamano **SQLGetInfo**, **SQLGetFunctions**, e **SQLGetTypeInfo**. Un buon punto di partenza è SQL e API grammatica livelli di conformità del driver. In cui sono descritti i livelli di ampi di supporto della funzionalità. L'applicazione può quindi chiamare **SQLGetInfo** con le altre opzioni per determinare il supporto tecnico o variabilità delle funzionalità necessarie, **SQLGetFunctions** per determinare se le funzioni esigenze oltre restituito sono supportate a livello di conformità, e **SQLGetTypeInfo** per determinare quali tipi di dati SQL sono supportati.  
  
 Un'applicazione può determinare se un attributo di istruzione o la connessione è supportato tramite la chiamata **SQLSetStmtAttr** oppure **SQLSetConnectAttr** con quell'attributo. Se la funzione restituisce SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, l'attributo è supportato; Se viene restituito SQL_ERROR e SQLSTATE HYC00 (funzionalità facoltativa non implementata), l'attributo non è supportato.  
  
 Le applicazioni possono inoltre determinare una quantità limitata di informazioni prima di connettersi al driver chiamando **SQLDrivers**.
