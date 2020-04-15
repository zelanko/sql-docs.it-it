---
title: Eliminazione di righe nel set di righe con SQLSetPos . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 940bcc3e2ee6a042394797d6038028cce64862f1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305952"
---
# <a name="deleting-rows-in-the-rowset-with-sqlsetpos"></a>Eliminazione di righe nel set di righe con SQLSetPos
L'operazione di eliminazione di **SQLSetPos** consente all'origine dati di eliminare una o più righe selezionate di una tabella. Per eliminare righe con **SQLSetPos**, l'applicazione chiama **SQLSetPos** con *Operation* impostato su SQL_DELETE e *RowNumber* impostato sul numero della riga da eliminare. Se *RowNumber* è 0, tutte le righe del set di righe vengono eliminate.  
  
 Dopo la restituzione **di SQLSetPos,** la riga eliminata è la riga corrente e il relativo stato è SQL_ROW_DELETED. La riga non può essere utilizzata in altre operazioni posizionate, ad esempio chiamate a **SQLGetData** o **SQLSetPos**.  
  
 Quando si eliminano tutte le righe del set di righe (*RowNumber* è uguale a 0), l'applicazione può impedire al driver di eliminare determinate righe utilizzando la matrice di operazioni di riga, come per l'operazione di aggiornamento di **SQLSetPos**. Vedere [Aggiornamento delle righe nel set di righe con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
 Ogni riga eliminata deve essere una riga che esiste nel set di risultati. Se i buffer dell'applicazione sono stati riempiti mediante recupero e se è stata mantenuta una matrice di stato di riga, i relativi valori in ognuna di queste posizioni di riga non devono essere SQL_ROW_DELETED, SQL_ROW_ERROR o SQL_ROW_NOROW.
