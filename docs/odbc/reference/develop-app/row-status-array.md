---
title: Matrice di stato di riga | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- cursors [ODBC], block
- result sets [ODBC], row status array
- block cursors [ODBC]
- result sets [ODBC], block cursors
- rowset status [ODBC]
ms.assetid: 4b69f189-2722-4314-8a02-f4ffecd6dabd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 57b187bf4f14bd5c05f91a433fa331e954fa0fb9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020375"
---
# <a name="row-status-array"></a>Matrice di stato riga
Oltre ai dati, **SQLFetch** e **SQLFetchScroll** può restituire una matrice che contiene lo stato di ogni riga nel set di righe. Questa matrice viene specificata tramite l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR. Questa matrice viene allocata dall'applicazione e deve avere tanti elementi come vengono specificati mediante l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE. I valori nella matrice sono impostati dallo **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, e **SQLSetPos.** I valori descrivono lo stato della riga e se tale stato è stato modificato dopo l'ultimo recupero.  
  
|Valore di matrice di stato riga|Descrizione|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|La riga è stata recuperata correttamente e non è stato modificato dopo l'ultimo recupero.|  
|SQL_ROW_SUCCESS_WITH_INFO|La riga è stata recuperata correttamente e non è stato modificato dopo l'ultimo recupero. Tuttavia, è stato restituito un avviso sulla riga.|  
|SQL_ROW_ERROR|Si è verificato un errore durante il recupero della riga.|  
|SQL_ROW_UPDATED|La riga è stata recuperata correttamente ed è stata aggiornata dopo l'ultimo recupero. Se la riga è recuperata di nuovo o aggiornata da **SQLSetPos**, il relativo stato viene modificato per il nuovo stato.<br /><br /> Alcuni driver non è in grado di rilevare le modifiche ai dati e pertanto non può restituire questo valore. Per determinare se un driver può rilevare gli aggiornamenti alle righe refetched, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_ROW_UPDATES.|  
|SQL_ROW_DELETED|La riga è stata eliminata dopo l'ultimo recupero.|  
|SQL_ROW_ADDED|La riga inserita da **SQLBulkOperations**. Se la riga è recuperata nuovamente o viene aggiornata dal **SQLSetPos**, il suo stato sia SQL_ROW_SUCCESS.<br /><br /> Questo valore non è impostato **SQLFetch** oppure **SQLFetchScroll**.|  
|SQL_ROW_NOROW|Il set di righe sovrapposti la fine del set di risultati, ed è stata restituita alcuna riga che corrisponde a questo elemento della matrice di stato di riga.|
