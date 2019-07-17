---
title: Livelli di conformità SQL (Driver ODBC per Oracle) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063353"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>Livello di conformità SQL (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Il Driver ODBC per Oracle supporta la grammatica SQL minima e la grammatica SQL principale e supporta anche le seguenti estensioni ODBC per SQL:  
  
-   Dati di data, ora e timestamp  
  
-   Left e right outer join  
  
-   Funzioni numeriche:  
  
    |||||  
    |-|-|-|-|  
    |Abs|Log|round|Tan|  
    |funzione CEILING|LOG10|second|truncate|  
    |Cos|Mod|accesso||  
    |Exp|Pi|sin||  
    |floor|Power|sqrt||  
  
-   Funzioni di data:  
  
    |||||  
    |-|-|-|-|  
    |CURDATE|DayOfWeek|NomeMese|second|  
    |Funzione Curtime|Dayofyear|minute|week|  
    |Funzione Dayname|Ora|a questo punto|year|  
    |DayOfMonth|Mese|Trimestre||  
  
-   Funzioni stringa:  
  
    |||||  
    |-|-|-|-|  
    |Ascii|Left|Ok|UCase|  
    |Char|Length|RTrim||  
    |Concat|Ltrim|SOUNDEX||  
    |Lcase|Sostituisci|substring||  
  
-   Funzione di conversione dei tipi:  
  
    ||  
    |-|  
    |Converti|  
  
-   Funzioni di sistema:  
  
    ||  
    |-|  
    |Ifnull|  
    |Utente|
