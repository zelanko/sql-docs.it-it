---
title: Compilazione di un programma SQL incorporato Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- compiling embedded SQL programs [ODBC]
- embedded SQL [ODBC]
ms.assetid: 9e94146a-5b80-4a01-b586-1e03ff05b9ac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb801dc532009410055b67031b3e036cc6b9c3d0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306532"
---
# <a name="compiling-an-embedded-sql-program"></a>Compilazione di un programma Embedded SQL
Poiché un programma SQL incorporato contiene una combinazione di istruzioni SQL e del linguaggio host, non può essere inviato direttamente a un compilatore per il linguaggio host. Al contrario, viene compilato tramite un processo a più passaggi. Anche se questo processo differisce da prodotto a prodotto, i passaggi sono più o meno gli stessi per tutti i prodotti.  
  
 Questa illustrazione mostra i passaggi necessari per compilare un programma SQL incorporato.  
  
 ![Passaggi per la compilazione di un programma SQL incorporato](../../odbc/reference/media/pr02.gif "pr02 (in questo pr02)")  
  
 Cinque passaggi sono coinvolti nella compilazione di un programma SQL incorporato:  
  
1.  Il programma SQL incorporato viene inviato al precompilatore SQL, uno strumento di programmazione. Il precompilatore analizza il programma, trova le istruzioni SQL incorporate e le elabora. È necessario un precompilatore diverso per ogni linguaggio di programmazione supportato dal DBMS. I prodotti DBMS offrono in genere precompilatori per uno o più linguaggi, tra cui C, Pascal, COBOL, Fortran, Ada, PL/I e vari linguaggi di assembly.  
  
2.  Il precompilatore produce due file di output. Il primo file è il file di origine, privo delle istruzioni SQL incorporate. Al loro posto, il precompilatore sostituisce le chiamate a routine DBMS proprietarie che forniscono il collegamento di runtime tra il programma e il DBMS. In genere, i nomi e le sequenze di chiamata di queste routine sono noti solo al precompilatore e al DBMS; non sono un'interfaccia pubblica per il DBMS. Il secondo file è una copia di tutte le istruzioni SQL incorporate utilizzate nel programma. Questo file viene talvolta chiamato modulo di richiesta del database, o DBRM.  
  
3.  L'output del file di origine del precompilatore viene inviato al compilatore standard per il linguaggio di programmazione host (ad esempio un compilatore C o COBOL). Il compilatore elabora il codice sorgente e produce codice oggetto come output. Si noti che questo passaggio non ha nulla a che fare con il DBMS o con SQL.  
  
4.  Il linker accetta i moduli oggetto generati dal compilatore, li collega a varie routine di libreria e produce un programma eseguibile. Le routine di libreria collegate al programma eseguibile includono le routine DBMS proprietarie descritte nel passaggio 2.  
  
5.  Il modulo di richiesta del database generato dal precompilatore viene inviato a un'utilità di associazione speciale. Questa utilità esamina le istruzioni SQL, le analizza, le convalida e le ottimizza, quindi produce un piano di accesso per ogni istruzione. Il risultato è un piano di accesso combinato per l'intero programma, che rappresenta una versione eseguibile delle istruzioni SQL incorporate. L'utilità di associazione archivia il piano nel database, assegnandogli in genere il nome del programma applicativo che lo utilizzerà. L'esecuzione di questo passaggio in fase di compilazione o di esecuzione dipende dal sistema DBMS.  
  
 Si noti che i passaggi utilizzati per compilare un programma SQL incorporato sono strettamente correlati ai passaggi descritti in precedenza in [Elaborazione di un'istruzione SQL](../../odbc/reference/processing-a-sql-statement.md). In particolare, si noti che il precompilatore separa le istruzioni SQL dal codice del linguaggio host e l'utilità di associazione analizza e convalida le istruzioni SQL e crea i piani di accesso. Nei DBSMO in cui il passaggio 5 viene eseguito in fase di compilazione, i primi quattro passaggi dell'elaborazione di un'istruzione SQL vengono eseguiti in fase di compilazione, mentre l'ultimo passaggio (esecuzione) viene eseguito in fase di esecuzione. Questo ha l'effetto di rendere l'esecuzione delle query in tali DBS molto veloce.
