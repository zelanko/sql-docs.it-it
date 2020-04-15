---
title: Cursori a blocchi Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 1a92b5d8-7c6e-4ce5-8c99-600a387026aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa35888ef93da9648fe6422bdc35ebf9da3a0525
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306352"
---
# <a name="block-cursors"></a>Cursori rettangolari
Molte applicazioni impiegano una notevole quantità di tempo per portare i dati in rete. Parte di questo tempo viene speso effettivamente portando i dati attraverso la rete, e parte di esso viene speso per l'overhead di rete, ad esempio la chiamata effettuata dal driver per richiedere una riga di dati. Quest'ultimo tempo può essere ridotto se l'applicazione fa un uso efficiente di *cursori a blocchi,* o *grassi,* *cursors,* che possono restituire più di una riga alla volta.  
  
 Un'applicazione ha sempre la possibilità di utilizzare un cursore a blocchi. Nelle origini dati da cui è possibile recuperare solo una riga alla volta, è necessario simulare i cursori a blocchi nel driver. Questa operazione può essere eseguita eseguendo più recuperi a riga singola. Anche se è improbabile che ciò fornisca miglioramenti delle prestazioni, apre opportunità per le applicazioni. Tali applicazioni subiranno quindi un aumento delle prestazioni man mano che i DBSMO implementano i cursori a blocchi in modo nativo e i driver associati a tali DBS li espongono.  
  
 Le righe restituite in un singolo recupero con un cursore a blocchi sono denominate *rowset*. È importante non confondere il set di righe con il set di risultati. Il set di risultati viene mantenuto nell'origine dati, mentre il set di righe viene mantenuto nei buffer dell'applicazione. Mentre il set di risultati è fisso, il set di righe non lo è: cambia posizione e contenuto ogni volta che viene recuperato un nuovo set di righe. Proprio come un cursore a riga singola, ad esempio il tradizionale cursore forward-only SQL, punta a una riga corrente, un cursore a blocchi punta al set di righe, che può essere considerato come *righe correnti*.  
  
 Per eseguire operazioni che operano su una singola riga quando sono state recuperate più righe, l'applicazione deve innanzitutto indicare quale riga è la riga corrente. La riga corrente è richiesta dalle chiamate a **SQLGetData** e dalle istruzioni di aggiornamento ed eliminazione posizionate. Quando un cursore di blocco restituisce innanzitutto un set di righe, la riga corrente è la prima riga del set di righe. Per modificare la riga corrente, l'applicazione chiama **SQLSetPos** o **SQLBulkOperations** (per aggiornare in base al segnalibro). Nella figura seguente viene illustrata la relazione del set di risultati, del set di righe, della riga corrente, del cursore del set di righe e del cursore a blocchi. Per ulteriori informazioni, vedere Utilizzo dei [cursori](../../../odbc/reference/develop-app/using-block-cursors.md)a blocchi , più avanti in questa sezione e [Istruzioni di aggiornamento ed eliminazione posizionate](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) e Aggiornamento dei dati con [SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
 ![Recupero del rowset successivo, precedente, primo e ultimo](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 Se un cursore è un cursore di blocco è indipendente dal fatto che sia scorrevole. Ad esempio, la maggior parte del lavoro in un'applicazione di report viene impiegato per il recupero e la stampa di righe. Per questo motivo, funzionerà più velocemente con un cursore a blocchi forward-only. Utilizza un cursore forward-only per evitare le spese di un cursore scorrevole e un cursore a blocchi per ridurre il traffico di rete.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione di colonne per l'uso con cursori rettangolari](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [Uso di cursori rettangolari](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [Matrice di stato riga](../../../odbc/reference/develop-app/row-status-array.md)
