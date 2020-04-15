---
title: 'Cursori dinamici ODBC : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], dynamic
- dynamic cursors [ODBC]
ms.assetid: de709fd3-9eb2-44e1-a2f0-786e2b9602a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f94b83ef1458cd9f8368d1bea3a39682bd80b1a2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302323"
---
# <a name="odbc-dynamic-cursors"></a>Cursori dinamici ODBC
Un cursore dinamico è proprio questo: dinamico. Può rilevare eventuali modifiche apportate all'appartenenza, all'ordine e ai valori del set di risultati dopo l'apertura del cursore. Si supponga, ad esempio, che un cursore dinamico recuperi due righe e un'altra applicazione aggiorni in seguito una di queste righe ed elimini l'altra. Se il cursore dinamico tenta quindi di recuperare nuovamente le righe, non troverà la riga eliminata, ma restituirà i nuovi valori per la riga aggiornata.  
  
 I cursori dinamici rilevano tutti gli aggiornamenti, le eliminazioni e gli inserimenti, sia propri che quelli effettuati da altri. Questo è soggetto al livello di isolamento della transazione, come impostato dall'attributo di connessione SQL_ATTR_TXN_ISOLATION. La matrice di stato della riga specificata dall'attributo statement SQL_ATTR_ROW_STATUS_PTR riflette queste modifiche e può contenere SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO, SQL_ROW_ERROR, SQL_ROW_UPDATED e SQL_ROW_ADDED. Non può restituire SQL_ROW_DELETED perché un cursore dinamico non restituisce righe eliminate all'esterno del set di righe e pertanto non riconosce più l'esistenza della riga eliminata nel set di risultati o l'elemento corrispondente nella matrice di stato della riga. SQL_ROW_ADDED viene restituita solo quando una riga viene aggiornata da una chiamata a **SQLSetPos**, non quando viene aggiornata da un altro cursore.  
  
 Un modo per implementare i cursori dinamici nel database consiste nel creare un indice selettivo che definisce l'appartenenza e l'ordinamento del set di risultati. Poiché l'indice viene aggiornato quando altri utenti apportano modifiche, un cursore basato su tale indice è sensibile a tutte le modifiche. Una selezione aggiuntiva all'interno del set di risultati definito da questo indice è possibile elaborando lungo l'indice.  
  
 I cursori dinamici possono essere simulati richiedendo che il set di risultati venga ordinato da un tasto univoco. Con tale restrizione, i recuperi vengono eseguiti eseguendo un'istruzione **SELECT** ogni volta che il cursore recupera le righe. Si supponga, ad esempio, che il set di risultati sia definito da questa istruzione:For example, suppose the result set is defined by this statement:  
  
```  
SELECT * FROM Customers ORDER BY Name, CustID  
```  
  
 Per recuperare il set di righe successivo in questo set di risultati, il cursore simulato imposta i parametri nella seguente istruzione **SELECT** sui valori nell'ultima riga del set di righe corrente e quindi lo esegue:  
  
```  
SELECT * FROM Customers WHERE (Name > ?) AND (CustID > ?)  
   ORDER BY Name, CustID  
```  
  
 Questa istruzione crea un secondo set di risultati, il primo set di righe il cui set di righe successivo nel set di risultati originale, in questo caso il set di righe nella tabella Customers. Il cursore restituisce questo set di righe all'applicazione.  
  
 È interessante notare che un cursore dinamico implementato in questo modo crea effettivamente molti set di risultati, che consente di rilevare le modifiche al set di risultati originale. L'applicazione non viene mai a conoscenza dell'esistenza di questi set di risultati ausiliari; viene semplicemente visualizzato come se il cursore fosse in grado di rilevare le modifiche al set di risultati originale.
