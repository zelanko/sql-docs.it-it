---
title: Matrice di stato della riga Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 60dead23fe0051c05698e094f37ddad96b2b337d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304292"
---
# <a name="row-status-array"></a>Matrice di stato riga
Oltre ai dati, **SQLFetch** e **SQLFetchScroll** possono restituire una matrice che fornisce lo stato di ogni riga nel set di righe. Questa matrice viene specificata tramite l'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR. Questa matrice viene allocata dall'applicazione e deve avere tutti gli elementi specificati dall'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE. I valori nella matrice vengono impostati da **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**e **SQLSetPos.** I valori descrivono lo stato della riga e se tale stato è stato modificato dall'ultimo recupero.  
  
|Valore della matrice di stato della riga|Descrizione|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|La riga è stata recuperata correttamente e non è stata modificata dall'ultimo recupero.|  
|SQL_ROW_SUCCESS_WITH_INFO|La riga è stata recuperata correttamente e non è stata modificata dall'ultimo recupero. Tuttavia, è stato restituito un avviso relativo alla riga.|  
|SQL_ROW_ERROR|Si è verificato un errore durante il recupero della riga.|  
|SQL_ROW_UPDATED|La riga è stata recuperata correttamente ed è stata aggiornata dall'ultimo recupero. Se la riga viene recuperata nuovamente o aggiornata da **SQLSetPos**, il relativo stato viene modificato nel nuovo stato.<br /><br /> Alcuni driver non sono in grado di rilevare le modifiche apportate ai dati e pertanto non possono restituire questo valore. Per determinare se un driver può rilevare gli aggiornamenti alle righe rerecuperate, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_ROW_UPDATES.|  
|SQL_ROW_DELETED|La riga è stata eliminata dall'ultimo recupero.|  
|SQL_ROW_ADDED|La riga è stata inserita da **SQLBulkOperations**. Se la riga viene recuperata nuovamente o viene aggiornata da **SQLSetPos**, il relativo stato è SQL_ROW_SUCCESS.<br /><br /> Questo valore non è impostato da **SQLFetch** o **SQLFetchScroll**.|  
|SQL_ROW_NOROW|Il set di righe si sovrapponeva alla fine del set di risultati e non veniva restituita alcuna riga corrispondente a questo elemento della matrice di stato della riga.|
