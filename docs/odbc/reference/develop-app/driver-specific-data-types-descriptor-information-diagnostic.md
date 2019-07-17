---
title: 'Diagnostica di descrittore, informazioni, tipi specifici del driver: Data, | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa17a5552855916798c78e0e7d371b58e58a401e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046926"
---
# <a name="driver-specific-data-types-descriptor-types-information-types-diagnostic-types-and-attributes"></a>Tipi di dati specifici del driver, tipi di descrittori, tipi di informazioni, tipi di diagnostica e attributi
I driver possono allocare i valori specifici del driver per le operazioni seguenti:  
  
-   **Indicatori di tipo di dati di SQL** questi intervalli vengono usati *ParameterType* nelle **SQLBindParameter** e in *DataType* in **SQLGetTypeInfo** e restituito da **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLGetTypeInfo**,  **SQLDescribeParam**, **SQLProcedureColumns**, e **SQLSpecialColumns**.  
  
-   **Campi del descrittore** questi intervalli vengono usati *FieldIdentifier* nelle **SQLColAttribute**, **SQLGetDescField**, e **SQLSetDescField**.  
  
-   **I campi di diagnostica** questi intervalli vengono usati *DiagIdentifier* nelle **SQLGetDiagField** e **SQLGetDiagRec**.  
  
-   **Tipi di informazioni** questi intervalli vengono usati *InfoType* nelle **SQLGetInfo**.  
  
-   **Connessione e gli attributi di istruzione** questi intervalli vengono usati *attributo* nelle **SQLGetConnectAttr**, **SQLGetStmtAttr**,  **SQLSetConnectAttr**, e **SQLSetStmtAttr**.  
  
 Per ognuno di questi elementi, sono disponibili due set di valori: valori riservati per l'utilizzo da ODBC e valori riservati per i driver. Prima di implementare i valori specifici del driver, un writer di driver deve richiedere un valore per ogni tipo specifico del driver, un campo o attributo da Open Group. Per i nuovi sviluppi di driver, utilizzare l'intervallo descritto nella tabella seguente. La gestione dei Driver di ODBC 3.8 non genererà un errore se viene usato un valore sconosciuto che non è compreso nell'intervallo descritto di seguito. Tuttavia, le versioni successive di gestione Driver potrebbero generare un errore se i valori sconosciuti vengono ricevuti che non sono compresi nell'intervallo.  
  
 Quando uno di questi valori viene passato a una funzione ODBC, il driver deve controllare se il valore è valido. I driver restituiscono SQLSTATE HYC00 (funzionalità facoltativa non implementata) per valori specifici del driver che si applicano a altri driver.  
  
 A partire da ODBC 3.8, gli sviluppatori di driver possono allocare gli attributi specifici del driver all'interno di un intervallo riservato.  
  
> [!NOTE]  
>  La gestione dei Driver di ODBC 3.8 convalida né applica questi intervalli per la compatibilità con le versioni precedenti. Potrebbe imporre, tuttavia, una versione futura di gestione Driver.  
  
|Tipo di attributo|Tipo di dati ODBC|Intervallo di specifiche del driver base|Limite dell'intervallo di specifiche del driver|Costante ODBC per l'intervallo di valori specifici del driver base|  
|--------------------|--------------------|---------------------------------|----------------------------------|---------------------------------------------------------|  
|Gli indicatori di tipo di dati SQL|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_SQL_TYPE_BASE|  
|Campi di descrizione|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DESCRIPTOR_BASE|  
|Campi di diagnostica|SQLSMALLINT|0x4000|0x7FFF|SQL_DRIVER_DIAGNOSTIC_BASE|  
|Tipi di informazioni|SQLUSMALLINT|0x4000|0x7FFF|SQL_DRIVER_INFO_TYPE_BASE|  
|Attributi di connessione|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_CONNECT_ATTR_BASE|  
|Attributi di istruzione|SQLINTEGER|0x00004000|0x00007FFF|SQL_DRIVER_STATEMENT_ATTR_BASE|  
  
> [!NOTE]  
>  Tipi di dati specifici del driver, i campi di descrizione, i campi di diagnostica, i tipi di informazioni, gli attributi di istruzione e gli attributi di connessione devono essere descritte nella documentazione del driver. Quando uno di questi valori viene passato a una funzione ODBC, il driver deve controllare se il valore è valido. I driver restituiscono SQLSTATE HYC00 (funzionalità facoltativa non implementata) per valori specifici del driver che si applicano a altri driver.  
  
 I valori di base sono definiti per facilitare lo sviluppo di driver. Attributi di diagnostica specifici del driver, ad esempio, possono essere definiti nel formato seguente:  
  
```  
SQL_DRIVER_DIAGNOSTIC_BASE+0, SQL_DRIVER_DIAGNOSTIC_BASE +1  
```
