---
title: Funzioni di data e ora (driver ODBC Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303062"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>Funzioni data e ora (driver ODBC Visual FoxPro)
Nella tabella seguente sono elencate le funzioni di data e ora ODBC supportate dal driver ODBC Visual FoxPro. Quando la grammatica Visual FoxPro per la stessa funzione differisce dalla sintassi ODBC, viene elencato l'equivalente Visual FoxPro.  
  
|Grammatica ODBC|Grammatica Visual FoxPro|  
|------------------|---------------------------|  
|CAGLIo *()*|Data *()*|  
|CURTIME *()*|ORA *()*|  
|NOMEGIORNO *(date_exp)*|CDOW *(date_exp)*|  
|DAYOFMONTH (*date_exp)*|GIORNO *()*|  
|ORA *(time_exp)*||  
|MINUTO *(time_exp)*||  
|MESE *(time_exp)*||  
|MONTHname *(date_exp)*|CMONTH *(date_exp)*|  
|ORA *()*|DATETIME *()*|  
|SECONDO *(time_exp)*|SEC *(time_exp)*|  
|SETTIMANA *(date_exp)*||  
|ANNO *(date_exp)*||  
  
 Le funzioni di data e ora seguenti non sono supportate:  
  
 DAYOFYEAR *(date_exp)*  
  
 TRIMESTRE *(date_exp)*  
  
 TIMESTAMPADD *(intervallo, integer_exp, timestamp_exp)*  
  
 TIMESTAMPDIFF *(intervallo, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>Sequenze di escape ODBC  
 Il driver supporta inoltre la sequenza di escape ODBC per i dati di data e timestamp. La sintassi della clausola escape è la seguente:  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 In questa sintassi, **d** indica che *value* è una data nel formato *aaaa-mm-gg* e **TS** indica che il *valore* è un timestamp in *aaaa-mm-gg hh: mm: SS*[.* f...*] formato. La sintassi abbreviata per i dati di data e timestamp è la seguente:  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 Ogni istruzione seguente, ad esempio, aggiorna la tabella ALLTYPES usando la sintassi abbreviata date e timestamp in un comando SQL UPDATE supportato:  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>Osservazioni  
 Per ulteriori informazioni sulle sequenze di escape, vedere [sequenze di escape in ODBC](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) in ODBC *Programmer ' s Reference*.
