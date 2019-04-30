---
title: Funzioni di catalogo in ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], listed
- functions [ODBC], catalog functions
ms.assetid: 4f28f557-7eca-4905-aa6d-45a6cf501a66
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84c870d45cc487fc9ec5497e43b764bd4187d2f6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63217622"
---
# <a name="catalog-functions-in-odbc"></a>Funzioni di catalogo in ODBC
ODBC contiene le funzioni del catalogo seguenti:  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|**SQLTables**|Restituisce un elenco di cataloghi, schemi, tabelle o i tipi di tabella nell'origine dati.|  
|**SQLColumns**|Restituisce un elenco di colonne in una o più tabelle.|  
|**SQLStatistics**|Restituisce un elenco delle statistiche su una singola tabella. Restituisce anche un elenco di indici associate alla tabella.|  
|**SQLSpecialColumns**|Restituisce un elenco di colonne che identifica in modo univoco una riga in una singola tabella. Restituisce anche un elenco di colonne della tabella che vengono aggiornate automaticamente.|  
|**SQLPrimaryKeys**|Restituisce un elenco di colonne che compongono la chiave primaria di una singola tabella.|  
|**SQLForeignKeys**|Restituisce un elenco di chiavi esterne in una singola tabella o un elenco di chiavi esterne in altre tabelle che fanno riferimento a una singola tabella.|  
|**SQLTablePrivileges**|Restituisce un elenco di privilegi associati a una o più tabelle.|  
|**SQLColumnPrivileges**|Restituisce un elenco di privilegi associati a una o più colonne in una singola tabella.|  
|**SQLProcedures**|Restituisce un elenco di procedure nell'origine dati.|  
|**SQLProcedureColumns**|Restituisce un elenco di parametri di input e output, il valore restituito e le colonne in set di risultati di una sola stored procedure.|  
|**SQLGetTypeInfo**|Restituisce un elenco di tipi di dati SQL supportati dall'origine dati. Questi tipi di dati vengono in genere utilizzati nelle **CREATE TABLE** e **ALTER TABLE** istruzioni.|  
  
 In quanto **SQLTables**, **SQLColumns**, **SQLStatistics**, e **SQLSpecialColumns** conformi alla CLI di gruppo aprire e **SQLGetTypeInfo** conforme a ISO 92 CLI, vengono implementate dalla maggior parte dei driver. Le funzioni di catalogo rimanenti sono al livello di conformità di ODBC.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Dati restituiti dalle funzioni catalogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [Argomenti nelle funzioni di catalogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [Viste degli schemi](../../../odbc/reference/develop-app/schema-views.md)
