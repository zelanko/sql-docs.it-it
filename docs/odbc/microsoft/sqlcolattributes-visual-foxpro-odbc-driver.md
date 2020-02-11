---
title: SQLColAttributes (driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: d403dfa0-c26d-47d4-91d9-2f29aa387399
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9fb35211160cb7cba866c2b1c9b1cf72340e92ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132624"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: completo  
  
 Conformità API ODBC: livello principale  
  
 Restituisce informazioni sul descrittore per una colonna in un set di risultati. Le informazioni sul descrittore vengono restituite come una stringa di caratteri, un valore dipendente dal descrittore a 32 bit o un valore integer.  
  
> [!NOTE]  
>  Impossibile utilizzare **SQLColAttributes** per restituire informazioni sulla colonna del segnalibro (colonna 0).  
  
 Il driver ODBC Visual FoxPro supporta tutti i valori *fDescType* . Nella tabella seguente sono inclusi i commenti sull'implementazione del driver dei valori selezionati.  
  
|*fDescType*|Comment|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|Restituisce FALSE: Visual FoxPro non contiene campi contatore.|  
|SQL_COLUMN_CASE_SENSITIVE|Restituisce sempre TRUE se il tipo di colonna è character.|  
|SQL_COLUMN_LABEL|Restituisce il nome della colonna, che viene restituito anche da SQL_COLUMN_NAME.|  
|SQL_COLUMN_MONEY|Restituisce TRUE se il tipo di colonna è Currency (rappresentato da una "Y" nel linguaggio Visual FoxPro).|  
|SQL_COLUMN_OWNER_NAME|Restituisce sempre una stringa vuota.|  
|SQL_COLUMN_QUALIFIER_NAME|Restituisce sempre una stringa vuota.|  
|SQL_COLUMN_SEARCHABLE|Restituisce SQL_UNSEARCHABLE per le colonne di tipo generale; Queste colonne non possono essere utilizzate in una clausola WHERE.<br /><br /> Restituisce SQL_SEARCHABLE per le colonne di tipo character o Memo con NOCPTRANS non impostato. Queste colonne possono essere utilizzate in una clausola WHERE con qualsiasi operatore di confronto.<br /><br /> Restituisce SQL_ALL_EXCEPT_LIKE per tutti gli altri tipi di colonna; Queste colonne possono essere utilizzate in una clausola WHERE con tutti gli operatori di confronto, ad eccezione di come.|  
|SQL_COLUMN_TABLE_NAME|Restituisce sempre una stringa vuota.|  
  
 Per ulteriori informazioni, vedere [SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) in *ODBC Programmer ' s Reference*.
