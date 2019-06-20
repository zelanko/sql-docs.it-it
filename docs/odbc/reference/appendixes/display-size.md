---
title: Dimensioni visualizzazione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- SQL data types [ODBC], column characteristics
ms.assetid: 9f7f766f-2492-463c-aab7-f2476e222042
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c7d4a14a6afc2d716e85e687cbae1a202a596d7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63241245"
---
# <a name="display-size"></a>Dimensioni di visualizzazione
Le dimensioni di visualizzazione di una colonna sono il numero massimo di caratteri necessari per visualizzare i dati in formato carattere. Nella tabella seguente definisce le dimensioni di visualizzazione per ogni tipo di dati SQL ODBC.  
  
|Identificatore di tipo SQL|Dimensioni visualizzazione|  
|-------------------------|------------------|  
|Tutti i tipi di carattere [a]|Il definita (per tipi predefiniti) o massimo (tipi di variabile) numero di caratteri necessari per visualizzare i dati in formato carattere.|  
|SQL_DECIMAL SQL_NUMERIC|La precisione della colonna più 2 (un segno *precisione* cifre e un separatore decimale). Ad esempio, le dimensioni di visualizzazione di una colonna definita come NUMERIC(10,3) sono 12.|  
|SQL_BIT|1 (1 digit).|  
|SQL_TINYINT|4 se firmato (un segno e 3 cifre) o 3 se senza segno (3 cifre).|  
|SQL_SMALLINT|6 se è firmato (un segno e 5 cifre) o 5 se senza segno (5 cifre).|  
|SQL_INTEGER|11 se firmato (un segno e 10 cifre) o 10 se senza segno (10 cifre).|  
|SQL_BIGINT|20 (il segno e 19 cifre, se è firmato o 20 cifre se senza segno).|  
|SQL_REAL|14 (un segno, 7 cifre, un separatore decimale, la lettera *elettronica*, un segno e 2 cifre).|  
|SQL_FLOAT SQL_DOUBLE|24 (un segno, 15 cifre, un separatore decimale, la lettera *elettronica*, un segno e 3 cifre).|  
|Tutti i tipi binari [a]|Il definita o massimo (tipi di variabile) 2 di tempi di lunghezza della colonna. (Ogni byte binario è rappresentato da un numero esadecimale a 2 cifre).|  
|SQL_TYPE_DATE|10 (una data nel formato *aaaa-mm-gg*).|  
|SQL_TYPE_TIME|8 (un'ora nel formato *hh: mm:* )<br /><br /> - oppure -<br /><br /> 9 + *s* (un'ora nel formato *hh.mm.ss*[. fff...], dove *s* precisione frazionaria dei secondi).|  
|SQL_TYPE_TIMESTAMP|19 (per un timestamp nel *aaaa-mm-gg hh.mm.ss* formato)<br /><br /> - oppure -<br /><br /> 20 + *s* (per un timestamp nel *aaaa-mm-gg hh.mm.ss*formato [. fff], in cui *s* precisione frazionaria dei secondi).|  
|Tutti i tipi di dati intervallo|Visualizzare [lunghezza del tipo di dati di intervallo](../../../odbc/reference/appendixes/interval-data-type-length.md).|  
|SQL_GUID|36 (il numero di caratteri nel *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* formato|  
  
 [a] se il driver non è possibile determinare la lunghezza di colonna o parametro di tipi di variabili, restituirà SQL_NO_TOTAL.
