---
title: Funzioni di data e ora (driver ODBC Di Visual FoxPro) . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC date functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], time and date functions
- FoxPro ODBC driver [ODBC], time and date functions
- time and date functions [ODBC]
- ODBC time and date functions [ODBC]
- date functions [ODBC]
ms.assetid: c1fb63b7-af50-45d6-8dec-ae6ea7119527
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86260f8e7245bed15122d4dbfc4649131674e17f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303062"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>Funzioni data e ora (driver ODBC Visual FoxPro)
Nella tabella seguente sono elencate le funzioni di data e ora ODBC supportate dal driver ODBC di Visual FoxPro. Quando la grammatica di Visual FoxPro per la stessa funzione è diversa dalla sintassi ODBC, viene elencato l'equivalente di Visual FoxPro.  
  
|Grammatica ODBC|Grammatica di Visual FoxPro|  
|------------------|---------------------------|  
|CURDATE *( )*|DATA *( )*|  
|CURTIME *( )*|TEMPO *( )*|  
|DAYNAME *(date_exp)*|CDOW *(date_exp)*|  
|GIORNOOFMONTH(*date_exp)*|GIORNO *( )*|  
|ORA *(time_exp)*||  
|MINUTO *(time_exp)*||  
|MESE *(time_exp)*||  
|MONTHNAME *(date_exp)*|CMONTH *(date_exp)*|  
|ORA *( )*|DATETIME *( )*|  
|SECONDO *(time_exp)*|SEC *(time_exp)*|  
|SETTIMANA *(date_exp)*||  
|ANNO *(date_exp)*||  
  
 Le seguenti funzioni di data e ora non sono supportate:  
  
 GIORNOOFYEAR *(date_exp)*  
  
 QUARTER *(date_exp)*  
  
 TIMESTAMPADD *(intervallo, integer_exp, timestamp_exp)*  
  
 TIMESTAMPDIFF *(intervallo, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>Sequenze di escape ODBC  
 Il driver supporta anche la sequenza di escape ODBC per i dati di data e timestamp. La sintassi della clausola di escape è la seguente:The escape clause syntax is as follows:  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 In questa sintassi, **d** indica che *value* è una data nel formato *aaaa-mm-gg* e **ts** indica che *value* è un timestamp in *yyyy-mm-dd hh:mm:ss*[.* f...*] Formato. La sintassi abbreviata per i dati di data e ora è la seguente:  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 Ad esempio, ognuna delle istruzioni seguenti aggiorna la tabella ALLTYPES utilizzando la sintassi a sintassi a sintassi a sintassi a sintassi a sintassi a sintassi a sintassi a sintassi a sintassi a sintassi data e ora e ora in un comando SQL UPDATE supportato:  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>Osservazioni  
 Per ulteriori informazioni sulle sequenze di escape, vedere [Sequenze di escape in ODBC](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) in ODBC *Programmer's Reference*.
