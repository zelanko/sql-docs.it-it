---
title: Comando SET NULL Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c83c9ef9f8a0ce143308b73d8df09b05fb2cdea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300811"
---
# <a name="set-null-command"></a>SET NULL (comando)
Determina il modo in cui i valori null sono supportati dai comandi SQL TABLE - SQL, CREATE TABLE - SQL e INSERT .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ON  
 (Impostazione predefinita per il driver; l'impostazione predefinita per Visual FoxPro è OFF. Specifica che tutte le colonne di una tabella creata con ALTER TABLE e CREATE TABLE consentiranno valori Null. È possibile eseguire l'override del supporto dei valori Null per le colonne della tabella includendo la clausola NOT NULL nelle definizioni delle colonne.  
  
 Specifica inoltre che INSERT - SQL inserirà valori null in tutte le colonne non incluse nella clausola INSERT - SQL VALUE. INSERT: SQL inserirà valori Null solo nelle colonne che consentono valori Null.INSERT - SQL will insert null values only in columns that allow null values.  
  
 OFF  
 Specifica che tutte le colonne di una tabella creata con ALTER TABLE e CREATE TABLE non consentiranno valori Null. È possibile designare il supporto del valore Null per le colonne in ALTER TABLE e CREATE TABLE includendo la clausola NULL nelle definizioni delle colonne.  
  
 Specifica inoltre che INSERT - SQL inserirà valori vuoti in tutte le colonne non incluse nella clausola INSERT - SQL VALUE.  
  
## <a name="remarks"></a>Osservazioni  
 SET NULL influisce solo sul modo in cui i valori Null sono supportati da ALTER TABLE, CREATE TABLE e INSERT - SQL. Altri comandi non sono interessati da SET NULL.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER TABLE - Comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [CREATE TABLE - Comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT (comando SQL)](../../odbc/microsoft/insert-sql-command.md)
