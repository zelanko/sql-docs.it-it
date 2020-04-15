---
title: Modifiche al tipo di dati Datetime Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- compatibility [ODBC], datetime data types
ms.assetid: c38c79f9-8bb0-4633-ac86-542366c09a95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4f186047dd31aa2c4b66ec1ce73c8cb9fae31c04
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304644"
---
# <a name="datetime-data-type-changes"></a>Modifiche ai tipi di dati datetime
In ODBC *3.x*gli identificatori per i tipi di dati SQL di data, ora e timestamp sono stati modificati da SQL_DATE, SQL_TIME e SQL_TIMESTAMP (con istanze di **#define** nel file di intestazione 9, 10 e 11) a SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP (con istanze di **#define** nel file di intestazione 91, 92 e 93), rispettivamente. Gli identificatori di tipo C corrispondenti sono stati modificati da SQL_C_DATE, SQL_C_TIME e SQL_C_TIMESTAMP rispettivamente a SQL_C_TYPE_DATE, SQL_C_TYPE_TIME e SQL_C_TYPE_TIMESTAMP.  
  
 Le dimensioni della colonna e le cifre decimali restituite per i tipi di dati datetime SQL in ODBC *3.x* sono uguali alla precisione e alla scala restituite in ODBC *2.x*. Questi valori sono diversi dai valori nei campi SQL_DESC_PRECISION e descrittore SQL_DESC_SCALE. Per ulteriori informazioni, vedere [Dimensione colonna, Cifre decimali, Lunghezza ottetto di trasferimento e Dimensioni di visualizzazione.](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)  
  
 Queste modifiche interessano **SQLDescribeCol**, **SQLDescribeParam**e **SQLColAttribute**; **SQLBindCol**, **SQLBindParameter**e **SQLGetData**; e **SQLColumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, **SQLStatistics**e **SQLSpecialColumns**.  
  
 Nella tabella seguente viene illustrato come ODBC *3.x* Gestione Driver esegue il mapping dei tipi di dati data, ora e timestamp C immessi negli argomenti *TargetType* di **SQLBindCol** e **SQLGetData** o nell'argomento *ValueType* di **SQLBindParameter**.  
  
|Tipo di dati<br /><br /> codice inserito|*2.x* app per<br /><br /> *Driver 2.x*|*2.x* app per<br /><br /> *Driver 3.x*|*3.x* app per<br /><br /> *Driver 2.x*|*3.x* app per<br /><br /> *Driver 3.x*|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|Nessuna mappatura|SQL_C_TYPE_DATE (91)|Nessuna mappatura[1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|Errore (da DM)|Errore (da DM)|SQL_C_DATE (9)|Nessuna mappatura[2]|  
|SQL_C_TIME (10)|Nessuna mappatura|SQL_C_TYPE_TIME (92)|Nessuna mappatura[1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|Errore (da DM)|Errore (da DM)|SQL_C_TIME (10)|Nessuna mappatura[2]|  
|SQL_C_TIMESTAMP (11)|Nessuna mappatura|SQL_C_TYPE_TIMESTAMP (93)|Nessuna mappatura[1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|Errore (da DM)|Errore (da DM)|SQL_C_TIMESTAMP (11)|Nessuna mappatura[2]|  
  
 [1] Di conseguenza, un'applicazione ODBC *3.x* che utilizza un driver ODBC *2.x* può utilizzare i codici data, ora o timestamp restituiti nei set di risultati restituiti dalle funzioni di catalogo.  
  
 [2] Di conseguenza, un'applicazione ODBC *3.x* che utilizza un driver ODBC *3.x* può utilizzare i codici data, ora o timestamp restituiti nei set di risultati restituiti dalle funzioni di catalogo.  
  
 Nella tabella seguente viene illustrato come Gestione Driver ODBC *3.x* esegue il mapping dei tipi di dati SQL di data, ora e timestamp immessi nell'argomento *ParameterType* di **SQLBindParameter** o nell'argomento *DataType* di **SQLGetTypeInfo**.  
  
|Tipo di dati<br /><br /> codice inserito|*2.x* app per<br /><br /> *Driver 2.x*|*2.x* app per<br /><br /> *Driver 3.x*|*3.x* app per<br /><br /> *Driver 2.x*|*3.x* app per<br /><br /> *Driver 3.x*|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|Nessuna mappatura|SQL_TYPE_DATE (91)|Nessuna mappatura[1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|Errore (da DM)|Errore (da DM)|SQL_DATE (9)|Nessuna mappatura[2]|  
|SQL_TIME (10)|Nessuna mappatura|SQL_TYPE_TIME (92)|Nessuna mappatura[1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|Errore (da DM)|Errore (da DM)|SQL_TIME (10)|Nessuna mappatura[2]|  
|SQL_TIMESTAMP (11)|Nessuna mappatura|SQL_TYPE_TIMESTAMP (93)|Nessuna mappatura[1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|Errore (da DM)|Errore (da DM)|SQL_TIMESTAMP (11)|Nessuna mappatura[2]|  
  
 [1] Di conseguenza, un'applicazione ODBC *3.x* che utilizza un driver ODBC *2.x* può utilizzare i codici data, ora o timestamp restituiti nei set di risultati restituiti dalle funzioni di catalogo.  
  
 [2] Di conseguenza, un'applicazione ODBC *3.x* che utilizza un driver ODBC *3.x* può utilizzare i codici data, ora o timestamp restituiti nei set di risultati restituiti dalle funzioni di catalogo.
