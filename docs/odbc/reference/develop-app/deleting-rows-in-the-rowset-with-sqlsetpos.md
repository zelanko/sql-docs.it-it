---
title: L'eliminazione delle righe nel set di righe con SQLSetPos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], deleting rows
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
ms.assetid: 3117a47d-e179-4f76-89d0-656582f1c9bb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 78ee14838b467cfe6e555c97f1e74c65cccf98ff
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63049831"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>Eliminazione di righe nel set di righe con SQLSetPos
L'operazione di eliminazione della **SQLSetPos** consente all'origine dati di eliminare uno o più righe selezionate di una tabella. Per eliminare le righe con **SQLSetPos**, l'applicazione chiama **SQLSetPos** con *operazione* impostato su SQL_DELETE e *RowNumber* impostato il numero di riga da eliminare. Se *RowNumber* è 0, vengono eliminate tutte le righe nel set di righe.  
  
 Dopo aver **SQLSetPos** viene restituito, la riga eliminata è la riga corrente e lo stato è SQL_ROW_DELETED. La riga non può essere usata in tutte le operazioni ulteriormente posizionate, ad esempio chiamate a **SQLGetData** oppure **SQLSetPos**.  
  
 Quando si eliminano tutte le righe del set di righe (*RowNumber* è uguale a 0), l'applicazione può impedire il driver di eliminare determinate righe utilizzando la matrice di operazione riga, esattamente come per l'operazione di aggiornamento di **SQLSetPos** . (Vedere [aggiornamento di righe nel set di righe con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).)  
  
 Ogni riga eliminata deve essere una riga che esiste nel set di risultati. Se sono stati compilati i buffer dell'applicazione mediante il recupero e se è stata mantenuta una matrice di stato di riga, i valori in ognuna di queste posizioni di riga non devono essere SQL_ROW_DELETED, SQL_ROW_ERROR o SQL_ROW_NOROW.
