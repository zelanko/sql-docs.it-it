---
title: Cursori a blocchi | Microsoft Docs
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
ms.openlocfilehash: 3e0ea6ff655140c979f400f67a59cd7259bac9e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118824"
---
# <a name="block-cursors"></a>Cursori rettangolari
Molte applicazioni dedicano una quantità significativa di tempo a trasferire i dati attraverso la rete. Parte di questo periodo di tempo viene impiegato per portare i dati attraverso la rete e parte di esso viene impiegato per un sovraccarico di rete, ad esempio la chiamata eseguita dal driver per richiedere una riga di dati. Il secondo tempo può essere ridotto se l'applicazione utilizza in modo efficiente i *cursori* *Block,* o *FAT* , che possono restituire più di una riga alla volta.  
  
 Un'applicazione ha sempre la possibilità di usare un cursore a blocchi. Sulle origini dati da cui è possibile recuperare solo una riga alla volta, è necessario simulare i cursori a blocchi nel driver. Questa operazione può essere eseguita eseguendo più recuperi a riga singola. Sebbene sia improbabile che si ottenga un miglioramento delle prestazioni, si aprono opportunità per le applicazioni. Tali applicazioni, quindi, comportano un aumento delle prestazioni poiché i DBMS implementano i cursori a blocchi in modo nativo e i driver associati a tali DBMS li espongono.  
  
 Le righe restituite in una singola operazione di recupero con un cursore a blocchi sono denominate *set di righe*. È importante non confondere il set di righe con il set di risultati. Il set di risultati viene mantenuto nell'origine dati, mentre il set di righe viene mantenuto nei buffer dell'applicazione. Mentre il set di risultati è fisso, il set di righe non è-modifica la posizione e il contenuto ogni volta che viene recuperato un nuovo set di righe. Proprio come un cursore a riga singola, ad esempio il cursore tradizionale SQL di sola riga, fa riferimento a una riga corrente, un cursore a blocchi punta al set di righe, che può essere considerato come *righe correnti*.  
  
 Per eseguire operazioni che operano su una singola riga quando sono state recuperate più righe, l'applicazione deve prima indicare quale riga è la riga corrente. La riga corrente è richiesta dalle chiamate a **SQLGetData** e alle istruzioni Update e Delete posizionate. Quando un cursore a blocchi restituisce innanzitutto un set di righe, la riga corrente è la prima riga del set di righe. Per modificare la riga corrente, l'applicazione chiama **SQLSetPos** o **SQLBulkOperations** (per aggiornare tramite segnalibro). Nella figura seguente viene illustrata la relazione tra il set di risultati, il set di righe, la riga corrente, il cursore del set di righe e il cursore a Per ulteriori informazioni, vedere [utilizzo di cursori a blocchi](../../../odbc/reference/develop-app/using-block-cursors.md), più avanti in questa sezione, e [posizionamento delle istruzioni Update e Delete](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) e [aggiornamento dei dati con SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md).  
  
 ![Recupero del rowset successivo, precedente, primo e ultimo](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 Se un cursore è un cursore a blocchi è indipendente dal fatto che sia scorrevole o meno. La maggior parte del lavoro in un'applicazione di report, ad esempio, è dedicata al recupero e alla stampa delle righe. Per questo motivo, funzionerà più velocemente con un cursore di blocco di sola trasmissione. Usa un cursore di sola trasmissione per evitare i costi di un cursore scorrevole e un cursore a blocchi per ridurre il traffico di rete.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione di colonne per l'uso con cursori rettangolari](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [Uso di cursori rettangolari](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [Matrice di stato riga](../../../odbc/reference/develop-app/row-status-array.md)
