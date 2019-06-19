---
title: SQLGetInfo (Driver File di testo) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 256e964e556421db62dc8f52fdc6bc759c3a200a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63018360"
---
# <a name="sqlgetinfo-text-file-driver"></a>SQLGetInfo (driver file di testo)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver File di testo. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLGetInfo** supporta il tipo di informazioni SQL_FILE_USAGE. Il valore restituito è un numero intero a 16 bit che indica il modo in cui il driver considera direttamente i file in un'origine dati:  
  
-   SQL_FILE_NOT_SUPPORTED - il driver non è un driver a un solo livello.  
  
-   SQL_FILE_TABLE - un driver a un solo livello di gestione dei file in un'origine dati come tabelle.  
  
-   SQL_FILE_QUALIFIER - un driver a un solo livello considera i file in un'origine dati come un qualificatore.  
  
 Il driver ODBC restituisce SQL_FILE_TABLE per Textdriver, poiché ogni file è una tabella.  
  
## <a name="sqldbmsver"></a>SQL_DBMS_VER  
  
|ISAM|Version|Formato dei numeri di versione|  
|----------|-------------|-------------------------------|  
|Testo|1,0|01.00.0000|  
  
## <a name="sqlcatalogusage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sqltimedatefunctions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &AMP;#124; SQL_FN_TD_CURTIME &AMP;#124; SQL_FN_TD_DAYOFMONTH &AMP;#124; SQL_FN_TD_DAYOFWEEK &AMP;#124; SQL_FN_TD_DAYOFYEAR &AMP;#124; SQL_FN_TD_HOUR &AMP;#124; SQL_FN_TD_MINUTE &AMP;#124; SQL_FN_TD_MONTH &AMP;#124; SQL_FN_TD_NOW &AMP;#124; SQL_FN_TD_SECOND &AMP;#124; SQL_FN_TD_WEEK &AMP;#124; SQL_FN_TD_YEAR
