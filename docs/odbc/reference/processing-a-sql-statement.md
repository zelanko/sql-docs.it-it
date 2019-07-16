---
title: Elaborazione di un'istruzione SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], processing
- SQL [ODBC], processing statements
- statement processing [ODBC]
- SQL statements [ODBC]
- ODBC [ODBC], SQL
ms.assetid: 96270c4f-2efd-4dc1-a985-ed7fd5658db2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dfbf23f0be369ae540dac33d33a3e3c1505d5ebe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076286"
---
# <a name="processing-a-sql-statement"></a>Elaborazione di un'istruzione SQL
Prima di illustrare le tecniche per l'utilizzo a livello di codice SQL, è necessario discutere le modalità di elaborazione di un'istruzione SQL. I passaggi necessari sono comuni a tutte le tre tecniche, anche se ogni tecnica vengono eseguite in momenti diversi. Nella figura seguente vengono illustrati i passaggi coinvolti nell'elaborazione di un'istruzione SQL, che sono illustrati nella parte restante di questa sezione.  
  
 ![Passaggi per l'elaborazione di un'istruzione SQL](../../odbc/reference/media/pr01.gif "pr01")  
  
 Per elaborare un'istruzione SQL, un DBMS esegue i cinque passaggi seguenti:  
  
1.  Il sistema DBMS analizza innanzitutto l'istruzione SQL. Interrompe l'istruzione in singole parole, denominate tokens, assicura che l'istruzione include un verbo valido e le clausole valide e così via. In questo passaggio possono essere rilevati gli errori di ortografia e gli errori di sintassi.  
  
2.  Il sistema DBMS convalida l'istruzione. Controlla l'istruzione sul catalogo di sistema. Tutte le tabelle denominate nell'istruzione presenti nel database? Tutte le colonne esistenti e i nomi delle colonne non sono ambigui? L'utente dispone dei privilegi necessari per eseguire l'istruzione? Alcuni errori semantici possono essere rilevati in questo passaggio.  
  
3.  Il sistema DBMS genera un piano di accesso per l'istruzione. Il piano di accesso è una rappresentazione binaria dei passaggi necessari per eseguire l'istruzione. è l'equivalente DBMS di codice eseguibile.  
  
4.  Il sistema DBMS consente di ottimizzare il piano di accesso. Illustra vari modi per eseguire il piano di accesso. Un indice consente di velocizzare la ricerca? Dovrebbe DBMS innanzitutto applicare una condizione di ricerca a una tabella e quindi aggiungerla alla tabella B o deve iniziare con l'aggiunta e usare la condizione di ricerca in un secondo momento? Una ricerca sequenziale tramite una tabella è può essere evitata o ridotto a un subset della tabella? Dopo avere esplorato le alternative, il sistema DBMS sceglie uno di essi.  
  
5.  Il sistema DBMS esegue l'istruzione, eseguire il piano di accesso.  
  
 I passaggi necessari per elaborare un'istruzione SQL variano nella quantità richiedono l'accesso al database e la quantità di tempo che necessario. L'analisi di un'istruzione SQL non richiede l'accesso al database e possono essere eseguita molto rapidamente. Ottimizzazione, d'altra parte, è un elevato della CPU di elaborare e richiede l'accesso al catalogo di sistema. Per una query complessa, riferita, query optimizer può esplorare migliaia diversi modi di eseguire la stessa query. Tuttavia, il costo dell'esecuzione della query in modo inefficiente in genere è talmente elevato che il tempo impiegato nell'ottimizzazione riacquisito più di velocità di esecuzione maggiore di query. Si tratta ancora più significativo se lo stesso piano di accesso ottimizzata è possibile utilizzare più volte per eseguire le query ricorrenti.
