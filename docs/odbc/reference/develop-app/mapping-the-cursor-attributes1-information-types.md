---
title: Mapping dei tipi di informazioni del cursore Attributes1 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d70cf0a93a6c6160faeb0afe991b2adfff11b8f1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301044"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>Mapping delle informazioni di tipo Cursor Attributes1
Quando ODBC 3. *x* l'applicazione chiama **SQLGetInfo** in un driver ODBC 2 *. x* con il tipo di informazioni SQL_XXXX_CURSOR_ATTRIBUTES1 (per i cursori dinamici, di sola trasmissione, keyset o statici), l'impostazione dei bit restituiti da Gestione driver dipende da ODBC 2. il driver *x* restituisce per il ODBC 2 corrispondente. tipi di informazioni *x* . I bit vengono impostati come illustrato nella tabella seguente.  
  
|Bit in<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|Tipo di cursore|ODBC 2. informazioni *x*<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|Tutti|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|Dynamic, Keyset-Driver, static|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|Dynamic, Keyset-Driver, static|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|Tutti|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|Dynamic, Keyset-Driver, static|SQL_POS_OPERATIONS|
