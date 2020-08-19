---
description: Aggiornamento delle righe tramite segnalibro con SQLBulkOperations
title: Aggiornamento di righe tramite segnalibro con SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], updating rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: c9ad82b7-8dba-45b0-bdb9-f4668b37c0d6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9981136d546d53b131cff0d71edcdeab5b2e650c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482874"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>Aggiornamento delle righe tramite segnalibro con SQLBulkOperations
Quando si aggiorna una riga in base al segnalibro, **SQLBulkOperations** consente all'origine dati di aggiornare una o più righe della tabella. Le righe sono identificate dal segnalibro in una colonna del segnalibro associato. La riga viene aggiornata usando i dati nei buffer dell'applicazione per ogni colonna associata, tranne quando il valore nel buffer di lunghezza/indicatore per una colonna è SQL_COLUMN_IGNORE. Le colonne non vincolate non verranno aggiornate.  
  
 Per aggiornare le righe tramite segnalibro con **SQLBulkOperations**, l'applicazione:  
  
1.  Recupera e memorizza nella cache i segnalibri di tutte le righe da aggiornare. Se è presente più di un segnalibro e l'associazione per colonna viene utilizzata, i segnalibri vengono archiviati in una matrice; Se è presente più di un segnalibro e viene usata l'associazione per riga, i segnalibri vengono archiviati in una matrice di strutture di riga.  
  
2.  Imposta l'attributo dell'istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di segnalibri e associa il buffer che contiene il valore del segnalibro o la matrice di segnalibri alla colonna 0.  
  
3.  Inserisce i nuovi valori dei dati nei buffer del set di righe. Per informazioni su come inviare dati Long con **SQLBulkOperations**, vedere [Long Data e SQLSetPos e SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md).  
  
4.  Imposta il valore nel buffer di lunghezza/indicatore di ogni colonna, se necessario. Si tratta della lunghezza in byte dei dati o SQL_NTS per le colonne associato ai buffer di stringa, la lunghezza in byte dei dati per le colonne associato ai buffer binari e SQL_NULL_DATA per le colonne da impostare su NULL.  
  
5.  Imposta il valore nel buffer di lunghezza/indicatore delle colonne che non devono essere aggiornate per SQL_COLUMN_IGNORE. Sebbene l'applicazione possa ignorare questo passaggio e inviare nuovamente i dati esistenti, questo è inefficiente e rischia di inviare valori all'origine dati troncati durante la lettura.  
  
6.  Chiama **SQLBulkOperations** con l'argomento *Operation* impostato su SQL_UPDATE_BY_BOOKMARK.  
  
 Per ogni riga inviata all'origine dati come aggiornamento, i buffer dell'applicazione devono contenere dati di riga validi. Se i buffer dell'applicazione sono stati riempiti tramite il recupero, se è stata mantenuta una matrice di stato della riga e se il valore di stato di una riga è SQL_ROW_DELETED, SQL_ROW_ERROR o SQL_ROW_NOROW, i dati non validi potrebbero essere inavvertitamente inviati all'origine dati.
