---
title: Comando SET NULL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f8addb9b4c7c200ee8f213bdd959067039ccfff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68063676"
---
# <a name="set-null-command"></a>SET NULL (comando)
Determina il modo in cui i valori null sono supportati dai comandi ALTER TABLE-SQL, CREATE TABLE-SQL e INSERT-SQL.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ATTIVA  
 (Impostazione predefinita per il driver; l'impostazione predefinita per Visual FoxPro è OFF). Specifica che tutte le colonne di una tabella creata con ALTER TABLE e CREATE TABLE consentiranno valori null. È possibile eseguire l'override del supporto di valori null per le colonne nella tabella includendo la clausola NOT NULL nelle definizioni delle colonne.  
  
 Specifica inoltre che INSERT-SQL inserisce valori null in tutte le colonne non incluse nella clausola INSERT-SQL VALUE. INSERT-SQL inserisce i valori null solo nelle colonne che consentono valori null.  
  
 OFF  
 Specifica che tutte le colonne di una tabella creata con ALTER TABLE e CREATE TABLE non consentiranno valori null. È possibile designare il supporto di valori null per le colonne in ALTER TABLE e CREATE TABLE includendo la clausola NULL nelle definizioni delle colonne.  
  
 Specifica inoltre che INSERT-SQL inserisce i valori vuoti in tutte le colonne non incluse nella clausola INSERT-SQL VALUE.  
  
## <a name="remarks"></a>Osservazioni  
 SET NULL interessa solo il modo in cui i valori null sono supportati da ALTER TABLE, CREATE TABLE e INSERT-SQL. Gli altri comandi non sono interessati dal SET NULL.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER TABLE-comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Comando CREATE TABLE-SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT (comando SQL)](../../odbc/microsoft/insert-sql-command.md)
