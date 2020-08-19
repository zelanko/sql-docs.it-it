---
description: Eliminazione di righe tramite segnalibro con SQLBulkOperations
title: Eliminazione di righe tramite segnalibro con SQLBulkOperations | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7dcb96180cdcee5987d8a1cbafeae117ec82bba0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424683"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>Eliminazione di righe tramite segnalibro con SQLBulkOperations
Quando si elimina una riga tramite segnalibro, **SQLBulkOperations** consente all'origine dati di eliminare una o più righe selezionate della tabella. Le righe sono identificate dal segnalibro in una colonna del segnalibro associato.  
  
 Per eliminare righe tramite segnalibro con **SQLBulkOperations**, l'applicazione esegue le operazioni seguenti:  
  
1.  Recupera e memorizza nella cache i segnalibri di tutte le righe da eliminare. Se è presente più di un segnalibro e l'associazione per colonna viene utilizzata, i segnalibri vengono archiviati in una matrice; Se è presente più di un segnalibro e viene usata l'associazione per riga, i segnalibri vengono archiviati in una matrice di strutture di riga.  
  
2.  Imposta l'attributo dell'istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di segnalibri e associa il buffer che contiene il valore del segnalibro o la matrice di segnalibri alla colonna 0.  
  
3.  Chiama **SQLBulkOperations** con l' *operazione* impostata su SQL_DELETE_BY_BOOKMARK.
