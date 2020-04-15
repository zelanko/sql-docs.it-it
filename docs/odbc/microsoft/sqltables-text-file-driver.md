---
title: SQLTables (Driver dei file di testo) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLTables
- SQLTables function [ODBC], Text File Driver
ms.assetid: f47fd1a4-5bd8-4b2e-8ae3-e595e49f4f95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 938ceba5da25d176628d5c1d9875383d977e3aec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299331"
---
# <a name="sqltables-text-file-driver"></a>SQLTables (driver file di testo)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di file di testo. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argomento|Commenti|  
|--------------|--------------|  
|*szTableOwner*|L'unico argomento valido per *szTableOwner* è NULL perché nessuno dei driver supporta i nomi dei proprietari. Con *szTableOwner* impostato su NULL, vengono restituite tutte le tabelle. NULL viene restituito nella colonna TABLE_OWNER.|  
|*SzTableQualifier (qualificatore di szTable)*|Nella colonna TABLE_QUALIFIER, **SQLTables** restituirà il percorso di una directory.|  
|*SzTableType (Tipo di SzTableType)*|"TABLE" è l'unico tipo di tabella supportato.<br /><br /> Quando viene utilizzato il driver di testo, l'elenco dei file restituito da **SQLTables** è determinato dalle estensioni di file nella casella **elenco estensioni** nella finestra di dialogo **Impostazione di testo ODBC** .|
