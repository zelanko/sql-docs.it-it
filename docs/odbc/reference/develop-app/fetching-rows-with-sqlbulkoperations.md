---
title: Recupero di righe con SQLBulkOperations Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], fetching rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: 0efee2d6-ce94-411e-9976-97ba28b8da37
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae0b4c2114059cecaaf8f8825169300f131bd473
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305650"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>Recupero di righe con SQLBulkOperations
I dati possono essere recuperati in un set di righe utilizzando i segnalibri da una chiamata a **SQLBulkOperations.Data** can be refetched into a rowset using bookmarks by a call to SQLBulkOperations. Le righe da recuperare sono identificate dai segnalibri in una colonna di segnalibri associata. Le colonne con un valore di SQL_COLUMN_IGNORE non vengono recuperate.  
  
 Per eseguire operazioni di esecuzione bulk con **SQLBulkOperations**, l'applicazione esegue le operazioni seguenti:  
  
1.  Recupera e memorizza nella cache i segnalibri di tutte le righe da aggiornare. Se è presente più di un segnalibro e viene utilizzata l'associazione per colonna, i segnalibri vengono archiviati in una matrice; se è presente più di un segnalibro e viene utilizzata l'associazione per riga, i segnalibri vengono archiviati in una matrice di strutture di riga.  
  
2.  Imposta l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di righe da recuperare e associa il buffer contenente il valore del segnalibro o la matrice di segnalibri alla colonna 0.  
  
3.  Imposta il valore nel buffer di lunghezza/indicatore di ogni colonna in base alle esigenze. Si tratta della lunghezza in byte dei dati o SQL_NTS per le colonne associate a buffer di stringa, la lunghezza in byte dei dati per le colonne associate a buffer binari e SQL_NULL_DATA per tutte le colonne da impostare su NULL. L'applicazione imposta il valore nel buffer di lunghezza/indicatore delle colonne che devono essere impostate sul valore predefinito (se presente) o NULL (se non) su SQL_COLUMN_IGNORE.  
  
4.  Chiama **SQLBulkOperations** con l'argomento *Operation* impostato su SQL_FETCH_BY_BOOKMARK.  
  
 Non è necessario che l'applicazione utilizzi la matrice di operazioni di riga per impedire l'esecuzione dell'operazione su determinate colonne. L'applicazione seleziona le righe che desidera recuperare copiando solo i segnalibri per tali righe nella matrice di segnalibri associata.
