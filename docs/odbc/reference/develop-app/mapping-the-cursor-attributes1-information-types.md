---
description: Mapping delle informazioni di tipo Cursor Attributes1
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
ms.openlocfilehash: fcd4c1eaa6ddd2e6db4f2634cc22d3148e7977cf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461403"
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
