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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076286"
---
# <a name="processing-a-sql-statement"></a>Elaborazione di un'istruzione SQL
Prima di illustrare le tecniche per l'utilizzo di SQL a livello di codice, è necessario illustrare il modo in cui viene elaborata un'istruzione SQL. I passaggi necessari sono comuni a tutte e tre le tecniche, sebbene ciascuna tecnica le esegua in momenti diversi. Nella figura seguente vengono illustrati i passaggi necessari per l'elaborazione di un'istruzione SQL, descritti nella parte restante di questa sezione.  
  
 ![Passaggi per l'elaborazione di un'istruzione SQL](../../odbc/reference/media/pr01.gif "PR01")  
  
 Per elaborare un'istruzione SQL, un sistema DBMS esegue i cinque passaggi seguenti:  
  
1.  Il sistema DBMS analizza prima di tutto l'istruzione SQL. Suddivide l'istruzione in singole parole, denominate token, verifica che l'istruzione includa un verbo valido e clausole valide e così via. In questo passaggio è possibile rilevare errori di sintassi e errori di ortografia.  
  
2.  Il sistema DBMS convalida l'istruzione. Consente di controllare l'istruzione rispetto al catalogo di sistema. Tutte le tabelle denominate nell'istruzione esistono nel database? Sono presenti tutte le colonne e i nomi di colonna non sono ambigui? L'utente dispone dei privilegi necessari per eseguire l'istruzione? In questo passaggio è possibile rilevare alcuni errori semantici.  
  
3.  Il sistema DBMS genera un piano di accesso per l'istruzione. Il piano di accesso è una rappresentazione binaria dei passaggi necessari per eseguire l'istruzione; si tratta dell'equivalente DBMS del codice eseguibile.  
  
4.  Il sistema DBMS ottimizza il piano di accesso. Vengono esaminati vari modi per eseguire il piano di accesso. È possibile usare un indice per velocizzare la ricerca? Il sistema DBMS applica prima di tutto una condizione di ricerca alla tabella A, quindi la aggiunge alla tabella B oppure deve iniziare con il join e usare la condizione di ricerca in un secondo momento? Una ricerca sequenziale in una tabella può essere evitata o ridotta a un subset della tabella? Dopo aver esplorato le alternative, il sistema DBMS ne sceglie una.  
  
5.  Il sistema DBMS esegue l'istruzione eseguendo il piano di accesso.  
  
 I passaggi usati per elaborare un'istruzione SQL variano a seconda della quantità di accesso al database richiesta e del tempo necessario. L'analisi di un'istruzione SQL non richiede l'accesso al database e può essere eseguita molto rapidamente. L'ottimizzazione, d'altra parte, è un processo con utilizzo intensivo della CPU e richiede l'accesso al catalogo di sistema. Per una query complessa con più tabelle, Query Optimizer può esplorare migliaia di modi diversi per eseguire la stessa query. Tuttavia, il costo di esecuzione della query in modo inefficiente è in genere così elevato che il tempo impiegato per l'ottimizzazione è maggiore rispetto a quello recuperato in una maggiore velocità di esecuzione delle query. Questo è ancora più significativo se lo stesso piano di accesso ottimizzato può essere utilizzato più volte per eseguire query ripetitive.
