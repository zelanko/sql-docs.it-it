---
title: Matrice di stato riga | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020375"
---
# <a name="row-status-array"></a>Matrice di stato riga
Oltre ai dati, **SQLFetch** e **SQLFetchScroll** possono restituire una matrice che fornisce lo stato di ogni riga nel set di righe. Questa matrice viene specificata tramite l'attributo dell'istruzione SQL_ATTR_ROW_STATUS_PTR. Questa matrice viene allocata dall'applicazione e deve avere tutti gli elementi specificati dall'attributo dell'istruzione SQL_ATTR_ROW_ARRAY_SIZE. I valori nella matrice vengono impostati da **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**e **SQLSetPos.** I valori descrivono lo stato della riga e se lo stato è stato modificato dopo l'ultimo recupero.  
  
|Valore matrice stato riga|Descrizione|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|La riga è stata recuperata e non è stata modificata dopo l'ultima operazione di recupero.|  
|SQL_ROW_SUCCESS_WITH_INFO|La riga è stata recuperata e non è stata modificata dopo l'ultima operazione di recupero. Tuttavia, è stato restituito un avviso sulla riga.|  
|SQL_ROW_ERROR|Si è verificato un errore durante il recupero della riga.|  
|SQL_ROW_UPDATED|La riga è stata recuperata ed è stata aggiornata da quando è stata eseguita l'ultima operazione di recupero. Se la riga viene recuperata o aggiornata da **SQLSetPos**, il relativo stato viene impostato sul nuovo stato.<br /><br /> Alcuni driver non sono in grado di rilevare le modifiche ai dati e pertanto non possono restituire questo valore. Per determinare se un driver è in grado di rilevare gli aggiornamenti alle righe recuperate, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_ROW_UPDATES.|  
|SQL_ROW_DELETED|La riga è stata eliminata dall'ultimo recupero.|  
|SQL_ROW_ADDED|La riga è stata inserita da **SQLBulkOperations**. Se la riga viene nuovamente recuperata o viene aggiornata da **SQLSetPos**, lo stato viene SQL_ROW_SUCCESS.<br /><br /> Questo valore non è impostato da **SQLFetch** o **SQLFetchScroll**.|  
|SQL_ROW_NOROW|Il set di righe ha sovrapposto la fine del set di risultati e non è stata restituita alcuna riga corrispondente a questo elemento della matrice di stato della riga.|
