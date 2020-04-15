---
title: Tipi specifici del driver - Dati, descrittore, Informazioni, Diagnostica . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver-specific diagnostic values [ODBC]
- diagnostic information [ODBC], driver-specific values
- ODBC drivers [ODBC], driver-specific diagnostic values
ms.assetid: ad4c76d3-5191-4262-b47c-5dd1d19d1154
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19bb2dd113fbeae871892ea510713c638c886e5a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305767"
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipi di dati specifici del driver, tipi di descrittori, tipi di informazioni, tipi di diagnostica e attributi
I driver possono allocare valori specifici del driver per gli elementi seguenti:Drivers can allocate driver-specific values for the following:  
  
-   **Indicatori del tipo di dati SQLSQL Data Type Indicators** Vengono utilizzati in *ParameterType* in **SQLBindParameter** e in *DataType* in **SQLGetTypeInfo** e restituiti da **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLGetTypeInfo**, **SQLDescribeParam**, **SQLProcedureColumns**e **SQLSpecialColumns**.  
  
-   **Campi descrittore** Vengono utilizzati in *FieldIdentifier* in **SQLColAttribute**, **SQLGetDescField**e **SQLSetDescField**.  
  
-   **Campi di diagnostica** Vengono utilizzati in *DiagIdentifier* in **SQLGetDiagField** e **SQLGetDiagRec**.  
  
-   **Tipi di informazioni** Questi vengono utilizzati in *InfoType* in **SQLGetInfo**.  
  
-   **Attributi di connessione e istruzioneConnection and Statement Attributes** Vengono utilizzati in *Attribute* in **SQLGetConnectAttr**, **SQLGetSttAttr**, **SQLSetConnectAttr**e **SQLSetStmtAttr**.  
  
 Per ognuno di questi elementi, sono disponibili due set di valori: valori riservati per l'utilizzo da ODBC e valori riservati per l'utilizzo da parte dei driver. Prima di implementare i valori specifici del driver, un writer di driver deve richiedere un valore per ogni tipo, campo o attributo specifico del driver da Open Group. Per lo sviluppo di nuovi driver, utilizzare l'intervallo descritto nella tabella seguente. Gestione Driver ODBC 3.8 non genererà un errore se viene utilizzato un valore sconosciuto che non è compreso nell'intervallo descritto di seguito. Tuttavia, le versioni successive di Gestione Driver potrebbero generare un errore se vengono ricevuti valori sconosciuti che non sono compresi nell'intervallo.  
  
 Quando uno di questi valori viene passato a una funzione ODBC, il driver deve verificare se il valore è valido. I driver restituiscono SQLSTATE HYC00 (funzionalità facoltativa non implementata) per i valori specifici del driver che si applicano ad altri driver.  
  
 A partire da ODBC 3.8, i writer di driver possono allocare attributi specifici del driver all'interno di un intervallo riservato.  
  
> [!NOTE]  
>  Gestione Driver ODBC 3.8 non convalida né applica questi intervalli per garantire la compatibilità con le versioni precedenti. Una versione futura di Gestione Driver potrebbe applicarli, tuttavia.  
  
|Tipo di attributo|Tipo di dati ODBC|Base di portata specifica del driver|Limite intervallo specifico del driver|Costante ODBC per la base dell'intervallo di valori specifici del driver|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|Indicatori del tipo di dati SQL|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|Campi descrittore|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|Campi diagnostici|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|Tipi di informazioni|SQLUSMALLINT (informazioni in lingua inglese)|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|Attributi di connessione|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|Attributi dell'istruzione|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  I tipi di dati specifici del driver, i campi descrittore, i campi di diagnostica, i tipi di informazioni, gli attributi dell'istruzione e gli attributi di connessione devono essere descritti nella documentazione del driver. Quando uno di questi valori viene passato a una funzione ODBC, il driver deve verificare se il valore è valido. I driver restituiscono SQLSTATE HYC00 (funzionalità facoltativa non implementata) per i valori specifici del driver che si applicano ad altri driver.  
  
 I valori di base sono definiti per facilitare lo sviluppo del driver. Ad esempio, gli attributi di diagnostica specifici del driver possono essere definiti nel seguente formato:  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
