---
title: Mapping di cursore1 tipi di informazioni | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], mapping cursor attributes1 information types
- application upgrades [ODBC], mapping cursor attributes1 information types
- mapping cursor attributes1 information types [ODBC]
- backward compatibility [ODBC], mapping cursor attributes1 information types
- upgrading applications [ODBC], mapping cursor attributes1 information types
ms.assetid: 9f112449-ca86-45ac-a865-e6174d67f91b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e9549c442e301f3a6ed8d3da9c73d52177adf01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62628888"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>Mapping delle informazioni di tipo Cursor Attributes1
Quando un'applicazione ODBC 3. *x* applicazione chiama **SQLGetInfo** in un'API ODBC 2*x* driver con il tipo di informazioni SQL_XXXX_CURSOR_ATTRIBUTES1 (per dinamico di tipo forward-only, i driver, o i cursori statici), l'impostazione dei bit restituiti da Gestione Driver dipende dal quale ODBC 2. *x* driver restituisce per la corrispondente di ODBC 2. *x* tipi di informazioni. I bit sono impostati come illustrato nella tabella seguente.  
  
|Bit in<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|Tipo di cursore|ODBC 2. *x* informazioni<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|All|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|Dinamici, i driver, statico|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|Dinamici, i driver, statico|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|All|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|Dinamici, i driver, statico|SQL_POS_OPERATIONS|
