---
description: Inserimento di righe con SQLBulkOperations
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36f04a393d2053389f823c33a55050f24dd87020
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424633"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>Inserimento di righe con SQLBulkOperations
L'inserimento di dati con **SQLBulkOperations** è simile all'aggiornamento dei dati con **SQLBulkOperations** perché usa i dati dei buffer dell'applicazione associati.  
  
 In modo che ogni colonna nella nuova riga abbia un valore, tutte le colonne associate con un valore di lunghezza/indicatore di SQL_COLUMN_IGNORE e tutte le colonne non associate devono accettare valori NULL o avere un valore predefinito.  
  
 Per inserire righe con **SQLBulkOperations**, l'applicazione esegue le operazioni seguenti:  
  
1.  Imposta l'attributo dell'istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di righe da inserire e inserisce i nuovi valori dei dati nei buffer dell'applicazione associati. Per informazioni su come inviare dati Long con **SQLBulkOperations**, vedere [Long Data e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
2.  Imposta il valore nel buffer di lunghezza/indicatore di ogni colonna, se necessario. Si tratta della lunghezza in byte dei dati o SQL_NTS per le colonne associato ai buffer di stringa, la lunghezza in byte dei dati per le colonne associato ai buffer binari e SQL_NULL_DATA per le colonne da impostare su NULL. L'applicazione imposta il valore nel buffer di lunghezza/indicatore delle colonne che devono essere impostate sul valore predefinito (se presente) o NULL (se non ne esiste uno) per SQL_COLUMN_IGNORE.  
  
3.  Chiama **SQLBulkOperations** con l'argomento *Operation* impostato su SQL_ADD.  
  
 Dopo la restituzione di **SQLBulkOperations** , la riga corrente è invariata. Se la colonna del segnalibro (colonna 0) è associata, **SQLBulkOperations** restituisce i segnalibri delle righe inserite nel buffer del set di righe associato a tale colonna.
