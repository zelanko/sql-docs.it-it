---
title: SQLTables (driver file di testo) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299331"
---
# <a name="sqltables-text-file-driver"></a>SQLTables (driver file di testo)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver del file di testo. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argomento|Commenti|  
|--------------|--------------|  
|*szTableOwner*|L'unico argomento valido per *szTableOwner* è null perché nessuno dei driver supporta i nomi di proprietario. Con *szTableOwner* impostato su null, vengono restituite tutte le tabelle. Nella colonna TABLE_OWNER viene restituito NULL.|  
|*szTableQualifier*|Nella colonna TABLE_QUALIFIER **SQLTables** restituirà il percorso di una directory.|  
|*SzTableType*|"TABLE" è l'unico tipo di tabella supportato.<br /><br /> Quando si utilizza il driver di testo, l'elenco dei file restituiti da **SQLTables** è determinato dalle estensioni di file nella casella di **Riepilogo estensioni** della finestra di dialogo di **configurazione del testo ODBC** .|
