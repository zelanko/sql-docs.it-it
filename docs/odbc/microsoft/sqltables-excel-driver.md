---
title: SQLTables (driver di Excel) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLTables
- SQLTables function [ODBC], Excel Driver
ms.assetid: 9410b686-4b5b-4b51-b5ef-f9d2e7a48faa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c436a1f52a862cda753d8c043515f5584607d98c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299301"
---
# <a name="sqltables-excel-driver"></a>SQLTables (driver Excel)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di Excel.This topic provides Excel Driver-specific information. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argomento|Commenti|  
|--------------|--------------|  
|*szTableOwner*|L'unico argomento valido per *szTableOwner* è NULL perché nessuno dei driver supporta i nomi dei proprietari. Con *szTableOwner* impostato su NULL, vengono restituite tutte le tabelle. NULL viene restituito nella colonna TABLE_OWNER.|  
|*SzTableQualifier (qualificatore di szTable)*|Quando viene utilizzato il driver di Microsoft Excel 3.0 o 4.0, se si chiama **SQLTables** con un valore per *szTableQualifier* che non è il nome di una tabella esistente, il driver creerà una tabella con tale nome.<br /><br /> Nella colonna TABLE_QUALIFIER, **SQLTables** restituirà il percorso di una directory.|  
|*SzTableType (Tipo di SzTableType)*|Per Microsoft Excel 3.0 o 4.0, "TABLE" è l'unico tipo di tabella supportato.<br /><br /> Per le versioni successive dei file di Microsoft Excel, viene restituito "SYSTEM TABLE" per i nomi dei fogli (tabelle con un carattere "" alla fine) e "TABLE" viene restituito per le tabelle all'interno dei fogli di lavoro.|
