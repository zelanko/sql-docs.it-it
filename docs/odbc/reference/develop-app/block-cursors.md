---
title: Bloccare i cursori | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc62e7b5225c434bac33630f2f0cf8f39c72bfc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199298"
---
# <a name="block-cursors"></a>Cursori rettangolari
Molte applicazioni impiegano una quantità significativa di tempo che i dati attraverso la rete. Parte di questo tempo viene impiegato effettivamente portando i dati attraverso la rete e una parte viene impiegata per la diminuzione del sovraccarico, rete, ad esempio la chiamata eseguita dal driver per richiedere una riga di dati. Il tempo di quest'ultimo può essere ridotto se l'applicazione effettua un uso efficiente delle *blocco* o *fat* *cursori,* che può restituire più di una riga alla volta.  
  
 Sempre un'applicazione ha la possibilità di utilizzare un cursore a blocchi. Origini dati da cui può essere recuperata solo una riga alla volta, cursori a blocchi devono essere simulati nel driver. Questa operazione può essere eseguita mediante l'esecuzione di più operazioni di recupero di riga singola. Si tratta probabilmente non forniscono alcun miglioramento delle prestazioni, viene aperto opportunità per le applicazioni. Queste applicazioni si verificheranno quindi un aumento delle prestazioni come parte dei DBMS implementare cursori a blocchi in modo nativo e li espongono i driver associati a tali DBMS.  
  
 Le righe restituite in un'unica operazione di recupero con un cursore a blocchi vengono chiamate i *set di righe*. È importante non confondere il set di righe con il set di risultati. Il set di risultati viene mantenuto nell'origine dati, mentre il set di righe viene mantenuto nel buffer dell'applicazione. Mentre il set di risultati viene risolto, il set di righe non - cambia posizione e il contenuto ogni volta che viene recuperato un nuovo set di righe. Proprio come un cursore a riga singola, ad esempio i punti di cursore forward-only SQL tradizionali a una riga corrente, un cursore a blocchi punta al set di righe, che può essere considerata *righe correnti*.  
  
 Per eseguire operazioni che operano su una singola riga quando sono state recuperate più righe, l'applicazione prima di tutto necessario indicare quale riga è la riga corrente. La riga corrente viene richiesto dalle chiamate a **SQLGetData** e aggiornamento posizionato ed eliminare le istruzioni. Quando un cursore a blocchi termina prima di tutto un set di righe, la riga corrente è la prima riga del set di righe. Per modificare la riga corrente, l'applicazione chiama **SQLSetPos** oppure **SQLBulkOperations** (per l'aggiornamento tramite segnalibro). Nella figura seguente mostra la relazione tra il set di risultati, set di righe, riga corrente, set di righe cursore e cursore a blocchi. Per altre informazioni, vedere [cursori a blocchi usando](../../../odbc/reference/develop-app/using-block-cursors.md)più avanti in questa sezione, e [istruzioni di eliminazione e aggiornamento posizionato](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) e [aggiornamento dei dati con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
 ![Recupero del successivo, precedente, primo e ultimo set di righe](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 Se un cursore è un cursore a blocchi è indipendente dal fatto che è scorrevole. Ad esempio, la maggior parte del lavoro in un'applicazione di report viene impiegata per il recupero e la stampa di righe. Per questo motivo, verranno eseguiti più rapidamente con un tipo forward-only, cursore a blocchi. Usa un cursore forward-only per evitare le spese di un cursore scorrevole e un cursore a blocchi per ridurre il traffico di rete.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione di colonne per l'utilizzo con cursori rettangolari](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [Utilizzo di cursori rettangolari](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [Matrice di stato riga](../../../odbc/reference/develop-app/row-status-array.md)
