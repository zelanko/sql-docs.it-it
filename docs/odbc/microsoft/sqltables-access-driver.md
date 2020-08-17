---
description: SQLTables (driver Access)
title: SQLTables (driver di accesso) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Access Driver
- Access driver [ODBC], SQLTables
ms.assetid: 94423cf9-341a-4db6-bb10-8f5448df7fc3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69dce4116064cdb7509f628fcc493e57c414666e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339917"
---
# <a name="sqltables-access-driver"></a>SQLTables (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di accesso. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argomento|Commenti|  
|--------------|--------------|  
|*szTableOwner*|L'unico argomento valido per *szTableOwner* è null perché nessuno dei driver supporta i nomi di proprietario. Con *szTableOwner* impostato su null, vengono restituite tutte le tabelle. Nella colonna TABLE_OWNER viene restituito NULL.|  
|*szTableQualifier*|Nella colonna TABLE_QUALIFIER **SQLTables** restituirà il percorso di un file di database.|  
|*SzTableType*|Quando si utilizza il driver Microsoft Access, "tabella di sistema" è supportata per *szTableType* per le tabelle di sistema, "sinonimo" è supportato per le tabelle collegate e "View" è supportato per le query che restituiscono righe.|  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLTables](../../odbc/reference/syntax/sqltables-function.md)
