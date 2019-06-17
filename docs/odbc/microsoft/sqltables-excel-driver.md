---
title: SQLTables (Driver Excel) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23ce67350b7fa7d0a88f3d51e618ce9bb9f9ebcf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287285"
---
# <a name="sqltables-excel-driver"></a>SQLTables (driver Excel)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver Excel. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argomento|Commenti|  
|--------------|--------------|  
|*szTableOwner*|L'argomento valido solo per *szTableOwner* è NULL perché nessuno dei driver supporta i nomi dei proprietari. Con *szTableOwner* impostato su NULL, vengono restituite tutte le tabelle. Nella colonna TABLE_OWNER viene restituito NULL.|  
|*szTableQualifier*|Quando Microsoft Excel 3.0 o 4.0 driver viene usato, se si chiama **SQLTables** con un valore per *szTableQualifier* che non è il nome di una tabella esistente, il driver creerà una tabella con lo stesso nome.<br /><br /> Nella colonna TABLE_QUALIFIER **SQLTables** restituirà il percorso in una directory.|  
|*SzTableType*|Per Microsoft Excel 3.0 o 4.0, "TABLE" è l'unico tipo di tabella supportato.<br /><br /> Per le versioni successive di file di Microsoft Excel, per i nomi dei fogli (tabelle con "$" all'estremità) viene restituita "Tabella di sistema" e "TABLE" viene restituito per le tabelle all'interno di fogli di lavoro.|
