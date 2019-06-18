---
title: Inserimento di righe con SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], inserting rows
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: ed585ea7-4d56-4df9-8dc3-53ca82382450
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b5dac8ae14f01dd464aab42eaed42480f1e715c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62446802"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>Inserimento di righe con SQLBulkOperations
Inserimento di dati con **SQLBulkOperations** è simile all'aggiornamento dati con **SQLBulkOperations** poiché utilizza i dati dai buffer di applicazione associate.  
  
 In modo che ogni colonna nella nuova riga ha un valore, tutte le colonne con un valore di lunghezza/indicatore di SQL_COLUMN_IGNORE associate e tutte le colonne non associate devono accettare i valori NULL oppure avere un valore predefinito.  
  
 Per inserire righe con **SQLBulkOperations**, l'applicazione esegue le operazioni seguenti:  
  
1.  Imposta l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di righe da inserire e inserisce i nuovi valori di dati nei buffer di applicazione associate. Per informazioni su come inviare dati di tipo long con **SQLBulkOperations**, vedere [dati di tipo Long e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
2.  Imposta il valore nel buffer di lunghezza/indicatore di ogni colonna in base alle esigenze. Questa è la lunghezza in byte dei dati o SQL_NTS per le colonne associate ai buffer di stringa, la lunghezza in byte dei dati delle colonne associate a buffer binario e SQL_NULL_DATA per tutte le colonne da impostare su NULL. L'applicazione imposta il valore nel buffer di lunghezza/indicatore di tali colonne che devono essere impostate sui valori predefiniti (se presente) o NULL (se ne esiste uno non) a SQL_COLUMN_IGNORE.  
  
3.  Le chiamate **SQLBulkOperations** con il *operazione* argomento impostato su SQL_ADD.  
  
 Dopo aver **SQLBulkOperations** viene restituito, la riga corrente rimane invariata. Se è associata la colonna del segnalibro (colonna 0), **SQLBulkOperations** restituisce i segnalibri righe inserite nel buffer di set di righe associati a tale colonna.
