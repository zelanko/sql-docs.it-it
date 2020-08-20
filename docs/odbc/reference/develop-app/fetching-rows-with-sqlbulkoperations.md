---
description: Recupero di righe con SQLBulkOperations
title: Recupero di righe con SQLBulkOperations | Microsoft Docs
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
ms.openlocfilehash: e4c3cb6a38e3ef9c42f4e853b8c406579b5c0236
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499871"
---
# <a name="fetching-rows-with-sqlbulkoperations"></a>Recupero di righe con SQLBulkOperations
I dati possono essere recuperati in un set di righe usando i segnalibri tramite una chiamata a **SQLBulkOperations.** Le righe da recuperare sono identificate dai segnalibri in una colonna del segnalibro associato. Le colonne con un valore di SQL_COLUMN_IGNORE non vengono recuperate.  
  
 Per eseguire il recupero bulk con **SQLBulkOperations**, l'applicazione esegue le operazioni seguenti:  
  
1.  Recupera e memorizza nella cache i segnalibri di tutte le righe da aggiornare. Se è presente più di un segnalibro e l'associazione per colonna viene utilizzata, i segnalibri vengono archiviati in una matrice; Se è presente più di un segnalibro e viene usata l'associazione per riga, i segnalibri vengono archiviati in una matrice di strutture di riga.  
  
2.  Imposta l'attributo dell'istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di righe da recuperare e associa il buffer che contiene il valore del segnalibro o la matrice di segnalibri alla colonna 0.  
  
3.  Imposta il valore nel buffer di lunghezza/indicatore di ogni colonna, se necessario. Si tratta della lunghezza in byte dei dati o SQL_NTS per le colonne associato ai buffer di stringa, la lunghezza in byte dei dati per le colonne associato ai buffer binari e SQL_NULL_DATA per le colonne da impostare su NULL. L'applicazione imposta il valore nel buffer di lunghezza/indicatore delle colonne che devono essere impostate sul valore predefinito (se presente) o NULL (se non ne esiste uno) per SQL_COLUMN_IGNORE.  
  
4.  Chiama **SQLBulkOperations** con l'argomento *Operation* impostato su SQL_FETCH_BY_BOOKMARK.  
  
 Non è necessario che l'applicazione utilizzi la matrice dell'operazione di riga per impedire l'esecuzione dell'operazione su determinate colonne. L'applicazione seleziona le righe da recuperare copiando solo i segnalibri per tali righe nella matrice di segnalibri associati.
