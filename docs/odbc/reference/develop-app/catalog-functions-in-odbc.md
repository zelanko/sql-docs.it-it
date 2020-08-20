---
description: Funzioni di catalogo in ODBC
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b7a34a29e55f6705ccc98e5644096ac6ea7bfd67
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465973"
---
# <a name="catalog-functions-in-odbc"></a>Funzioni di catalogo in ODBC
ODBC contiene le funzioni di catalogo seguenti:  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|**SQLTables**|Restituisce un elenco di cataloghi, schemi, tabelle o tipi di tabella nell'origine dati.|  
|**SQLColumns**|Restituisce un elenco di colonne in una o più tabelle.|  
|**SQLStatistics**|Restituisce un elenco di statistiche relative a una singola tabella. Restituisce anche un elenco di indici associati alla tabella.|  
|**SQLSpecialColumns**|Restituisce un elenco di colonne che identifica in modo univoco una riga in una singola tabella. Restituisce inoltre un elenco di colonne della tabella che vengono aggiornate automaticamente.|  
|**SQLPrimaryKeys**|Restituisce un elenco di colonne che compongono la chiave primaria di una singola tabella.|  
|**SQLForeignKeys**|Restituisce un elenco di chiavi esterne in una singola tabella o un elenco di chiavi esterne in altre tabelle che fanno riferimento a una singola tabella.|  
|**SQLTablePrivileges**|Restituisce un elenco di privilegi associati a una o più tabelle.|  
|**SQLColumnPrivileges**|Restituisce un elenco di privilegi associati a una o più colonne in una singola tabella.|  
|**SQLProcedures**|Restituisce un elenco di procedure nell'origine dati.|  
|**SQLProcedureColumns**|Restituisce un elenco di parametri di input e di output, il valore restituito e le colonne nel set di risultati di una singola procedura.|  
|**SQLGetTypeInfo**|Restituisce un elenco dei tipi di dati SQL supportati dall'origine dati. Questi tipi di dati vengono in genere utilizzati nelle istruzioni **Create Table** e **ALTER TABLE** .|  
  
 Poiché **SQLTables**, SQLColumns, **SQLStatistics**e **SQLSpecialColumns** sono conformi all'interfaccia della **riga**di comando di gruppo Open e **SQLGetTypeInfo** sono conformi all'interfaccia della riga di comando ISO 92, vengono implementate dalla maggior parte dei driver. Le funzioni di catalogo rimanenti si trovano nel livello di conformità ODBC.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Dati restituiti dalle funzioni catalogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [Argomenti nelle funzioni di catalogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [Viste dello schema](../../../odbc/reference/develop-app/schema-views.md)
