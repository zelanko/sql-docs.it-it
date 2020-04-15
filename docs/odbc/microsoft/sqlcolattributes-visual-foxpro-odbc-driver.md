---
title: SQLColAttributes (Driver ODBC di Visual FoxPro) . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9508fa7b9ada8273e1250d7584e577892acf5c51
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307912"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento sono contenute informazioni specifiche del driver ODBC di Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Completo  
  
 Conformità API ODBC: livello di baseODBC API Conformance: Core Level  
  
 Restituisce informazioni sul descrittore per una colonna in un set di risultati. Le informazioni sul descrittore vengono restituite come stringa di caratteri, come valore dipendente dal descrittore a 32 bit o come valore intero.  
  
> [!NOTE]  
>  **Impossibile utilizzare SQLColAttributes** per restituire informazioni sulla colonna del segnalibro (colonna 0).  
  
 Il driver ODBC di Visual FoxPro supporta tutti i valori *fDescType.* Nella tabella seguente sono inclusi i commenti sull'implementazione del driver dei valori selezionati.  
  
|*fDescTipo*|Comment|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|Restituisce FALSE: Visual FoxPro non ha campi contatore.|  
|SQL_COLUMN_CASE_SENSITIVE|Restituisce sempre TRUE se il tipo di colonna è Carattere.|  
|SQL_COLUMN_LABEL|Restituisce il nome della colonna, restituito anche da SQL_COLUMN_NAME.|  
|SQL_COLUMN_MONEY|Restituisce TRUE se il tipo di colonna è Currency (rappresentato da una "Y" nel linguaggio Visual FoxPro).|  
|SQL_COLUMN_OWNER_NAME|Restituisce sempre una stringa vuota.|  
|SQL_COLUMN_QUALIFIER_NAME|Restituisce sempre una stringa vuota.|  
|SQL_COLUMN_SEARCHABLE|Restituisce SQL_UNSEARCHABLE per le colonne di tipo Generale; queste colonne non possono essere utilizzate in una clausola WHERE.<br /><br /> Restituisce SQL_SEARCHABLE per le colonne di tipo Carattere o Memo con NOCPTRANS non impostato; queste colonne possono essere utilizzate in una clausola WHERE con qualsiasi operatore di confronto.<br /><br /> Restituisce SQL_ALL_EXCEPT_LIKE per tutti gli altri tipi di colonna; queste colonne possono essere utilizzate in una clausola WHERE con tutti gli operatori di confronto ad eccezione di LIKE.|  
|SQL_COLUMN_TABLE_NAME|Restituisce sempre una stringa vuota.|  
  
 Per ulteriori informazioni, vedere [SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) in *ODBC Programmer's Reference*.
