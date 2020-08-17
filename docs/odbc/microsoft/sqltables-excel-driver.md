---
description: SQLTables (driver Excel)
title: SQLTables (driver Excel) | Microsoft Docs
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
ms.openlocfilehash: acedd48fb48e8f8db844feb1911f044c472006a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339647"
---
# <a name="sqltables-excel-driver"></a>SQLTables (driver Excel)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di Excel. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argomento|Commenti|  
|--------------|--------------|  
|*szTableOwner*|L'unico argomento valido per *szTableOwner* è null perché nessuno dei driver supporta i nomi di proprietario. Con *szTableOwner* impostato su null, vengono restituite tutte le tabelle. Nella colonna TABLE_OWNER viene restituito NULL.|  
|*szTableQualifier*|Quando si utilizza il driver Microsoft Excel 3,0 o 4,0, se si chiama **SQLTables** con un valore per *szTableQualifier* che non corrisponde al nome di una tabella esistente, il driver creerà una tabella con tale nome.<br /><br /> Nella colonna TABLE_QUALIFIER **SQLTables** restituirà il percorso di una directory.|  
|*SzTableType*|Per Microsoft Excel 3,0 o 4,0, "TABLE" è l'unico tipo di tabella supportato.<br /><br /> Per le versioni più recenti dei file di Microsoft Excel, viene restituito "tabella di sistema" per i nomi dei fogli (tabelle con una "$" alla fine) e "TABLE" viene restituito per le tabelle nei fogli di lavoro.|
