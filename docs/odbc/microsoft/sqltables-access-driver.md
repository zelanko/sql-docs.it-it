---
title: SQLTables (Driver Access) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e23e6993f66dd706a800ae2b34a9fdc0d219898d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132464"
---
# <a name="sqltables-access-driver"></a>SQLTables (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni di accesso specifici del Driver. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argomento|Commenti|  
|--------------|--------------|  
|*szTableOwner*|L'argomento valido solo per *szTableOwner* è NULL perché nessuno dei driver supporta i nomi dei proprietari. Con *szTableOwner* impostato su NULL, vengono restituite tutte le tabelle. Nella colonna TABLE_OWNER viene restituito NULL.|  
|*szTableQualifier*|Nella colonna TABLE_QUALIFIER **SQLTables** restituirà il percorso in un file di database.|  
|*SzTableType*|Quando viene usato il driver Microsoft Access, "Tabella di sistema" è supportata per *szTableType* per tabelle di sistema "SINONIMI" sono supportato per le tabelle collegate e "Visualizzazione" è supportata per la restituzione di riga le query.|  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLTables](../../odbc/reference/syntax/sqltables-function.md)
