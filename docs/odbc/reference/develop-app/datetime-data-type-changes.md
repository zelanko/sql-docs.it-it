---
title: Modifica del tipo dati Data/ora | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5a87a1cbfbdff5eb428e73d74cdd1199955d673
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267701"
---
# <a name="datetime-data-type-changes"></a>Modifiche ai tipi di dati datetime
In ODBC 3. *x*, gli identificatori per data, ora e tipi di dati timestamp SQL sono stati modificati da SQL_DATE, SQL_TIME e SQL_TIMESTAMP (con istanze di **#define** nel file di intestazione di 9, 10 e 11) a SQL_TYPE_DATE, SQL_TYPE_TIME e SQL_TYPE_TIMESTAMP (con istanze di **#define** nel file di intestazione di 91, 92 e 93), rispettivamente. I corrispondenti identificatori di tipo C sono stati modificati da SQL_C_DATE SQL_C_TIME e SQL_C_TIMESTAMP SQL_C_TYPE_DATE, SQL_C_TYPE_TIME e SQL_C_TYPE_TIMESTAMP, rispettivamente.  
  
 Le dimensioni e cifre decimali restituiti per i tipi di dati datetime SQL in ODBC 3. *x* sono quello utilizzato per la precisione e scala restituite dal in ODBC 2. *x*. Questi valori sono diversi dai valori nei campi del descrittore SQL_DESC_PRECISION e SQL_DESC_SCALE. (Per altre informazioni, vedere [le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensioni di visualizzazione](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).)  
  
 Queste modifiche interessano **SQLDescribeCol**, **SQLDescribeParam**, e **SQLColAttribute**; **SQLBindCol**, **SQLBindParameter**, e **SQLGetData**; e **SQLColumns**, **SQLGetTypeInfo** , **SQLProcedureColumns**, **SQLStatistics**, e **SQLSpecialColumns**.  
  
 La tabella seguente illustra come ODBC 3 *. x* esegue il mapping dei data, ora e timestamp C tipi di dati immessi in Gestione Driver il *TargetType* argomenti di **SQLBindCol**e **SQLGetData** o il *ValueType* argomento del **SQLBindParameter**.  
  
|Tipo di dati<br /><br /> codice inserito|2.*x* dell'app<br /><br /> 2.*x* driver|2.*x* dell'app<br /><br /> 3.*x* driver|3.*x* dell'app<br /><br /> 2.*x* driver|3.*x* dell'app<br /><br /> 3.*x* driver|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|Nessun mapping|SQL_C_TYPE_DATE (91)|Nessun mapping di [1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|Errore (DM)|Errore (DM)|SQL_C_DATE (9)|Nessun mapping [2]|  
|SQL_C_TIME (10)|Nessun mapping|SQL_C_TYPE_TIME (92)|Nessun mapping di [1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|Errore (DM)|Errore (DM)|SQL_C_TIME (10)|Nessun mapping [2]|  
|SQL_C_TIMESTAMP (11)|Nessun mapping|SQL_C_TYPE_TIMESTAMP (93)|Nessun mapping di [1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|Errore (DM)|Errore (DM)|SQL_C_TIMESTAMP (11)|Nessun mapping [2]|  
  
 [1] in seguito a questa operazione, un'applicazione ODBC 3. *x* funziona con un'API ODBC 2. *x* driver può utilizzare i codici di data, ora o timestamp restituiti nei set di risultati restituiti dalle funzioni di catalogo.  
  
 [2] in seguito a questa operazione, un'applicazione ODBC 3. *x* funziona con un'applicazione ODBC 3. *x* driver può utilizzare i codici di data, ora o timestamp restituiti nei set di risultati restituiti dalle funzioni di catalogo.  
  
 La tabella seguente illustra come ODBC 3 *. x* esegue il mapping dei tipi di dati SQL date, time e timestamp immessi in Gestione Driver il *ParameterType* argomento di **SQLBindParameter**  o nel *DataType* dell'argomento **SQLGetTypeInfo**.  
  
|Tipo di dati<br /><br /> codice inserito|2.*x* dell'app<br /><br /> 2.*x* driver|2.*x* dell'app<br /><br /> 3.*x* driver|3.*x* dell'app<br /><br /> 2.*x* driver|3.*x* dell'app<br /><br /> 3.*x* driver|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|Nessun mapping|SQL_TYPE_DATE (91)|Nessun mapping di [1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|Errore (DM)|Errore (DM)|SQL_DATE (9)|Nessun mapping [2]|  
|SQL_TIME (10)|Nessun mapping|SQL_TYPE_TIME (92)|Nessun mapping di [1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|Errore (DM)|Errore (DM)|SQL_TIME (10)|Nessun mapping [2]|  
|SQL_TIMESTAMP (11)|Nessun mapping|SQL_TYPE_TIMESTAMP (93)|Nessun mapping di [1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|Errore (DM)|Errore (DM)|SQL_TIMESTAMP (11)|Nessun mapping [2]|  
  
 [1] in seguito a questa operazione, un'applicazione ODBC 3. *x* funziona con un'API ODBC 2. *x* driver può utilizzare i codici di data, ora o timestamp restituiti nei set di risultati restituiti dalle funzioni di catalogo.  
  
 [2] in seguito a questa operazione, un'applicazione ODBC 3. *x* funziona con un'applicazione ODBC 3. *x* driver può utilizzare i codici di data, ora o timestamp restituiti nei set di risultati restituiti dalle funzioni di catalogo.
