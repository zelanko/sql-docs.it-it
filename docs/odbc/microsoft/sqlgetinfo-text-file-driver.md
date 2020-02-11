---
title: SQLGetInfo (driver file di testo) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetInfo
ms.assetid: 6b7a630e-47f8-4ee1-b2a7-476bc1d0b0d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 892fdabc319b1d495120cdce20d77f05cd232418
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898823"
---
# <a name="sqlgetinfo-text-file-driver"></a>SQLGetInfo (driver file di testo)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver del file di testo. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLGetInfo** supporta il tipo di informazioni SQL_FILE_USAGE. Il valore restituito è un intero a 16 bit che indica il modo in cui il driver tratta direttamente i file in un'origine dati:  
  
-   SQL_FILE_NOT_SUPPORTED: il driver non è un driver a livello singolo.  
  
-   SQL_FILE_TABLE: un driver a livello singolo considera i file in un'origine dati come tabelle.  
  
-   SQL_FILE_QUALIFIER: un driver a livello singolo considera i file in un'origine dati come qualificatore.  
  
 Il driver ODBC restituisce SQL_FILE_TABLE per Textdriver, in quanto ogni file è una tabella.  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|ISAM|Versione|Formato dei numeri di versione|  
|----------|-------------|-------------------------------|  
|Text|1.0|01.00.0000|  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &#124; SQL_FN_TD_CURTIME &#124; SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_NOW &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
