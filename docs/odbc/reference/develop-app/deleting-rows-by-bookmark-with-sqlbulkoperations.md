---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5895a106c389afe2d1979cf8d9c16e92f570538a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049944"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>Eliminazione di righe tramite segnalibro con SQLBulkOperations
Quando si elimina una riga dal segnalibro **SQLBulkOperations** consente all'origine dati di eliminare uno o più righe selezionate della tabella. Le righe sono identificate mediante il segnalibro in una colonna del segnalibro associato.  
  
 Per eliminare righe tramite segnalibro con **SQLBulkOperations**, l'applicazione esegue le operazioni seguenti:  
  
1.  Recupera e memorizza nella cache i segnalibri di tutte le righe da eliminare. Se è presente più di un segnalibro e viene utilizzata l'associazione per colonna, i segnalibri vengono archiviati in una matrice. Se è presente più di un segnalibro e viene utilizzata l'associazione per riga, i segnalibri vengono archiviati in una matrice di strutture di riga.  
  
2.  Imposta l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE sul numero di segnalibri e associa i buffer che contiene il valore di segnalibro o la matrice dei segnalibri, alla colonna 0.  
  
3.  Le chiamate **SQLBulkOperations** con *operazione* impostato su SQL_DELETE_BY_BOOKMARK.
