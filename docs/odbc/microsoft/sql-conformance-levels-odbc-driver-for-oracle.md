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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 969296e377d398615ad95cf1337c3f9f97d5eb5c
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363401"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>Livello di conformità SQL (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Il driver ODBC per Oracle supporta la grammatica SQL minima e la grammatica SQL di base e supporta anche le estensioni ODBC seguenti per SQL:  
  
-   Dati data, ora e timestamp  
  
-   Join a sinistra e right outer  
  
-   Funzioni numeriche:  

    :::row:::
        :::column:::
            Abs  
            Ceiling  
            Cos  
            Exp  
            Piano  
        :::column-end:::
        :::column:::
            File di log  
            Log10  
            Mod  
            Pi  
            Elettricità  
        :::column-end:::
        :::column:::
            round  
            second  
            sign  
            sin  
            sqrt  
        :::column-end:::
        :::column:::
            tan  
            truncate  
        :::column-end:::
    :::row-end:::
    
-   Funzioni di data:  

    :::row:::
        :::column:::
            CURDATE  
            Curtime  
            NomeGiorno  
            DayOfMonth  
        :::column-end:::
        :::column:::
            DayOfWeek  
            Dayofyear  
            Ora  
            Month  
        :::column-end:::
        :::column:::
            MonthName  
            minute  
            now  
            quarter  
        :::column-end:::
        :::column:::
            second  
            week  
            year  
        :::column-end:::
    :::row-end:::

-   Funzioni di stringa:  

    :::row:::
        :::column:::
            Ascii  
            Char  
            Concat  
            Lcase  
        :::column-end:::
        :::column:::
            Sinistra  
            Length  
            Ltrim  
            Sostituisci  
        :::column-end:::
        :::column:::
            right  
            RTRIM  
            SOUNDEX  
            substring  
        :::column-end:::
        :::column:::
            UCase  
        :::column-end:::
    :::row-end:::

-   Funzione di conversione del tipo:  

    Conversione  

-   Funzioni di sistema:  
  
    Ifnull  
    Utente
