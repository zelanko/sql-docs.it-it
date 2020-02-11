---
title: Livelli di conformità SQL (driver ODBC per Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 241f4f3da12f63c15d917a0e47cb13ad0e96e6e3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063353"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>Livello di conformità SQL (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Il driver ODBC per Oracle supporta la grammatica SQL minima e la grammatica SQL di base e supporta anche le estensioni ODBC seguenti per SQL:  
  
-   Dati data, ora e timestamp  
  
-   Join a sinistra e right outer  
  
-   Funzioni numeriche:  
  
    |||||  
    |-|-|-|-|  
    |Abs|File di log|round|tan|  
    |Ceiling|Log10|second|truncate|  
    |Cos|Mod|sign||  
    |Exp|Pi|sin||  
    |Piano|Potenza|sqrt||  
  
-   Funzioni di data:  
  
    |||||  
    |-|-|-|-|  
    |CURDATE|DayOfWeek|MonthName|second|  
    |Curtime|Dayofyear|minute|week|  
    |NomeGiorno|Ora|now|year|  
    |DayOfMonth|Month|quarter||  
  
-   Funzioni di stringa:  
  
    |||||  
    |-|-|-|-|  
    |Ascii|Left|Ok|UCase|  
    |Char|Length|RTRIM||  
    |Concat|Ltrim|SOUNDEX||  
    |Lcase|Replace|substring||  
  
-   Funzione di conversione del tipo:  
  
    ||  
    |-|  
    |Conversione|  
  
-   Funzioni di sistema:  
  
    ||  
    |-|  
    |Ifnull|  
    |Utente|
