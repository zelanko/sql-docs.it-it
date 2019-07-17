---
title: SQLColAttributes (Driver ODBC Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68132624"
---
# <a name="sqlcolattributes-visual-foxpro-odbc-driver"></a>SQLColAttributes (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento contiene informazioni specifiche del Driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Full  
  
 Conformità di API ODBC: A livello centrale  
  
 Restituisce informazioni sul descrittore per una colonna in un set di risultati. Informazioni sul descrittore viene restituiti come una stringa di caratteri, un valore di dipendente dal descrittore di 32 bit o un valore intero.  
  
> [!NOTE]  
>  **SQLColAttributes** non può essere utilizzata per restituire informazioni relative alla colonna di segnalibro (colonna 0).  
  
 Il Driver ODBC Visual FoxPro supporta tutti i *fDescType* valori. La tabella seguente include i commenti sull'implementazione del driver di valori selezionati.  
  
|*fDescType*|Commento|  
|-----------------|-------------|  
|SQL_COLUMN_AUTO_INCREMENT|Restituisce FALSE: Visual FoxPro non dispone di alcun campo di contatore.|  
|SQL_COLUMN_CASE_SENSITIVE|Restituisce sempre TRUE se il tipo di colonna è di carattere.|  
|SQL_COLUMN_LABEL|Restituisce il nome di colonna, che viene restituito da SQL_COLUMN_NAME anche.|  
|SQL_COLUMN_MONEY|Restituisce TRUE se il tipo di colonna è Currency (rappresentato da una "Y" nel linguaggio Visual FoxPro).|  
|SQL_COLUMN_OWNER_NAME|Restituisce sempre una stringa vuota.|  
|SQL_COLUMN_QUALIFIER_NAME|Restituisce sempre una stringa vuota.|  
|SQL_COLUMN_SEARCHABLE|Restituisce SQL_UNSEARCHABLE alle colonne di tipo generale; Queste colonne non possono essere utilizzate in una clausola WHERE.<br /><br /> Restituisce SQL_SEARCHABLE alle colonne di tipo carattere o credito con NOCPTRANS nenastaveno; Queste colonne possono essere utilizzate in una clausola WHERE con qualsiasi operatore di confronto.<br /><br /> Restituisce SQL_ALL_EXCEPT_LIKE per tutti gli altri tipi di colonna; Queste colonne possono essere utilizzate in una clausola WHERE con tutti gli operatori di confronto, ad eccezione di tipo.|  
|SQL_COLUMN_TABLE_NAME|Restituisce sempre una stringa vuota.|  
  
 Per altre informazioni, vedere [SQLColAttributes](../../odbc/reference/syntax/sqlcolattributes-function.md) nel *riferimento per programmatori ODBC*.
