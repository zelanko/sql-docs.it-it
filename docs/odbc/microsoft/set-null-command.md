---
title: Comando NULL SET | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063676"
---
# <a name="set-null-command"></a>SET NULL (comando)
Determina come valori null sono supportati per l'istruzione ALTER TABLE - SQL, CREATE TABLE - SQL e INSERT - comandi SQL.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ON  
 (Valore predefinito per il driver, il valore predefinito di Visual FoxPro è impostata su OFF). Specifica che tutte le colonne in una tabella creata con CREATE TABLE e ALTER TABLE consentirà valori null. È possibile eseguire l'override di supporto di valori null per le colonne nella tabella includendo la clausola NOT NULL nelle definizioni di colonne.  
  
 Specifica inoltre che INSERT - SQL verrà inserire valori null in tutte le colonne non incluse nell'istruzione INSERT - clausola VALUE SQL. INSERT - SQL inserirà valori null solo in colonne che ammettono valori null.  
  
 OFF  
 Specifica che tutte le colonne in una tabella creata con CREATE TABLE e ALTER TABLE non consente valori null. È possibile designare il supporto di valori null per le colonne nell'istruzione ALTER TABLE e CREATE TABLE, includendo la clausola NULL nelle definizioni di colonne.  
  
 Specifica inoltre che INSERT - SQL inserirà valori vuoti in tutte le colonne non incluse nell'istruzione INSERT - clausola VALUE SQL.  
  
## <a name="remarks"></a>Note  
 SET NULL i valori solo come null influisce sono supportati da ALTER TABLE, CREATE TABLE e INSERT - SQL. Altri comandi non sono interessati dal SET NULL.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER TABLE - comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Crea tabella - comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT (comando SQL)](../../odbc/microsoft/insert-sql-command.md)
